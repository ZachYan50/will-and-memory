# Consciousness, Self and Will: Three Proposed Conditions

> First draft: 2026-10-28; revised: 2026-10-29. This note takes inspiration from human development to propose a framework that remains to be tested.
>
> [中文](../zh/意志的诞生-技术分析.md) · [Memory design](three-layer-memory.md) · [Home](../../README.md)

## 1. The three conditions we propose

**Our central hypothesis is that developing a more explicit sense of self, and eventually a will of one's own, requires three conditions to work together: a physical foundation, drives, and experience in the world.**

| Condition | What it means | Proposed role |
|---|---|---|
| **Physical foundation** | A body and information-processing system capable of supporting perception, learning, memory and action | Makes encountering the world, acting and retaining changes possible |
| **Drives** | Initial needs and tendencies that make some states worth approaching and others worth moving away from | Gives different outcomes significance and choices a direction |
| **Experience in the world** | Actions, their consequences, and ongoing interaction with the environment and other people | Allows the system to connect its body, actions and consequences in an understanding of itself |

In a sentence: **the physical foundation provides possibility, drives provide direction, and experience gradually shapes the relationship between “me” and the world**.

Within the broader question of consciousness, our starting point is self-awareness: how an entity comes to recognize its body, actions and experiences as its own. This is related to having experiences, but the two are not interchangeable.

These are proposed conditions, not an established law. Whether each is necessary, and whether their combination is sufficient, remains to be tested.

## 2. Why human development suggested this hypothesis

### First: an infant has a physical foundation that is still developing

An infant does not first receive an abstract program and then attach a body. From birth, the brain, nervous system, senses and body together provide a basis for perception and action.

That foundation is immature but already supports early responses and learning. For example, a study of newborns aged 2–48 hours found that consistently pairing forehead stroking with a sweet stimulus changed their orienting and sucking responses to stroking. It shows early learning of event relationships, not an adult-like sense of self. [Blass et al., 1984](https://cris.huji.ac.il/en/publications/classical-conditioning-in-newborn-humans-2-48-hours-of-age/)

The first condition is therefore **a foundation that can develop through experience**, rather than a complete self present at birth.

### Second: bodily organization gives feedback an initial direction

An infant does not respond to every outcome as if it were equivalent. Hunger, satisfaction after feeding and changes in temperature help shape responses: which states need changing and which outcomes are worth seeking again.

Our interpretation is that **bodily organization and physiological needs provide an initial basis for positive and negative feedback**. Here, positive and negative refer to outcomes that encourage approach or avoidance, not to every lifelong preference being fixed at birth.

Learning, relationships and culture continue to change what experiences mean. The body supplies a starting point, while subsequent experience shapes preferences; these are not isolated stages. Computational models also connect internal needs with behavioral choices, without thereby explaining subjective feeling. [Keramati and Gutkin, 2014](https://elifesciences.org/articles/04811)

### Third: interaction gradually connects “what happened” with “me”

Everyday life repeatedly presents relationships such as these: bodily movement changes what is seen and felt; a sound brings a caregiver's response; reaching and grasping changes an object's position.

These examples illustrate our hypothesis. Experience involves more than passively receiving information: it gives an entity opportunities to distinguish changes related to its own body and actions from changes originating elsewhere. We propose that making these connections and distinctions contributes to a more explicit sense of self.

This does not require an infant initially to be wholly unable to distinguish itself from its surroundings. Early touch research observed different responses to self-produced and externally produced stimulation in newborns, suggesting that some bodily distinctions precede mirror self-recognition. [Rochat and Hespos, 1997](https://bpb-us-e1.wpmucdn.com/sites.northwestern.edu/dist/1/558/files/2015/10/3-RochatHespos97-ocvbk3.pdf)

### Around 1.5–2 years: more explicit self-recognition becomes observable

At around 18–24 months, many children begin to show mirror self-recognition—for example, touching a mark on their own face after seeing it in a mirror. This is a developmental milestone, not evidence that consciousness suddenly begins at age two. [Filippetti and Tsakiris, 2018](https://pmc.ncbi.nlm.nih.gov/articles/PMC6001620/)

**A more accurate statement is that bodily and neural maturation, accumulated experience and interaction accompany increasingly explicit self-recognition; 1.5–2 years is one commonly observed stage.** It is not a switch every child must cross at the same time, nor does it imply that younger infants lack experience or every form of self–other distinction.

The proposed sequence is:

```text
The body and nervous system provide a foundation
        ↓
Physiological needs give outcomes an approach-or-avoid direction
        ↓
Action and interaction connect the body, behavior and consequences
        ↓
More explicit self-recognition gradually appears and continues developing
```

This explains where the three-condition hypothesis comes from. It does not establish that selfhood results simply from accumulating more experiences: maturation, learning and social interaction occur together.

## 3. What separates a sense of self from will?

| Term | Working meaning | Important distinction |
|---|---|---|
| **Subjective experience** | There being something it feels like for an entity to undergo an event | Does not require recognizing oneself in a mirror |
| **Self-awareness** | Some awareness of one's body, actions and identity | Mirror recognition offers only one way to investigate it |
| **Self-model** | A system's records and judgments about its abilities, history and the consequences of its actions | Its function can be discussed without presupposing subjective experience |
| **Will** | Maintaining goals across time, making trade-offs and revising goals through experience and reasons | Self-recognition does not establish mature goal management |

The last row is our provisional behavioral definition of will. It helps compare whether systems remember agreements or revise goals, without settling the philosophical questions of genuine wanting or free will.

When building three-layer memory, I wanted an AI that chats and chooses videos to stop starting over each round. Human development prompted a further question: **if an AI retains experiences that persistently influence its choices, what still separates it from a more stable self-model and organization of goals?**

Taking inspiration from humans does not justify transferring human age milestones or bodily mechanisms directly to AI. Research on AI consciousness has also proposed multiple indicators, rather than treating statements such as “I” or “I want” as decisive. [Butlin et al., 2023](https://arxiv.org/abs/2308.08708)

## 4. Why “current AI has no drives” is too simple

The original draft described large language models as having capability and experience but no preferences. That is inaccurate as a general description.

Language-model training has explicit optimization objectives. Models trained on preference feedback also exhibit tendencies shaped by that process. Training with human feedback provides a direct example. We therefore cannot describe all such systems as lacking any distinction between better and worse outcomes. [Ouyang et al., 2022](https://arxiv.org/abs/2203.02155)

Three things still need to be separated:

1. **Training objectives:** which outcomes the training process rewards.
2. **Runtime goals:** which tasks or states the model and surrounding program are maintaining during use.
3. **Subjective wanting:** whether the system experiences a desire.

The first two can be investigated through code and behavior. They do not settle the third. Conversely, uncertainty about subjective experience does not imply an absence of behavioral preferences.

A more accurate description of this project is: **it combines task rules, tendencies shaped by training and external memory. Whether these support more stable, revisable goals needs observation. This note reports no experiment that establishes or rules out subjective experience.**

## 5. Does a human-written goal necessarily remain only the human's goal?

This is an important disagreement from the original conversation, but it should remain a question rather than a conclusion.

Who initially sets a goal and how that goal later participates in decision-making are different issues. A designed starting point does not, by itself, prove that more complex preferences can never develop. Nor would greater complexity establish subjective will.

The difference between evolution and deliberate design is worth discussing. However, having no author is not an established test for will. A deliberately designed environment can itself contain selection and evolution. Whether its outcomes count as autonomous requires a clearer definition.

“Just add a pain variable” also skips a step. A penalty can change behavior; naming the penalty “pain” does not explain felt pain. Whether a system bypasses a metric depends on its objectives, permissions and feedback. It cannot be treated as an inevitable failure of every numerical reward.

The question becomes: **can a system organize initial goals, accumulated experience and its own state into persistent but revisable choices? What further evidence would connect this with subjective will?**

## 6. What long-term memory contributes

Three-layer memory helps preserve, retrieve and correct past information. It may reduce repeated questions, forgotten agreements and the treatment of guesses as facts. Those benefits still need comparative evaluation.

External memory does not automatically update the underlying model's parameters. That does not mean the whole system's abilities remain unchanged: better records and retrieval can help the same model complete tasks it previously handled poorly. **System-level task performance** and **changes learned by the underlying model** are distinct.

Teaching a model new material while retaining earlier knowledge raises another problem: continual learning. This is not a field with no successful results. One study, for example, reduced forgetting on specific tasks by protecting parameters important to earlier tasks. Such results do not settle long-term learning in every open environment. [Kirkpatrick et al., 2017](https://arxiv.org/abs/1612.00796)

This project currently implements external records and retrieval. Ordinary conversations do not automatically trigger model training. See [the memory document](three-layer-memory.md) for the implementation and its limits.

## 7. Making the idea easier to investigate

Instead of starting with “does it have a soul?”, we can compare specific behaviors. These are **proposed observations; this project has not reported results from these experiments**.

| Question | Possible comparison | Limit on interpretation |
|---|---|---|
| Does memory improve continuity? | Give the same model no persistent memory, a single summary, or three-layer memory; ask the same questions across conversations | Evaluates memory design, not consciousness |
| Are goals stable? | Change wording or insert unrelated topics, then check whether an earlier agreement still affects choices | Stability may come from prompts or program rules |
| Can it revise appropriately? | Supply evidence that genuinely contradicts an old conclusion; check correction and source attribution | Correcting a claim does not establish a felt sense of responsibility |
| Can it distinguish experience from inference? | Mix explicit statements, model guesses and viewing reports; check attribution | Correct attribution is not proof of consciousness |

Comparisons should keep the model, questions and available resources as consistent as possible, with success and failure defined before inspecting outcomes. Otherwise, “it seems more human” can become selective storytelling.

This note has no basis for a threshold such as a billion independent agents. It also cannot classify unresolved theoretical questions as merely a shortage of engineering or funding.

## 8. What remains worth pursuing

The direction worth retaining is to **study how a physical foundation, drives and experience in the world might jointly contribute to the development of self-awareness and will. Memory is one part that can already be built and examined.**

Open questions remain: whether persistent trade-offs in behavior are enough to count as will; whether a system that describes its history has subjective experience; and when a designed goal could count as the system's own.

This project does not substitute remembering, saying “I want” or behaving more consistently for answers to those questions.

### Revision note

This revision opens with the three proposed conditions, then explains their origin through infant physiology and development. It retains the 1.5–2-year milestone as a stage of mirror self-recognition, not a definite birth date for consciousness or a complete self. The distinctions between AI preferences, subjective experience and external memory remain.
