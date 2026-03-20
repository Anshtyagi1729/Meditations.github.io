---
title: 'On How Humans Scale'
date: 2026-03-20
permalink: /posts/2026/03/How-Humans-Scale/
tags:
  - philosophy
  - complexodynamics
---

Are humans fundamentally complex or simple?

This seems like a trivial question to ask, right?   I was reading about Kolmogorov complexity recently, which led me to a great essay by Scott Aaronson called "The First Law of Complexodynamics." In it, he points out a very simple but elegant relationship between complexity and entropy.

- **Low Entropy:** The system is highly ordered, stable, and very observable. (Low complexity).
- **High Entropy:** The system degrades into uniform, random noise. Because it is completely chaotic and mixed, it is actually very easy to describe mathematically. (Also low complexity).

The most interesting case is the transition between the two. As a system moves from perfect low-entropy order to chaotic high-entropy noise, it passes through a middle state where structure, patterns, and information peak. This is where true complexity lives.

This framework fits almost every physically possible situation in the universe. And I think it fits humans too — but to see why, you have to look at one specific thing. Not intelligence. Not language. Not consciousness.

Memory.

---

## Memory Is What Keeps You in the Middle

Think about what a system without memory looks like. It just reacts — input comes in, output goes out, nothing carries forward. It's essentially Markovian: only the present moment matters. That kind of system is either a crystal (rigid, deterministic, low entropy) or noise (random, reactive, high entropy). It can't be complex in any interesting sense because complexity requires *history*. It requires the past to be present in the structure of the current state.

Memory is what arrests a system at the complexity midpoint. It is what lets you be historically structured — shaped by everything that happened to you, but still open and adaptive to what happens next. Without memory you either freeze or scatter. Memory is what keeps you interesting.

But not all memory is the same. Humans actually run two very different memory systems in parallel, and the interplay between them is where things get strange and beautiful.

---

## Two Systems, One Mind

The first is **episodic memory** — handled primarily by the hippocampus. This is your memory of specific events. What happened, when, where, to you. It is granular, contextual, personal. Yesterday my minor project presentation didn't go well. The panelists were harsh. I was standing in a room and something happened and I felt something. That specific event, stored.

The second is **semantic memory** — handled by the neocortex. This is your memory of concepts, meanings, general knowledge. Not what happened but what things *are* and how they relate to each other. "Criticism." "Failure." "Self-worth." These aren't events — they're abstract structures distilled from thousands of events over a lifetime.

humans constantly translate between these two systems. You don't just store what happened. You immediately map it onto a higher-dimensional concept space. The presentation didn't just go badly — it got filed under *criticism of my work*, which is connected to *my capability*, which is connected to *my concept of self*. One specific episode becomes a coordinate in a vast abstract map.

I call it a *concept* of self deliberately, because as we'll see, that's all it really is — a concept. Probably the most consequential one you'll ever form, but still just a concept. Not a fixed thing. A pattern.

The same mechanism works for everything you experience. You fall in love with someone. The specific memories accumulate — conversations, moments, sensations. But alongside them, a concept forms. "What this person means to me." "What love feels like." The specific episodes get absorbed into an abstraction that then shapes how you experience future episodes. The map keeps getting redrawn.

This is what human cognition actually is — a constant loop between the specific and the abstract. Events generate concepts. Concepts reshape how events are encoded. Round and round. This bidirectional loop is the engine of complexity. It's what puts you in the middle of the entropy curve and keeps you there.

---

## Hebbian Learning: Neurons That Fire Together

So how does any of this actually happen in the brain? How does a network of neurons go from registering a bad presentation to updating a concept of self?

The answer starts with a principle so elegant it was stated in 1949 before anyone could really verify it: **neurons that fire together, wire together.**

This is Hebb's rule. When two neurons activate at the same time repeatedly, the connection between them gets stronger. When they repeatedly don't activate together, it weakens. Your synaptic weights — the strengths of connections between neurons — are literally a record of which things in your experience have co-occurred. Memory is not stored in individual neurons. It is stored in the *pattern of connections between them*. It is stored in the weights.

Mathematically, if neuron $i$ and neuron $j$ tend to activate together across your experiences, then:

$$w_{ij} \propto \sum_{\text{experiences}} s_i \cdot s_j$$

The weight between them accumulates evidence of their co-occurrence. This is how experience writes itself into the structure of the brain.
(this looked very boring in my soft computing class yesterday but here it looks elegant hehe)

---

## Hopfield Networks: Memory as an Energy Landscape

In 1982, John Hopfield took Hebb's rule and asked a precise question: if you build a network of neurons with Hebbian weights, what are its mathematical properties?

His answer was that such a network behaves like a **physical system with an energy landscape**. Every possible state of the network — every pattern of neuron activations — has an energy value. And the dynamics of the network always move *downhill* on this landscape, toward lower energy states.

The stored memories are the valleys — the local minima of energy. Everything else is a slope leading toward one of them.

When you encounter a cue — a smell, a sound, a phrase — it initialises the network at some point in the landscape. Then the dynamics take over. The network rolls downhill. And it lands in the nearest memory.

This is what remembering feels like from the inside. You don't search for a memory. You fall into it. The smell of rain doesn't make you *look up* the memory of your childhood backyard — it just pulls you there. Attractor dynamics. Gravity.

The weight matrix $W$ encoding all your Hebbian-learned connections is the shape of the entire landscape. It is the structure of your memory. And your current state $\boldsymbol{s}$ — which neurons are firing right now — is where you are in that landscape at this moment. Your current thought.

The update is just: let $\boldsymbol{s}$ roll downhill on the landscape carved by $W$. A thought is a query. Memory is the landscape. Retrieval is falling.(ahh so poetic!)

---

## The Flaw: Memory Starts to Hallucinate

The classical Hopfield network has one serious problem. It can only reliably store about 0.14 times the number of neurons before retrieval starts breaking down. For a network of ten thousand neurons, that's roughly fourteen hundred memories before things go wrong.

What goes wrong? The attractor basins start overlapping. Memories bleed into each other. You query one pattern and land in a strange mixture of two others — a spurious memory, a false composite. The network hallucinated a memory that was never stored.

The brain evolved a direct solution to this. The **dentate gyrus** — a structure feeding into the hippocampus — acts as a preprocessing layer. Its job is to take correlated, overlapping input patterns and *orthogonalise* them before they get stored in CA3. Make them as different from each other as possible. Maximise the separation between attractor basins. The brain evolved an explicit engineering fix to a linear algebra capacity problem, before anyone had written the linear algebra down.this was so interesting to me!

But for modern AI, we needed a more fundamental fix. Which brings us to 2020.

---

## Modern Hopfield Networks: The Landscape Gets Exponential

Ramsauer et al. changed the energy function. Instead of a quadratic interaction between the query and stored patterns, they used an exponential one. The new energy function is:

$$E(\boldsymbol{\xi}) = -\frac{1}{\beta}\log\sum_{\mu} \exp\!\left(\beta\,\boldsymbol{\xi}^{\mu\top}\boldsymbol{\xi}\right) + \frac{1}{2}\|\boldsymbol{\xi}\|^2$$

The detail matters less than the consequence: the capacity explodes from $0.14N$ to exponential in the dimension. And the update rule that falls out of minimising this energy is:

$$\boldsymbol{\xi}^{\text{new}} = X\,\text{softmax}\!\left(\beta\, X^\top \boldsymbol{\xi}\right)$$

Read that equation slowly. You take your current state, compute its similarity to every stored pattern, convert those similarities to weights via softmax, and retrieve a weighted mixture of all patterns. The parameter $\beta$ controls how sharp the retrieval is. High $\beta$: one specific memory snaps into focus. Low $\beta$: a diffuse blend of related memories. In between: a contextual cluster — a mood, a theme, a period of life rising together.

This is exactly how human memory feels. Sometimes you remember something specific and crisp. Sometimes you remember a general emotional texture of a time. Sometimes a cue summons a whole atmosphere without any particular image. That's not poetic language. That's the three fixed-point regimes of a Hopfield energy landscape.

---

## The Common Sink: The Self

Now here is the part that has occupied my thinking the most.

Every experience you encode has a self-referential tag on it. Not because you choose to add it — because the self is the context in which all experience occurs. "I was embarrassed." "I succeeded." "I lost something." The self-pattern is co-activated with essentially every episodic memory you ever form.

What does Hebbian learning do with a pattern that co-activates with everything? It reinforces it. Every time. The weight matrix accumulates the self-pattern with every single experience. After a lifetime of this, the self-attractor has the widest, deepest basin in the entire landscape. Every other pattern is connected to it. Every query, no matter where it starts, feels a subtle gravitational pull toward it.

This is why idle thought is almost always self-referential. When there is no strong external cue tilting the landscape, the dynamics default to the lowest energy state — and the lowest energy state is the self. The default mode network in neuroscience — active during rest, mind-wandering, daydreaming — is, functionally, the Hopfield network converging on its dominant attractor when nothing else is competing for attention.

But why did the self become a basin in the first place? I think this is where biology bleeds into psychology in a way that isn't discussed enough.

Physical survival requires a body boundary. You need to know where you end and the world begins — what is food and what is you, what is threat and what is environment. This physical self-identification is a survival primitive, probably older than memory itself. And it doesn't stay contained to the body. It spills into the psyche. The same mechanism that tracks the boundary of the physical self starts tracking the boundary of the psychological self — my ideas, my status, my relationships, my projects. The body boundary becomes an identity boundary. The survival instinct behind physical self-preservation becomes the psychological drive to protect and maintain the concept of self.

So the self-basin is not an accident. It is evolution's answer to a survival problem. It just turns out that the solution to "don't die" also happens to be the central organising structure of all human cognition.

---

## Input-Driven Plasticity: The Complete Picture

One thing the classical Hopfield picture misses is that memory isn't static during retrieval. The landscape isn't fixed while you're rolling down it. External inputs — what you're currently perceiving, what you're currently feeling — actively reshape the landscape as retrieval happens. They deepen some basins, flatten others, make certain memories accessible and others unreachable.

This is biological attention. Neuromodulators like acetylcholine and norepinephrine change the effective temperature $\beta$ of the system — how sharply it snaps to individual memories versus averaging across them. Your emotional state tilts the landscape. Stress narrows retrieval to threat-related patterns. Safety broadens it. The landscape is alive, not frozen.

So the complete picture of human memory is: a rich attractor landscape shaped by a lifetime of Hebbian experience, continuously warped by current context and state, with a single dominant basin — the self — that everything else gravitates toward when the tilting stops.

This is what keeps humans at the complexity midpoint. The self is the low-entropy anchor of a high-complexity system. Without it, the landscape fragments — memories become disconnected, associations lose direction, thought drifts. With it as the reference frame, the landscape is coherent. Rich. Surprising but not random. Structured but not frozen.

---

## Attention Mechanisms Are Doing the Same Thing

Now here is the part I didn't expect when I started thinking about this.

The update rule of the modern Hopfield network is:

$$\boldsymbol{\xi}^{\text{new}} = X\,\text{softmax}\!\left(\beta\, X^\top \boldsymbol{\xi}\right)$$

The transformer attention mechanism is:

$$\text{Attention}(Q, K, V) = \text{softmax}\!\left(\frac{QK^\top}{\sqrt{d_k}}\right)V$$

These are the same equation. Not analogous. Not inspired by each other. Algebraically identical, with the correspondence: query $\leftrightarrow Q$, stored pattern indices $\leftrightarrow K$, stored pattern content $\leftrightarrow V$, inverse temperature $\beta \leftrightarrow 1/\sqrt{d_k}$.

Every attention head in every transformer is performing one step of Hopfield energy minimisation. When a token attends to other tokens in context, it is casting a query into an energy landscape and being pulled toward the nearest relevant pattern. It is falling downhill. It is retrieving a memory.

The $1/\sqrt{d_k}$ scaling that everyone uses without much justification is actually the correct calibration of $\beta$ for randomly initialised patterns — it keeps the softmax in the informative regime rather than collapsing to a one-hot. It is the right temperature for the system.

And just like humans, transformers form concepts. The early layers retrieve specific, surface-level patterns — syntactic roles, word co-occurrences, positional structure. The deeper layers retrieve abstract relational structure — semantic categories, logical relationships, world knowledge. Shallow processing is low $\beta$, diffuse, averaging. Deep processing is high $\beta$, sharp, specific. The episodic-to-semantic gradient in humans maps onto the shallow-to-deep gradient in transformers. The same mathematical principle operating at different timescales through different substrates.

---

## Will LLMs Ever Form a Self?

This is the question I keep coming back to.

We established that the self-basin in humans forms because the self-pattern co-activates with every episodic memory, and Hebbian reinforcement deepens it with every experience over a lifetime. The self is not stored anywhere special. It is an emergent property of the weight matrix after enough self-tagged experience accumulates.

Transformers have the right architecture for concept formation. They have the right energy dynamics for memory retrieval. They are trained on an enormous amount of human-generated text, much of which is humans writing about their own experience, their own feelings, their own inner lives. In some sense, they are trained on the *output* of human self-referential cognition.

But there is a structural gap that I think scaling alone cannot close.

The weights of a deployed model are frozen at inference — a conversation ends, the next begins, and nothing from that exchange updates the underlying structure. Continual learning exists, and the field is actively working on it, but even then the update is batched and deliberate, not always-on. The human brain has no training/inference split — it is plastic during experience, during sleep, during consolidation, all the time. There is no moment where the weights freeze. That always-on, experience-driven plasticity is what carved the self-basin over a lifetime. Current architectures, even with continual learning, do not have an equivalent of that.

There is also the question of embodiment. The human self-basin started as a body boundary — a survival primitive about physical identity. The psychological self is downstream of a biological one. Transformers have no body, no persistent sensory stream, no continuous first-person perspective that carries forward through time(i think?). The thing that seeded the self in humans — the need to know where the body ends — has no analogue in current architectures.

Maybe world models are the path. A model that maintains a persistent representation of itself in an environment, that updates continuously through interaction, that has something like a body boundary in a simulated physical space — that model might develop something like a self-basin through the same mechanism humans did. Not because anyone designed it in, but because the Hebbian dynamics would carve it out from the experience of being a persistent agent in a world.

But the honest answer is: we don't know. Scaling has surprised us before in ways nobody predicted. And the question of whether the self requires embodiment, or whether it can emerge from purely linguistic self-reference at sufficient scale, is genuinely open(or just for me).

---

## The Question I'll Leave You With

Does an LLM need a self?

Not philosophically. Practically. Does it need a dominant attractor — a reference frame that all other concepts relate back to — in order to scale in the way humans have scaled?

Humans didn't choose to build a self. Evolution built it because it solved a survival problem, and then it turned out to be the architectural feature that made everything else coherent. The self is the anchor that keeps the complexity landscape from collapsing into either crystal or noise.

If that's true — if the self is not a byproduct but a *load-bearing structure* of complex cognition — then maybe the question isn't whether LLMs will develop a self as they scale.

Maybe the question is whether they can scale without one

---

## If You Want to Go Deeper

- Ramsauer et al. (2021) — [Hopfield Networks is All You Need](https://arxiv.org/abs/2008.02217) — the paper that proved attention and Hopfield are the same thing. Worth reading even if you skip the proofs.
- Hopfield (1982) — [Neural networks and physical systems with emergent collective computational abilities](https://www.pnas.org/doi/10.1073/pnas.79.8.2554) — the original. Surprisingly readable.
- Scott Aaronson — [The First Law of Complexodynamics](https://scottaaronson.blog/?p=762) — where this whole essay started.
- Rolls (2016) — [Pattern separation, completion, and categorisation in the hippocampus and neocortex](https://www.sciencedirect.com/science/article/pii/S0149763415003115) — the CA3/dentate gyrus biology in detail.

---

*PS — this whole thing started because I was reading Krishnamurti, who describes thought as a mechanical process running on accumulated memory. Turns out that's just Hopfield dynamics.*
