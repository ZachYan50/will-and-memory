# Three-Layer AI Memory: Remember What Matters and Retrieve the Details

> First draft: 2026-10-28; revised: 2026-11-01.
>
> [中文原文](../zh/三层记忆框架.md) · [Home](../../README.md)

## 1. A memory framework for AI applications

In long conversations and ongoing tasks, AI needs access to earlier agreements, preferences and experiences. Providing only recent material can leave those events out of its next decision. Including the entire history increases input length, processing time and cost.

The three-layer approach is to **preserve experience over time and retrieve what is needed for the current interaction, using summaries for orientation and original records for details.**

Memory has three layers: readily available core information, retrievable facts and episodes, and archived source records. Each has a distinct responsibility, and source references connect them.

The design can be used with different models and applications, including conversational assistants, personal assistants, learning companions and agents that carry out ongoing tasks. The application supplies storage, retrieval and tools. The model interprets material, decides what is worth remembering and revises its understanding when new evidence appears.

## 2. One conversation illustrates the three layers

Suppose someone says, “I like walking on rainy nights. The quiet is enough.” Days later, they explain, “Last time, it wasn't because I liked being alone. I was feeling very sad that day.”

If the system remembers only “this person likes solitude,” it has treated an interpretation as a fact. The layers can work together as follows:

| Layer | What it preserves | How it is used |
|---|---|---|
| **L1: core information** | Explicit, lasting preferences; uncertain personality judgments stay out | Provided directly each round |
| **L2: facts and episodes** | The preference for rainy-night walks, plus the conversation's context, exact words and later correction | Find relevant summaries, then expand the episode |
| **L3: source records** | The saved messages from both conversations | Check what was actually said |

The key is to **preserve both an understanding of an event and the evidence that allows that understanding to be corrected.**

## 3. What each layer does

### L1: readily available core information

L1 is a small collection of information available each round: explicit long-term preferences, important agreements or the assistant's ongoing responsibilities. It provides essential background when a new conversation round or task begins.

Keep L1 brief and stable. Update it when clear new evidence appears; a passing emotion or a single silence should not become a lasting personality judgment. Label inferences separately, and preserve other valid information when changing one item.

### L2: retrievable facts and episodes

L2 holds two kinds of record:

- **Fact entries:** concise conclusions with a date, sources and a fact-or-inference label, such as an explicitly stated preference or an agreement.
- **Episode entries:** events worth recalling, preserving their topic, summary, context, key quotations, turning points and interpretation at the time. Examples include an extended conversation, a shared task or the clarification of an important misunderstanding.

Facts provide quick answers; episodes preserve how those answers developed. An episode can be supplemented while retaining earlier versions. When a conclusion proves wrong, record the replacement and its correction link so future answers use the updated understanding.

Retrieval initially supplies short cards containing a title, summary, date and sources. Full details can be opened when needed.

### L3: source records for checking details

L3 preserves records actually received or produced, such as conversation messages, task inputs and tool results. New material is appended and existing records retained, allowing the system to check details omitted from summaries and the basis of an interpretation.

For images, audio and video, memory can store source identifiers, descriptions or transcripts, while the application manages media files separately. AI-generated reports should identify their author and sources, distinguishing the model's interpretation at the time from external events.

The value of L3 is that **material left out of today's summary can still be found later.**

## 4. How a conversation round or task uses memory

1. **Archive first.** Save the current messages or task records, assign stable source identifiers and deduplicate retries using those identifiers.
2. **Prepare context.** Supply L1, recent conversation or task progress, and L2 cards relevant to the current question.
3. **Recall details as needed.** Expand relevant episodes. When summaries are insufficient or retrieval finds nothing useful, search L3, try other keywords or look up a date.
4. **Complete the current action.** Use the material to answer or carry out the task.
5. **Update memory.** Add facts, supplement episodes or correct earlier interpretations using the new information. Leave memory as it is when there is nothing worth adding.

Track action outcomes and memory updates separately. If a reply was sent successfully but saving memory failed, retry the memory update without sending the reply again.

Each retrieval has a budget. That budget controls how much information enters the current context, while stored entries can continue to accumulate. The application sets byte limits, recent-message counts and card counts according to model capacity, cost and response time.

## 5. What is worth remembering, and in how much detail?

The framework treats three questions separately.

**Importance: will this be worth recalling later?** Consider explicit requests to remember, commitments, changes in views or relationships, and explicitly expressed emotions. Record the reasoning behind the judgment.

**Retention depth: how much of the event should remain available?** An ordinary fact may need a brief entry; an important episode may need more context, quotations and turning points. Two equally important events may require different amounts of detail.

**Current relevance: what should be read first now?** An important past event may be irrelevant to the current question, while an ordinary fact may contain exactly the answer needed.

A two-hundred-message exchange is therefore not automatically more important than a twenty-message one. Length may help determine how much detail to preserve, while importance depends on the substance and what changed.

Being retrieved does not make a memory more important. Update an existing memory when new conversation revisits it, adds details or changes its interpretation.

## 6. Keeping memory open to correction

Preserve clear source relationships between the layers:

- Link facts and episodes to specific source records, and verify direct quotations against those sources.
- Distinguish a person's own words, an AI summary and an AI inference.
- Use the latest conclusion while retaining correction records and earlier versions.
- When consolidating duplicate entries, merge only the selected material and retain its sources and unrelated memories.
- Keep users, projects and task spaces separate, allowing references across spaces according to application permissions.

Writes also need to handle duplicate submissions, concurrent changes and interruptions. Stable identifiers, version checks, atomic saves and recovery records let the application distinguish completed updates, retries and changes that require reading the latest version first.

These mechanisms make memory inspectable, traceable and correctable, preserving the evidence behind its summaries.

## 7. Connecting different AI applications

The framework defines memory responsibilities and a usage flow. An application needs a few basic capabilities:

| Capability | Responsibility |
|---|---|
| Archive | Preserve original inputs, outputs and source identifiers |
| Read and update core information | Supply and maintain L1 |
| Search | Find L2 and L3 material by current question, keyword or date |
| Expand | Read full episodes, source records and earlier versions |
| Commit and correct | Save entries, update episodes and link corrections |

These capabilities can be exposed through function calls, tools or the application's own control flow. Storage can begin with local files or use a database. Retrieval can use keywords, semantic search or both. These underlying choices can change while the layer responsibilities and source relationships remain clear.

For a concrete application, start by checking a few practical cases: remembering an explicit agreement, finding an old episode, incorporating a correction, and retrying without duplicate records or actions. Then adjust budgets, retrieval and retention depth through use.

Storage still consumes disk space and maintenance effort, and retrieval can miss relevant material. The aim is to accumulate and use long-term records as needed, rather than include the full history in every interaction.

## 8. Design references

Several research directions share ideas with this framework:

| Work | Related idea |
|---|---|
| [MemGPT, 2023](https://arxiv.org/abs/2310.08560) | Move information as needed between limited current context and external storage |
| [Generative Agents, 2023](https://arxiv.org/abs/2304.03442) | Retrieve experiences using relevance, recency and importance, and form higher-level reflections |
| [A-MEM, 2025](https://arxiv.org/abs/2502.12110) | Let new information affect the organization and interpretation of existing memories |
| [Colaco and Lahjouji, 2026, preprint](https://arxiv.org/abs/2607.08032) | Study what to retain under a limited budget and the information lost through compression |

These works provide design references. The three-layer division is: **keep core information readily available, recall important episodes as needed, and preserve source records for checking details.**
