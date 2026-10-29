# 意志与记忆 · Will & Memory

这个项目从一个实际问题出发：**一个能聊天、能看视频的 AI，怎样才能记住共同经历，而不是每次都从头认识你？**

修补记忆的过程中，又出现了一个更难的问题：如果它能长期记住、形成偏好，并根据经历改变选择，这离我们所说的“意志”还有多远？

这里记录两件相关但不同的工作：一套已经用于私人 B 站插件的记忆设计，以及一份关于意志的讨论。**前者可以检查实现和效果；后者仍是待检验的想法。记忆系统的运行，不等于意志或意识已经诞生。**

## 从哪里读起

| 你关心的问题 | 中文 | English |
|---|---|---|
| 这套记忆到底怎么工作？ | [三层记忆：设计、实现与边界](docs/zh/三层记忆框架.md) | [Three-Layer Memory](docs/en/three-layer-memory.md) |
| 为什么从硬件、驱力和经历推测自我的形成？ | [意识、自我与意志：三个条件的推测](docs/zh/意志的诞生-技术分析.md) | [Consciousness, Self and Will](docs/en/how-will-emerges.md) |

建议先读记忆，再读意志。两篇都先讲问题和例子，再讲依据与限制，不需要先掌握机器学习术语。

## 三层记忆，先用日常语言解释

- **第一层：随时记着的核心信息。** 例如对方明确说过的长期偏好。
- **第二层：值得回想的事实和经历。** 不只记一句结论，也可以保留为什么发生、双方怎么想、后来哪里变了。
- **第三层：可回查的原始记录。** 摘要不够时，再去找当时实际保存的消息或观看报告。

每次对话只取相关的一小部分。旧事被再次提起，可以补充已有记忆；仅仅被系统搜索到，不会因此自动变得更重要。

这里的目标是**让长期保存的信息不必全部塞进一次对话**。它不承诺无限磁盘、永不漏检，也不声称复现了人脑。

## 关于意识与自我，先提出三个推测条件

我们的推测是：较明确的“自我”逐渐形成，需要**硬件基础、驱力、在世界中的经历**共同参与。文章先说明这三个条件，再从人类发育解释推测的来历：婴儿具备身体与神经系统基础，生理需求为反馈提供初始方向，成长与互动逐步带来更明确的自我识别。

约1.5–2岁的镜像自我识别是其中一条发育线索，不是意识在那时突然出现的证明。三者的必要性与充分性尚未确立；AI 的训练目标、行为偏好和主观体验也仍需区分。

## 资料与版本

项目由一名高中生发起，在与 AI 的对话和实现过程中逐步形成。DeepSeek 参与原始讨论与实现；Codex 协助代码核对和本次文档修订。AI 参与写作不代替事实核查。

文档初稿：**2026-10-28**；本次修订：**2026-10-29**。两种语言同步调整了结构、论证范围和引用。原稿仍保留在 Git 提交历史中。

本仓库发布的是说明文档，不包含完整插件源码、私人对话或可复现的完整实验材料。实现细节以文档标明日期的本地版本为范围；引用论文也不意味着本项目已经复现其结果。**本文档未经过同行评审。**

## English

This project began with a practical question: **how can an AI that chats and watches videos remember shared experiences instead of starting over each time?**

It led to a second question: if a system remembers, develops preferences and changes its choices through experience, how close is that to what we call “will”?

The repository separates a working memory design from a hypothesis about self-awareness and will: a physical foundation, drives and experience in the world working together. The discussion now begins with those three conditions and uses infant development to explain the hypothesis. Mirror self-recognition around 18–24 months is a milestone, not an established onset of consciousness. Read [the memory design](docs/en/three-layer-memory.md) for the concrete system, then [the discussion of will](docs/en/how-will-emerges.md) for the broader question. A functioning memory system is not evidence that consciousness has emerged.

The three layers are a small core portrait, retrievable facts and episodes, and archived records. Storage, retrieval and interpretation still have limits. This repository contains documentation, not the full plugin or private conversations. The notes were revised in both languages on **2026-10-29** and have not been peer-reviewed.

## License

[MIT](LICENSE)
