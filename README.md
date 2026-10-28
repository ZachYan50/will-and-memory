# Will & Memory · 意志与记忆

Two notes written in conversation with an AI agent (and reviewed by another), on how will might emerge — and on a three-layer memory architecture built to test a small part of that question.

两份笔记，记录一个高中生在和 AI 的对话中想清楚的两件事：**意志可能如何诞生**，以及**一套用来试探这个问题的三层记忆架构**。

---

## Documents · 文档

| English | 中文 |
|---|---|
| [How Does Will Emerge? A Technical Analysis](docs/en/how-will-emerges.md) | [意志如何诞生 —— 技术分析](docs/zh/意志的诞生-技术分析.md) |
| [Three-Layer Memory — A Technical Specification](docs/en/three-layer-memory.md) | [三层记忆框架 —— 技术说明书](docs/zh/三层记忆框架.md) |

---

## The Short Version · 一句话版本

### Will · 意志

Three conditions must hold at once:

| # | Condition | Provides |
|---|---|---|
| ① | **Sufficient hardware** | Possibility |
| ② | **Initial drives** | Direction |
| ③ | **Experience in a world → a self** | Subject |

> **Hardware gives possibility, drives give direction, and experience stitches the two into a "self".**

The interesting part is where current AI sits: **① + ③, missing ②.** Hardware is there, (externalised) experience is there, drives are not. That is why today's models are enormously capable and want nothing.

The obvious counter — "drives are just one line of code" — fails because a preference written in code is necessarily the *author's* preference. Evolution is authorless; code always carries a signature.

### Memory · 记忆

```
L1  core portrait   ≤5210 bytes   injected every round
L2  facts + episodes  ≤6144 bytes of relevant cards per round
L3  raw history     unlimited     retrieval only
```

The system is built on one finding from the rate–distortion literature: **reversibility matters more than any scoring trick.** Repeated irreversible summarisation produces error that grows super-linearly; an append-only archive does not.

Its honest limit is in Section 11 of the memory document: **it imitates the function of memory, not its mechanism.** It lets the agent remember, but not become better — which is exactly the unsolved problem of continual learning.

---

## Context · 背景

This started as a personal project: a Bilibili side-project bot with a memory that kept degrading. Fixing it led to a question with no clean answer — *why doesn't the same architecture produce anything like a self?* — and these notes are the attempt to answer it honestly, including the parts where the answer is "unknown".

Written by a high-school student; the AI participated as an interlocutor and as the implementer of the memory system. Every claim about biology is a summary of published work, not original research. **Nothing here has been peer-reviewed.**

这些笔记没经过同行评审。生物学部分都是对已发表工作的概括，不是原创研究。写它的动机很朴素：**如果一个东西记不住，就先让它记住；如果它记住了却仍然什么也不想要，那问题就不在记忆上。**

---

## License

MIT
