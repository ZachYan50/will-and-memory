# 意志与记忆 · Will & Memory

这里收录两篇独立的文章：一篇讨论自我意识与意志如何形成，另一篇介绍用于 AI 对话的三层记忆设计。可以按兴趣分别阅读。

## 文章目录

| 文章 | 内容 | English |
|---|---|---|
| [自我意识如何形成：关于三个条件的推测](docs/zh/意志的诞生-技术分析.md) | 从人类成长理解身体、需求与经历如何参与自我的形成，再讨论意志以及对 AI 的启发 | [How Self-Awareness Develops](docs/en/how-will-emerges.md) |
| [三层记忆：设计、实现与边界](docs/zh/三层记忆框架.md) | 介绍私人 B 站插件中的记忆设计，包括信息如何保存、检索、更新，以及目前的限制 | [Three-Layer Memory](docs/en/three-layer-memory.md) |

## 自我意识与意志

这篇文章提出一个推测：**自我意识的形成，需要硬件基础、驱力和在世界中的经历共同参与。**

推测的依据来自人类成长：婴儿具有感知与学习的身体基础，生理需求促使其寻求满足、回避不适；随着身体发育和互动经历的积累，儿童逐渐表现出更明确的自我认识。

文章沿着这个成长过程，继续讨论人怎样形成自己的目标、作出取舍，以及人工系统能从中借鉴什么。

## 三层记忆设计

这篇文章回答一个实际问题：**怎样让 AI 在长期对话中记住重要的事，同时能够回查细节？**

- **第一层：随时记着的核心信息。** 例如对方明确说过的长期偏好。
- **第二层：值得回想的事实和经历。** 除了结论，也可以保留发生的原因、当时的想法和后来的变化。
- **第三层：可回查的原始记录。** 摘要不够时，寻找实际保存的消息或观看报告。

每轮对话只取相关的一部分内容。旧事被再次提起，可以补充已有记忆；仅仅被系统搜索到，不会因此自动变得更重要。

这套设计已经用于作者的私人插件。文档介绍当前实现，以及存储、检索和更新时需要注意的问题。

## 作者、资料与版本

这些文章由一名高中生发起，在与 AI 的讨论中逐步整理。DeepSeek 参与原始讨论和记忆系统实现；Codex 协助代码核对与文档修订。

文档初稿：**2026-10-28**；本次修订：**2026-10-29**。中文和英文内容同步，旧版保留在 Git 提交历史中。

本仓库发布文章，完整插件源码与私人对话未公开。记忆文章中的实现细节以注明日期的本地版本为准，研究资料在各篇文中列出。

## English

This repository contains two independent essays. You can read either according to your interests.

- [How Self-Awareness Develops](docs/en/how-will-emerges.md) proposes three conditions: a physical foundation, drives and experience in the world. It draws on human development to explore how people come to understand themselves, form goals and make choices, then considers what artificial systems might learn from that process.
- [Three-Layer Memory](docs/en/three-layer-memory.md) describes a memory design used in a private Bilibili plugin: a small core portrait, retrievable facts and episodes, and archived records. It explains storage, retrieval, updates and practical limits.

The essays were initiated by a high-school student through discussions with AI. DeepSeek contributed to the original discussions and memory implementation; Codex assisted with code checks and document editing. Both languages were revised on **2026-10-29**. The full plugin and private conversations are not published here. Implementation details refer to the dated local version, and research sources are linked in each essay.

## License

[MIT](LICENSE)
