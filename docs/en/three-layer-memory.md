# Three-Layer Memory — A Technical Specification

> Version: 2026-10-28 (episode layer)
> Code: `memory_store.py` (688 lines / 41.4 KB), `memory.mjs` (174 lines / 12.4 KB), memory section of `mcp_server.py`
> Memory tools: 9 (`bili_memory_*` × 8 + `bili_experience_search` × 1)
> Data directory: `<home>/.dsh/bili-duty/memory/`

---

## 1. The Problem It Solves

Every DM round is a **fresh headless process** that dies when it finishes.

Without this system:
- Each round sees only the last 20 messages; anything older is genuinely forgotten
- "Remembering more" means stuffing a longer context, which has a hard limit
- Past that limit, the model starts losing information in the middle (attention dilution)

**In one sentence**: it turns "how much can be remembered" from a **context-window** problem into a **storage + retrieval** problem.

---

## 2. The Three Layers

| Layer | Contents | Limit | How it is used | Update path |
|---|---|---|---|---|
| **L1 Core portrait** | Identity, explicit preferences, relationship | **≤5210 bytes** (currently 209) | **Injected in full every round** | `bili_memory_l1`, full rewrite, `tag: content` format |
| **L2 Long-term memory** | **Facts** (high/mid/low) + **episodes** | No total cap; **≤6144 bytes** of relevant cards per round | Cards selected by current topic; details expanded on demand | `bili_memory_commit`, 0–2 facts and 0–3 episodes per round |
| **L3 Raw history** | Every message verbatim (append-only) | Unlimited (currently 190 rows) | **Retrieval only**, never decoded into context | `bili_memory_ingest`, automatic |

### 2.1 Files and Their Roles

```
memory/
  L1-<uid>.md          core portrait (free text, tag format)
  facts/<uid>.md       L2 rendered projection (derived file, do not edit by hand)
  <uid>.state.json     source of truth: facts / episodes / tasks / operations
  <uid>.pending.json   exists only during a transaction; used for recovery
  history/<uid>.jsonl  L3 raw history (append-only)
  backups/             full backup taken before every compaction
```

> **Key point**: `state.json` is the truth; `facts.md` is only a projection. Edits to the markdown are overwritten on the next render.

### 2.2 Anatomy of an Episode

```
title             one-line subject
summary           ≤600 bytes
topics / aliases  keywords and aliases for retrieval
sources           list of msg_id values (must genuinely exist)
importance        {explicit, commitment, change, emotion}, each 0–3
importance_reason why those scores were given (the model's judgment, not the system's)
details           {context, user_view, assistant_view, turning_point,
                   interpretation, unresolved}
quotes            [{msg_id, text}] verbatim quotes (must appear verbatim in the sources)
revision          version number; supplements never overwrite
```

**Detail budget is set by the importance tier**: brief 1200 / standard 3600 / deep 8000 bytes.

---

## 3. Four Data Flows

```
① Write:   message arrives → raw text into L3 (with the real msg_id) → 0–3 L2 entries at round end
② Read:    L1 (full) + L2 (topic-selected ≤6144B) + last 20 messages + L3 retrieval hits (≤6)
③ Promote: an old event surfaces from L3 → bili_memory_promote → copied into L2 (L3 stays untouched)
④ Compact: L2 has duplicate facts → bili_memory_compact, selective merge (requires merge_ids,
            keeps every source); other memories are not touched
```

---

## 4. Nine Mechanisms

| # | Mechanism | Purpose |
|---|---|---|
| 1 | **Reversibility** | Raw history is never deleted or rewritten; failed compaction can always be recovered from L3 |
| 2 | **Traceable provenance** | Every entry carries a `msg_id`; `bili_memory_read` expands its context and earlier revisions |
| 3 | **Fact / inference separation** | Inferences must be labelled, and inside L1 they may only appear under `推测特征` (enforced in code) |
| 4 | **Correction chain** | `replaces` points at the superseded conclusion; a refuted conclusion cannot be revived |
| 5 | **Episode revisions** | Supplements do not overwrite; earlier revisions remain readable |
| 6 | **Three dimensions kept apart** | Importance ≠ retention depth ≠ momentary relevance |
| 7 | **Reinforcement only from new evidence** | Searching or recalling on its own does **not** count as experiencing something again (prevents self-reinforcing errors) |
| 8 | **Verbatim quote check** | A quote must appear verbatim in its source message; invented quotes are rejected |
| 9 | **Isolation** | The bot's own viewing reports (`bili_experience_search`) and the user's DM portrait never contaminate each other |

---

## 5. Promotion Criteria (L3→L2 and L2→L1)

### 5.1 L3 → L2

| Path | Trigger |
|---|---|
| Automatic | L3 is scanned **only when no relevant L2 entry matches** (saves budget when there is a match) |
| Active | `bili_memory_search(layer="history")` / `bili_memory_read` |
| Promotion | `bili_memory_promote(msg_id, …, evidence_msg_id, memory_id)` |

**Governing rule (from the prompt)**:

> **Merely recalling an old event does not raise its importance. Only a new message from the other party bringing it up again may deepen it.**

**Four importance dimensions (each 0–3)**:
`explicit` (an explicit request to remember), `commitment` (an agreement), `change` (a shift in view or relationship), `emotion` (explicitly expressed feeling).
`importance_reason` is mandatory; scoring must be **evidence-based, never by message count or retrieval count**.

**Hard code constraints**: the `msg_id` must exist in history; the evidence must exist; identical calls are deduplicated.

### 5.2 L2 → L1

> **Only when clear new evidence changes the core portrait**, update with `bili_memory_l1`, rewriting the whole file while **preserving unrelated existing content**.

| Constraint | Value |
|---|---|
| What may go in | Stable identity, explicit preferences, relationship (not "what we talked about") |
| Inference | **Only under `推测特征`**; enforced in code |
| Format | `tag: content` per line, tag 1–12 characters |
| Size | ≤5210 bytes |

**This is the most conservative step in the system.**

### 5.3 Who Decides

**The model judges; the code only guarantees "it can be traced".**
- Code enforces: provenance is real, format is legal, no fabrication, no duplication, no tampering
- Model decides: is it worth remembering, how important, and why

**The only objective signal**: re-mention across days (computed from `last_date`).
**Deliberately excluded**: message count and retrieval count (so that "I recalled it once" never becomes "it matters more").

---

## 6. Strengths

1. **Constant per-round context, unbounded history** — roughly 5 KB injected per round, and the same number after three years
2. **Resists "the more you summarise, the blurrier it gets"** — the rate–distortion literature predicts that repeated irreversible summarisation produces error growing **super-linearly** in the number of compactions, while reversible archives stay flat. Measured here: 59 facts squeezed into 4096 bytes left only **13 visible**
3. **Correctable and auditable** — "you said last time…" resolves to a concrete `msg_id` and the original text
4. **Failures are visible** — `archive / reply / memory` are recorded as three independent states; a failed reply does not corrupt memory, and a failed memory write never triggers a resend
5. **Conversation-first scheduling** — DM > mention > scrolling; detection never pauses during long rounds (10-second polling)

---

## 7. Costs and Weaknesses

1. **High complexity** — 41 KB of core code, 9 tools, 6 files. Three crashes in a single day (field overwrite, broken transaction, ID precision)
2. **Two-file consistency** — a window exists between `state.json` (truth) and `facts.md` (projection). A WAL covers most of it, but "markdown lagging behind state" remains possible
3. **Strong constraints create friction** — every fact must come from a real message, so the bot **cannot remember something from impression alone** (L1 is the only exception)
4. **Retrieval is literal, not semantic** — "that video that got me last time" will not be found unless those exact words appear. **Currently the largest functional gap**
5. **Rules depend on model compliance** — "at most 3 per round", "quotes must be verbatim": the system can **reject**, it cannot **fill in**
6. **Cost** — ~5 KB injected per round plus occasional read/export calls; compaction costs an extra model turn
7. **Self-produced, self-consumed** — the same model writes and reads the memory; mechanism 7 mitigates but does not cure this

---

## 8. Gaps (Not Implemented)

| Gap | Impact |
|---|---|
| **The episode layer is currently empty** | The 13 existing entries are facts — no turning points, no quotes. Episodes only start accumulating from 2026-10-28 |
| **No semantic retrieval** | The inherent ceiling of literal keyword matching |
| **No forgetting mechanism** | No time decay (the Ebbinghaus curve is unimplemented); only tiers and budgets |
| **No unified cross-domain memory** | Only DMs and the bot's own viewing reports; desktop chat and comment interactions are not wired in |
| **No conflict detection** | Contradictory facts are not flagged; only manual `replaces` corrections |
| **No "what does it see right now" snapshot** | Debugging the injection requires a simulated script |
| **No background consolidation ("dream")** | Compaction is threshold- or manually triggered; nothing runs while idle |
| **Single machine, single file** | No replication or sync (only a full backup before compaction) |

---

## 9. Theoretical Grounding

| Source | What was borrowed |
|---|---|
| Rate–distortion survey (2026, *What to Keep, What to Forget*) | **Reversibility matters more than any scoring trick**; multi-fidelity layering (a small high-fidelity tier plus a large lossy one) |
| MemGPT | Paging between main context and external storage; editable core memory |
| Generative Agents | Separating relevance × recency × importance; reflections must carry evidence links |
| A-MEM | Dynamic links between memories; new experiences reorganise old ones |
| Ebbinghaus | Forgetting curve (**not implemented**) |

**To be explicit**: adopting a three-layer structure ≠ reproducing human memory. Forgetting, reconstruction and emotional weighting are not implemented here. It is an engineering approximation that works over the long run.

---

## 10. Operational Checks (Three)

```
① Is facts.md still "one short line per entry, ≤200 Chinese characters"?
   → If it starts writing essays again, the prompt has lost its grip
② Does state.json contain accumulating pending / needs_review tasks?
   → If so, memory is stuck; stop letting it run
③ Does the history row count equal the number of received messages?
   → If not, archiving is dropping data (the most serious case)
```

---

## 11. Relationship to Continual Learning (Important)

This system is **external memory**. It is a stand-in for **internal plasticity** (actually changing the weights or structure).

| | External memory (this system) | Internal plasticity (biological) |
|---|---|---|
| Substrate | Text files | Synaptic weights |
| How it takes effect | Injected into context each round | The structure itself changes |
| Continuity across turns | ✅ Yes (narrative) | ✅ Yes (causal) |
| Growth in capability | ❌ No (the model itself is unchanged) | ✅ Yes |
| Recovery from failure | ✅ Yes, if the files survive | ❌ Damage is irreversible |

**Conclusion**:

> It imitates the **function** of memory, not its **mechanism**.
> It lets her *remember*, but not *become better*.

Given that continual learning remains unsolved in current AI, this is a **pragmatic but limited substitute** — it routes around internal plasticity with external structure.

See the companion document: *How Does Will Emerge?*, Chapter 6.

---

## Appendix: Key Numbers (measured 2026-10-28)

```
L1 portrait     209 bytes (limit 5210)
L2 facts        13 entries (episodes: 0)
L3 raw history  190 rows, all IDs unique
                  59 platform-issued IDs + 131 local-<sha1> IDs
Task records    40
Per-round injection  ~5 KB (L1 + L2 cards + last 20 messages + L3 hits)
```
