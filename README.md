# 意志与记忆 · Will & Memory

两份笔记，记录一个高中生在和 AI 的对话中想清楚的两件事：**意志可能如何诞生**，以及**一套用来试探这个问题的三层记忆架构**。

> 两份文档都有中英双语。中文链接在前面。

---

## 文档

| 中文 | English |
|---|---|
| [**意志如何诞生 —— 技术分析**](docs/zh/意志的诞生-技术分析.md) | [How Does Will Emerge?](docs/en/how-will-emerges.md) |
| [**三层记忆框架 —— 技术说明书**](docs/zh/三层记忆框架.md) | [Three-Layer Memory](docs/en/three-layer-memory.md) |

---

## 一句话版本

### 意志

要长出意志，三个条件必须同时成立：

| # | 条件 | 提供什么 |
|---|---|---|
| ① | **能力足够的硬件** | 可能性 |
| ② | **初始驱力** | 方向 |
| ③ | **在世界中的经历 → 自我** | 主体 |

> **硬件给可能性，驱力给方向，经历把这两样缝成一个「我」。**

最有意思的是当前 AI 的位置：**① + ③，缺②**。硬件有了，（外置的）经历也有了，驱力没有。所以今天的模型能力惊人，却什么也不想要。

那个显然的反驳——"驱力不就是一行代码吗"——不成立，因为**写在代码里的偏好，必然是作者的偏好**。演化是无作者的写作；代码永远留着一个签名。

### 记忆

```
L1  核心画像     ≤5210 字节    每轮注入
L2  事实 + 经历  每轮注入 ≤6144 字节的相关卡片
L3  原始历史     无限          只检索
```

这套系统建立在率失真文献的一个结论上：**可逆性比任何打分技巧都重要**。反复的不可逆摘要，误差会超线性增长；只追加的存档不会。

它诚实的局限写在记忆文档第 11 节：**它模仿的是记忆的功能，不是记忆的机制。** 它能让 agent 记住，但不能让它变得更会——而那正是持续学习这个未解问题。

---

## 背景

这原本是个私人项目：一个 B 站私信 bot，它的记忆一直在退化。修它的过程里冒出一个没有干净答案的问题——*为什么同样的架构生不出任何像"自我"的东西？*——这两份笔记就是尝试诚实地回答它，包括那些答案是"不知道"的部分。

写作者是高中生；AI 作为对话者参与，并负责记忆系统的实现。所有关于生物学的陈述都是对已发表工作的概括，不是原创研究。**这里的东西没有经过同行评审。**

动机很朴素：**如果一个东西记不住，就先让它记住；如果它记住了却仍然什么也不想要，那问题就不在记忆上。**

---

## English

Two notes written in conversation with an AI agent (and reviewed by another), on how will might emerge — and on a three-layer memory architecture built to test a small part of that question.

- [How Does Will Emerge? A Technical Analysis](docs/en/how-will-emerges.md)
- [Three-Layer Memory — A Technical Specification](docs/en/three-layer-memory.md)

**Nothing here has been peer-reviewed.** The biology is a summary of published work, not original research.

---

## License

MIT
