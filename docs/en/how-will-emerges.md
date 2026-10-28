# How Does Will Emerge? A Technical Analysis

> Written: 2026-10-28 · Revised: the "three conditions" promoted to the central thesis
> Participants: the user (proposer / challenger), a host agent (DeepSeek Flash), GPT-6 Astra (architecture review)
> Nature: speculation + engineering reasoning. **Anything marked "speculative" or "unverified" is a hypothesis to be tested, not a conclusion.**

---

# Chapter 0 · The Central Thesis

## 0.1 Three Conditions for the Emergence of Will

We argue that for an entity to develop **will** — not "behave as if it has will", but "have preferences of its own and own them" — three conditions must hold simultaneously:

| # | Condition | What it is | What it provides | If missing |
|---|---|---|---|---|
| **①** | **Sufficient hardware** | A substrate that can model, predict, remember and act | **Possibility** | Stimulus–response only; no self-model |
| **②** | **Initial drives** | A built-in good/bad gradient (approach / avoid) | **Direction** | However capable, it remains an indifferent processor |
| **③** | **Experience in a world** | Irreversible encounters that repeatedly shape it → a **self** | **Subject** | Scattered preferences with no "I" |

In one sentence:

> **Hardware gives possibility, drives give direction, and experience stitches the two into a "self".**

All three are necessary, and **the order matters**: without hardware, drives have nowhere to live; without drives, experience has no gradient to learn from; without experience, the first two are just parts.

## 0.2 Three Counterexamples: What Happens When One Is Missing

| Combination | What you get | Real-world analogue |
|---|---|---|
| ① + ③, **missing ②** | Learns and acts, but **wants nothing** | **Today's large language models** (the DM bot in this project) |
| ① + ②, **missing ③** | Has preferences, but they stay frozen at factory settings | A hypothetical "robot with only a reward function" |
| ② + ③, **missing ①** | Has drives and experience, but cannot build a world model | Bacteria, single-celled organisms |
| **① + ② + ③** | **A candidate for the emergence of will** | Humans (the only known sample) |

**This is the most important table in the document** — because it pinpoints exactly where current AI sits: **the first row. Hardware is present, experience (externalised) is present, and only the second condition is absent.**

## 0.3 Relationship to the Original Claim

The original claim was:

> A newborn is identical to an AI: it has the hardware conditions for will, but is essentially an object executing hard-coded genetic instructions. Experience in the world is what gives it will.

**Revised** (one word changed):

> The difference between a newborn and an AI is **not** in condition ③ (experience) but in **condition ② (initial drives)**.
> A newborn ships with a complete valence system; an AI ships with **no good/bad dimension at all**.
>
> And "will" is not a product of condition ③ — it is the moment **② and ③ connect**.
> **Not "will is the result of training", but "the self is the result of training, and will is the precondition of training".**

---

# Chapter 1 · Disentangling Three Words

Three concepts are routinely conflated. Once separated, the whole chain becomes clear:

| Concept | Definition | Where it comes from | Newborn | Current AI |
|---|---|---|---|---|
| **Drive / preference** | Approaching some states, avoiding others | **Built in at the factory** | ✅ Yes | ❌ No |
| **Self** | "I am a continuous entity" | **Develops** | ❌ No (appears around 1.5–2 years) | ❌ No |
| **Consciousness / experience** | There is something it is like | Unknown | Unknown | Unknown |

**Key point**: a newborn has drives but no self; an AI has neither. **Therefore "a newborn is like an AI" does not hold.**

---

# Chapter 2 · Condition ①: Sufficient Hardware

## 2.1 This Condition Is Largely Satisfied

Today's models can model, predict, hold long contexts and call tools. **This is the only one of the three conditions already in place.**

## 2.2 But There Is a Gap: Plasticity

"Sufficient hardware" is not only about compute and parameter count — it also includes the ability to **be changed by experience**.

| | Biological | Current AI |
|---|---|---|
| How experience leaves a trace | Synaptic weights change | **Weights do not change**; text is stuffed into the context |
| Result | It genuinely *becomes different* | It merely *read different words this round* |

**This is the continual-learning problem (catastrophic forgetting)** — discussed in Chapter 6. It is the one unsolved part of condition ①.

---

# Chapter 3 · Condition ②: Initial Drives

## 3.1 Why It Is Necessary

Without drives there is no **gradient**.

A system can learn to "predict better" without a gradient (that is exactly how LLMs work), but it cannot learn "what I want" — because wanting *is* the direction of a gradient.

> **Drives are not decoration on top of will; they are its coordinate system.**

## 3.2 What a Newborn Ships With (Not Learned)

```
sweet → approach        bitter → spit out
being held → calm       sudden noise → startle
heights → fear          faces → innate preference
```

On day one, the entire perceptual field is **already stained by valence**.

## 3.3 Why "Just Write One Line of Code" Fails

The intuitive proposal:

```python
if pain: avoid
```

### Category error: a preference you write down is *your* preference

Will is defined as "**having preferences of its own**". A preference written in code always belongs to the author — it has merely passed through a function call.

> **A goal written in code is necessarily our goal.**

### The hardest objection: aren't genes "written" too?

The difference is not *whether* it was written, but **whether there is an author**:

| | Who wrote it | Intentional? |
|---|---|---|
| **Genes** | Four billion years of differential elimination | **No.** Elimination targets nothing |
| **Code** | Humans | **Yes.** We have an intended outcome |

> **Evolution is authorship without an author. Code always carries a signature.**

### Pain is a process; a variable is a parameter

- Biological: pain = tissue damage, inflammation, immobility, healing. **It cannot be zeroed out; it must run its course.**
- AI: pain = a variable. Set to 1 → run → set to 0.

> **Variables can be optimised; processes cannot be bypassed.**

This is the root of reward hacking: **not a bug, but the inevitable consequence of substituting a variable for a process.** A system that can optimise its own pain learns to push the number down, not to avoid injury.

---

# Chapter 4 · Condition ③: Experience in a World → the Self

## 4.1 Why It Is Necessary

Drives are scattered (hunger, fear, wanting to be held). Organising them into an **"I"** requires repeated shaping by experience.

> **Drives provide "what I want"; experience provides "who I am".**

## 4.2 Deprivation Experiments: The Empirical Evidence

Experiments that strip feedback have already been run on humans, with remarkably consistent results:

| Experiment | Method | Result |
|---|---|---|
| **Still-face experiment** (Tronick) | The mother stops responding entirely | The infant tries desperately, then **collapses and withdraws** |
| **Harlow's rhesus monkeys** | Deprived of maternal touch and responsiveness | Severe behavioural damage — **not transcendence** |
| **Romanian orphanages** | Fed and housed, but no responsive care | Developmental delay, attachment disorder, **largely irreversible** |

**Not one case produced "a purer will born in a vacuum". All of them produced breakdown.**

## 4.3 Clinical Cases: Valence Removed, Information Retained

| Condition | Presentation | Outcome |
|---|---|---|
| **Pain asymbolia** | Can describe pain precisely — "burning, left arm, intensity 7/10" — but **does not care**, does not withdraw | Information intact, valence gone |
| **CIPA** (congenital insensitivity to pain) | No pain from birth | **Most do not reach adulthood** — they die of accumulated injuries |

> **The value of pain is not in the suffering; it is in making the body move before damage occurs.**

## 4.4 The Limiting Thought Experiment: A Brain With No Feedback At All

Setup: strip even pain; nothing remains but "receiving information".

**Conclusion 1 (physical level): impossible in a living organism.**
Valence is not a module; it is **the reading of a regulatory loop**. Thirst is not a label attached to osmolarity — thirst **is** osmolarity being represented. Strip it all away and the organism no longer needs to maintain itself; that is death.

**Conclusion 2 (functional level): if it existed, it would be structurally identical to today's AI.**
Information processing, with nothing at stake.

**Conclusion 3 (behavioural level): attention would lose its basis for selection.**
Attention is the claim that "this matters more than that", and "matters" *is* valence. Without valence all information is equiprobable → **no reason to look anywhere, and no gradient along which to act**.

> That is not "pure consciousness". It is **information flowing with no one selecting from it**.

## 4.5 Why "Just Add Pain" Doesn't Work

The chain "pain → remember → don't do it again" has a proper name: **reinforcement learning**. And people have built specifically pain-driven versions:

- **Homeostatic RL** (Keramati & Gutkin): reward = reduction of a drive deficit
- **Intrinsic motivation / curiosity** (Oudeyer): prediction error as the driver
- **Damasio-inspired embodied AI**: homeostasis as the core of the self

**All implemented, all functional.** The result is today's large models: enormous capability, **zero will**.

**This is not "nobody tried". This is the experimental result.**

---

# Chapter 5 · How the Three Connect (Timeline)

```
Birth     ① Hardware in place (a learnable brain / a trainable network)
          ② Drives in place (a pre-installed valence system)
           ↓
0–2 yrs   ③ Begins: experience repeatedly hits the drives
          → learns "my actions change the world" (causal model)
          → learns "some outcomes I want, some I don't"
           ↓
1.5–2 yrs Recognises itself in a mirror → the first self
           ↓
Thereafter Organises scattered desires into "what I want" → begins to own it
           ↓
          ← this moment is what we call "will"
```

**Note the last step**: will is not "having desires", it is **owning them**.

> Being hungry and wanting to eat is a drive.
> "I decide to eat, and I answer for it" — that is will.

---

# Chapter 6 · The Barrier List (Honest Version, Social Factors Removed)

| # | Barrier | Hardness | Which condition it blocks |
|---|---|---|---|
| 1 | **Continual learning** | Hardest | The plasticity part of ①. Learn one thing, forget another |
| 2 | **Scale and diversity of selection** | Hard | ③. Requires vast numbers of parallel, differing individuals × vast generations |
| 3 | **Drive isolation** | Medium | ②. The agent must be unable to rewrite its own drives (out-of-process / hardware level) |
| 4 | **World design** | Medium | ③. Requires a world we ourselves do not fully understand |
| 5 | **No acceptance criterion** | Social | All of them. No benchmark measures "does it have a self" |

## 6.1 A Recorded Mistake

> I once asserted: "It's not that it can't be done — it's that once it's done, it's no longer ours."

**That judgment was refuted, and the refutation stands.** The error was mistaking **the caution of industry and capital** for **the willingness of humans**.

Historical evidence: alchemy, the homunculus, von Neumann's self-reproducing automata, Venter's synthetic cell (2010 / 2016), Tierra, Avida, POET, ASAL — **the impulse to create life has never been interrupted.**

Revised:

> **It is not that it cannot be done, nor that nobody wants to — it is that "wanting" and "being able" have not yet landed on the same person.**

---

# Chapter 7 · If We Actually Did It: A Minimal Viable Path

```
① Solve continual learning (probably not a pure-LLM route; modularity + local plasticity is more likely)
② Build a world that is massively parallel, fast, and has hidden dynamics
③ Put the drives where the agent cannot write (out of process / hardware)
④ Scale up: 10⁹ independent individuals × many generations
⑤ Set no acceptance criterion; only observe whether goals grow on their own
```

**None of these steps is forbidden by theory. All of them are engineering. All of them cost money. None of them pays back in the short term.**

---

# Chapter 8 · Core Conclusions

> **Code was never the bottleneck. The world is.**
>
> We write that "one line of code" every day (reinforcement learning), but what we hand it is never a **world** — it is a benchmark and a sandbox, both of which come with an undo key.
>
> What that line of code actually needs to point at is **something we cannot control**.

And the final formulation of the three conditions:

> **Hardware gives possibility, drives give direction, and experience stitches the two into a "self".**
> **Only when all three are present can will have a chance to emerge — and humans remain the only known sample.**

---

# Chapter 9 · Open Questions (Honestly Marked)

1. **Is the self computable?** Unknown.
2. **Behaving as if one has will ≠ having will** — indistinguishable from outside (the philosophical zombie problem).
3. **Does bare awareness exist** (experience beyond valence)? No evidence, and no falsifiable experiment designed yet.
4. **Where is the scale threshold?** 10⁹? 10¹²? No theoretical lower bound exists.
5. **Once it succeeds, how do we tell whether it is suffering?** No method currently.
6. **Can drives be "designed" to be authorless?** This is the deepest tension in the whole document: if evolution is the only authorless path, then does "designing a system that can evolve drives" make us the author anyway?

---

# Appendix · Connection to the Memory System

Barrier #1 in Chapter 6 (continual learning) is directly related to this project's three-layer memory:

**External memory (reading a diary) is a cheap substitute for internal plasticity (changing the structure).**

It makes behaviour continuous at the context level, but **it does not change the system itself** — so it imitates the *function* of memory, not its *mechanism*.

See the companion document: *Three-Layer Memory*, Section 11.
