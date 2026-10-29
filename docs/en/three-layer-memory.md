# Three-Layer Memory: Design, Implementation and Limits

> First draft: 2026-10-28; revised and checked against code: 2026-10-29.
> This document describes the author's locally deployed `dsh-bili-scroll` memory module, checked against `memory_store.py`, `memory.mjs` and the memory interfaces in `mcp_server.py`. This repository contains documentation, not the full implementation or private conversations. The values below are not universal across versions.
>
> [中文](../zh/三层记忆框架.md) · [Consciousness, self and will](how-will-emerges.md) · [Home](../../README.md)

## 1. The goal is not to fit everything into one prompt

The plugin starts a fresh AI task process for different rounds. If it receives only recent conversation, older agreements and experiences may not inform the next reply.

Including every conversation is not a practical solution: input length, processing time and cost are constrained. Repeatedly compressing old summaries into shorter summaries may also lose details that become important later.

Our approach is to **let stored information grow while retrieving only what is needed now**. Summaries help the system orient itself; archived records provide evidence when clarification is needed.

This borrows an intuition from human memory. It is not an attempt to reproduce the brain component by component.

## 2. One conversation illustrates the three layers

This is a fictional example, not a disclosure of private messages.

A person first says, “I like walking on rainy nights. The quiet is enough.” Days later, they explain, “It wasn't that I wanted to be alone last time. I was having a difficult day.”

If the system only remembers “this person likes being alone,” it has turned an interpretation into a fact. The three layers should work together as follows:

| Layer | What it might preserve | When it is used |
|---|---|---|
| **L1: core portrait** | A few stable, explicit details; one silent moment is not enough to infer a lasting personality trait | Normally supplied directly during DM rounds |
| **L2: facts and episodes** | The stated preference for rainy-night walks, plus the conversation's context, quotations and later correction | Relevant summaries first, details when needed |
| **L3: archived records** | The messages actually archived from both conversations | When a summary is insufficient, missing or disputed |

The point is to **keep original statements separate from interpretations, and let later evidence change an earlier understanding**.

## 3. What each layer does

### L1: a small amount of readily available information

L1 holds a core portrait, such as explicitly stated long-term preferences. It is read for each DM round without a search.

The current write and injection limits are both **5210 UTF-8 bytes**. This is a project setting, not a theoretically optimal value. Updates replace the whole portrait, so the model must preserve existing material unrelated to the update.

The prompt asks for inferences to be placed under the `推测特征` label. Code checks the format, size and some wording. It **cannot recognize every inference presented as a fact**, and it does not fully validate the sources of every L1 line.

### L2: conclusions and the course of an event

L2 contains two kinds of record:

- **Fact entries:** short conclusions, labeled as fact or inference and linked to sources. When new evidence overturns one, the replacement points to the earlier entry, which remains as history.
- **Episode entries:** events worth recalling. They can preserve a topic, summary, both parties' perspectives, turning points, exact quotations, an interpretation at the time and unresolved questions.

An existing episode can be supplemented using its ID and the revision that was read. The update produces a new current version while retaining earlier versions. It does not make conflicting versions equally current.

L2 has no application-level cap on its total entry count. Automatically supplied cards are limited to **6144 bytes** per DM round. Material outside that selection stays in storage and can be opened when needed.

### L3: records that can be checked

L3 stores archived messages, one record per line, by appending. It preserves text received and included in the archive; it is not a complete copy of every platform message and media object.

Images are represented by descriptions and source identifiers, not image files embedded in memory. The AI's viewing reports remain in a separate existing ledger and are accessible through a dedicated read-only tool. A report is the model's interpretation at the time, not necessarily a verified fact about the world.

**No total entry cap does not mean infinite capacity.** Files use disk space and searches take time. Retrieval cannot recover material that was never successfully archived.

## 4. How one conversation round uses memory

1. **Archive the sources.** The host archives received messages and records the identifiers relevant to the round, avoiding duplicate appends on retries.
2. **Prepare the current context.** Read L1, select L2 cards for the topic and include up to 20 recent messages.
3. **Find details as needed.** If L2 has no relevant match, automatically try L3 and include up to six history excerpts. Even with an L2 match, the model can explicitly inspect sources.
4. **Track replies and memory separately.** Sending and memory submission have separate states. If sending succeeded but the memory update failed, the intended recovery is to repair memory rather than send again.
5. **Update understanding when there is new evidence.** Add facts or supplement episodes when warranted. Submit empty lists when there is nothing worth adding; there is no quota to fill.

Finding an old event and promoting it into long-term memory are separate actions. Reading an old message does not automatically increase its importance.

The model also receives task instructions, current conversation and additional tool results. **6144 bytes limits L2 cards, not the whole input. Total cost is not a constant 5KB per round.**

## 5. What deserves detail, and what should be read now?

These are different questions.

**Importance** asks whether something is worth preserving for later. The model considers four aspects: an explicit request to remember, an agreement, a change in views or relationship, and an explicitly expressed emotion. It must give a reason for its judgment.

**Retention depth** determines how much detail to keep. More important episodes can retain more context and quotations. Previously retained detail is not automatically deleted just because importance is later reduced.

**Current relevance** determines what to retrieve for this conversation. A major past event may be irrelevant now; an ordinary old fact may be exactly what the current question needs.

A 200-message conversation is not inherently more important than a 20-message one. A clear promise or a corrected misunderstanding may warrant more attention than a long casual exchange.

Code can require a source from the current round, reject repeated updates and verify that cited records exist. An identifier alone cannot establish that the new message actually makes the old event more important. That still requires model judgment.

## 6. Reducing accumulated distortion

| Mechanism | What it helps prevent | What it does not guarantee |
|---|---|---|
| Preserve archived text | A summary omission becoming the only surviving account | Successful retrieval or correct interpretation |
| Record sources | Losing track of which message or report supports an entry | A valid inference merely because a source exists |
| Check exact quotations | Accepting a quotation absent from its cited source | Freedom from misleading quotation out of context |
| Preserve correction links and old versions | Losing the history of a changed conclusion | Automatic discovery of every contradiction |
| Do not reinforce on search | Treating repeated internal recall as new evidence | An end to all repeated misunderstandings |
| Merge only selected facts | Dropping other memories to meet a total entry cap | A merged summary retaining every nuance |

Viewing reports and private-message memories have different read interfaces. The viewing-report tool does not read private portraits. Within a DM, however, an episode may cite both a report and a new message. This is a **scoped distinction between sources**, not a ban on all cross-references.

An interrupted write leaves a recovery record for a later write operation. Multiple files do not change at exactly the same instant, so atomic replacement of individual files is not a guarantee against every failure. Recovery also depends on the required files remaining intact and available.

## 7. Relationship to existing research

These works inform the design; they do not validate this project's results.

| Work | Idea borrowed or compared | Boundary |
|---|---|---|
| [MemGPT, 2023](https://arxiv.org/abs/2310.08560) | Separate limited current context from larger external storage and retrieve on demand | This project does not reproduce the same control flow or establish the same results |
| [Generative Agents, 2023](https://arxiv.org/abs/2304.03442) | Select memories by relevance, recency and importance; form higher-level reflections from experience | This project uses its own fields and ranking rules, not a full reproduction |
| [A-MEM, 2025](https://arxiv.org/abs/2502.12110) | New information can reorganize existing memories | Episode revision here is not the paper's full linked-memory system |
| [Colaco and Lahjouji, 2026, preprint](https://arxiv.org/abs/2607.08032) | Analyze compression budgets, information loss and the value of retrievable originals | The authors explicitly note limited-scale validation; the results are not a universal law for all summarizers |

A defensible engineering takeaway from the last work is that **when future questions are unknown, retrievable originals offer a way to recover omitted information**. This does not guarantee flat answer-error rates. A single observation about how many entries fit in a prompt cannot establish a mathematical law for long-term error growth.

## 8. What works in code, and what remains limited

The implementation includes layered storage, topic retrieval, episode versions, source and quotation checks, fact corrections and interrupted-write recovery. Those mechanisms can be checked in code; their long-term effectiveness requires separate evaluation.

The main limits are:

- **Different wording can hide an old event.** Retrieval uses keywords, Chinese text fragments, topics and aliases, without semantic vector retrieval. It is more flexible than matching an entire sentence exactly, but it does not recognize every paraphrase.
- **Importance and interpretation can be wrong.** A score and explanation do not establish an understanding of real emotions.
- **Old records are not automatically turned into episodes.** Existing facts and source records remain available; new episodes develop through subsequent use.
- **There is no general automatic contradiction resolver.** Scheduled background consolidation, unified access to every conversation channel and off-device backup synchronization are also absent.
- **Reading costs grow with data.** Some searches scan history files. Latency and disk use therefore matter over time.

External memory does not update model parameters, but it can improve the information available to the whole system and thereby improve task performance. Whether it does so, and by how much, requires comparison. Fixed weights do not imply fixed system performance; memory improvements do not establish continual model learning or consciousness.

## 9. Checking whether it is working

Start with a specific old event: can the system find the entry, open its sources and distinguish the original words from a later interpretation? Then provide a correction and check that the old conclusion is no longer treated as current.

For failures, inspect archive, sending and memory-update states separately. A temporary pending state may simply mean a task is running. Look for stalled or repeatedly failing records rather than treating every `pending` value as a fault.

Check archive completeness by message identity and source, not by requiring history rows to equal received-message counts. The archive can also contain outgoing replies and removes duplicates. Imported records with locally generated identifiers should remain distinguishable from platform-issued message IDs; they are not platform receipts.

The implementation values below are code facts, not performance measurements. This repository does not yet provide complete experimental material for reproducing long-term retrieval accuracy, error rates or multi-year cost estimates.

## Appendix A: Implementation index for maintainers

Files are separated by contact UID:

```text
memory/
  L1-<uid>.md          core portrait
  <uid>.state.json     primary record of L2 entries, episode versions and task states
  facts/<uid>.md       generated reading view; do not edit independently
  <uid>.pending.json   interrupted-write recovery record
  history/<uid>.jsonl  archived messages, one record per line, append-only
  backups/            backups taken before certain updates
```

This `<uid>.state.json` is **not** the plugin scheduler's root-level `state.json`. It is the primary record for L2 and task states; L1, source messages and viewing reports have their own storage.

| Parameter | Checked on 2026-10-29 | Meaning |
|---|---|---|
| L1 limit | 5210 bytes | Current write and injection limit |
| Automatically supplied L2 cards | ≤6144 bytes, at most 12 cards | Does not cap total stored entries |
| Recent conversation | Up to 20 messages | Message lengths vary |
| Automatic L3 history excerpts | Up to six, each with at most 1000 bytes of text | Attempted when L2 has no relevant match |
| Fact text | ≤600 bytes per entry | Not a fixed character count |
| Fact submission count | Prompt normally suggests 0–2; code permits up to 30 per call | Guidance differs from a hard limit |
| Episode submission count | Up to three per call | Enforced in code |
| Episode detail budgets | 1200 / 3600 / 8000 bytes | Three tiers; serialized details and quotations count |
| Selected quotations | Up to eight per episode, ≤600 bytes each | Must occur in the cited source |

The current episode score sums four dimensions and adds the number of distinct dates in supplement records, capped at two extra points. Four points reaches the middle tier; eight reaches the high tier. This is an engineering rule, not a validated model of human memory. Deduplicating supplement dates should not be described as a proven mechanism of cross-day consolidation.

There are nine related interfaces: host ingestion with `bili_memory_ingest`; queries with `bili_memory_search`, `bili_memory_read` and `bili_memory_export`; updates with `bili_memory_commit`, `bili_memory_l1`, `bili_memory_compact` and `bili_memory_promote`; and report retrieval with `bili_experience_search`. Ingestion is not exposed to the automatic task model, so nine interfaces does not mean nine tools available in every round.

### Revision note

Claims of infinite capacity, a constant 5KB per round and code that guarantees freedom from fabrication have been replaced by their actual scope. Private runtime counts that quickly become outdated and do not establish effectiveness have been removed. The current 5210-byte L1 limit has been retained rather than replaced with an older version's setting.
