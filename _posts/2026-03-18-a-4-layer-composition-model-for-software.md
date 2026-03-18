---
layout: post
title: "Spec Driven Development: A 4-Layer Composition Model for Software"
date: 2026-03-18
author: Divyendu Singh
---

In the [previous post](/blog/2026/03/15/mapping-mental-models-how-ai-can-redefine-ux-development/), I argued that we ship one mental model to every user — not because we lack the knowledge to do better, but because we could not afford to. That post approached the problem from the user's perspective: how mental models differ, why the cost of accommodating them has been prohibitive, and what near-term steps are available within today's software stack.

This post approaches it from the architecture side. Those near-term steps — asking users what kind of thinker they are, matching preferences at install time — are configuration. They change what is turned on or off. They do not change how the product is built. The question here is what changes when the product itself can be structurally different for different users.

---

## The Real Shift

The conventional narrative is that AI makes software cheaper to build. That is true but uninteresting. Cheaper code production is a linear improvement on an existing model — the same architecture, produced faster.

The structural change is different. AI makes it possible to define every layer of a software stack as a spec — and to validate the entire system end-to-end before building it. A product, or the next version of a product, can first exist entirely as specs across all layers. AI can visualize how those specs interact, mock any layer to test behavior against the others, and iterate on the design in compressed cycles — all before a single line of production code is written. The layers still get materialized. The product still ships. But the development cycle fundamentally changes: you define, validate, and iterate in spec space first, then materialize.

This was always conceptually possible. It was never economically practical. Each layer transition used to require specialized human effort that could only happen against materialized artifacts:

| Transition | Before AI | With AI |
|---|---|---|
| Spec → Realization | Multi-month engineering effort; the spec had to be materialized into a working system before anyone could evaluate whether the design was right | The realization exists as a spec first — a derived, platform-specific specification. AI can visualize and validate it against the layer above. Materialization happens once the design is validated, in days instead of months. |
| Realization → Configuration | Consulting engagement; configuration required a running system to configure against | Configuration is defined as a spec against the realization spec. AI validates the configured behavior by mocking the realization. You see how it behaves before you build it. |
| Configuration → User Profile | Product team's quarterly roadmap; required a running system to tune and test | User preferences are a spec. AI maps them onto the configuration spec and simulates the personalized behavior. The team validates fit before materialization. |

The key insight is not just that these transitions are faster — though they are. It is that each layer can be fully defined as a spec, and the interactions between layers can be tested end-to-end, before anything is built. The entire stack can be designed, validated, and iterated on in spec space. When the design is right, AI materializes it.

![The development cycle shift — from build-first to spec-first](/assets/images/blog/2026/03/18/dev-cycle-shift.png)

This was not impossible before AI. Layered architectures and separation of concerns have existed for decades. But validating a multi-layer system required building it first — you could not test the interactions between layers without materializing them. AI changes this by making spec-level visualization and validation practical for the first time.

<!--more-->

---

## The 4-Layer Composition Model

When every layer can be defined as a spec and AI can validate inter-layer behavior before materialization, a composition model emerges that was always theoretically sound but never practically viable.

![The 4-Layer Composition Model](/assets/images/blog/2026/03/18/4-layer-stack.png)

| Layer | Name | Core Concern | In the Development Cycle |
|---|---|---|---|
| 1 | Specification | What must hold | Contracts, interfaces, invariants, and pluggable component boundaries. Defines the possibility space without dictating implementation. Always a spec — this layer is never "materialized" in the traditional sense. |
| 2 | Realization | What makes it real | Makes the spec concrete. Exists as a derived spec first (e.g., a platform-specific specification), then materializes into code or an adapted architecture when validated. AI can visualize and test the realization against the spec before building. |
| 3 | Configuration | What to tune | Parameters, thresholds, modes, behavioral tuning. Defined as a spec first, validated against the realization spec. Materialized when the system ships or is deployed for a specific domain. |
| 4 | User Profile | What the user wants | Preferences, overrides, personalization — expressed as constraints. Defined as a spec, mapped onto the configuration layer, validated for fit. Materialized at runtime when the user interacts with the system. |

Each layer multiplies the diversity of the layer above it. One spec produces many realizations. Each realization supports many configurations. Each configuration serves many user profiles. The critical property is that each layer is a **clean substitution boundary** — you swap at the level you care about without disturbing the layers above or below.

The development cycle changes fundamentally. Before, the cycle was: define a layer → build it → test it → move to the next layer → discover a problem → go back and rebuild. With the 4-layer model, the cycle becomes: define all four layers as specs → use AI to validate the interactions between them → iterate on any layer without rebuilding the others → materialize when the design is right. AI compresses the cycle from months of build-test-iterate to days of define-validate-iterate.

If this sounds like the two-spec model from the previous post — where a mental model spec and a product spec combine to generate a personalized product — it is. The 4-layer model is the architecture that makes the two-spec model practical. The product spec is Layer 1. The mental model spec feeds into Layer 4. Layers 2 and 3 are the spec-driven machinery in between that lets one become the other — validated in spec space, materialized when ready.

The model applies at every scale. A web application with no hardware, no OS, no drivers — just a frontend, an API, and a database — can be developed as 4-layer specs just as well as a platform product. Layer 1 defines the application's contracts and interfaces. Layer 2 realizes it for a specific stack — React, Rails, Postgres, or whatever the team chooses. Layer 3 configures it for a specific domain or deployment. Layer 4 personalizes it for each user. The examples later in this post lean toward hardware and platform scenarios because the cost savings are most dramatic there, but the model is not limited to them. Any software product with enough complexity to benefit from separation of concerns can be structured this way.

All four layers can live within the same organization. The layers are not a new org chart. They are separation of concerns — and the concerns remain distinct regardless of how the teams are structured.

Three things are worth noting. First, AI compresses the effort required at each layer transition, which means smaller teams can operate across more layers than before. For a small product, a handful of people with coding agents might cover all four. But for a complex system — an operating system, a platform, an enterprise product — each layer will still require dedicated teams with deep domain expertise. The 4-layer model does not eliminate organizational complexity. It clarifies it.

Second, each layer is not a single spec file. You cannot define an operating system in one file any more than you can define it in one codebase — and even a web application of moderate complexity will have many spec files per layer. Each layer will contain specs organized by their own separation of concerns — modules, subsystems, interfaces, each with its own spec. The 4-layer model is a *structural* separation, not a *file-level* one. Within each layer, the same principles of modularity and decomposition apply.

Third, the layers are not prescriptive about technology. The same spec at Layer 1 could produce a React frontend or a native iOS app at Layer 2. The same Layer 2 realization could be configured for healthcare or education at Layer 3. The model is technology-agnostic by design — the specs define behavior and contracts, not implementation choices.

---

## What Changes

Three things change that could not change before.

**The cost of iteration inverts.** In the old world, the foundation was the least flexible layer — changing a framework meant rewriting everything above it, because every layer was a committed artifact. In the 4-layer model, the foundation is the *most* flexible. Specs are text. Changing a contract costs a conversation. Because the system can be validated in spec space before materialization, you can iterate on any layer without rebuilding the others. For small and medium systems, even a full materialization can be regenerated from an updated spec in hours.

For large systems, full regeneration is still cost-prohibitive. But the 4-layer model helps there too, because clean substitution boundaries mean you can re-materialize a single layer without touching the others.

The least flexible layer is actually Layer 4 — user profiles. Not because they are hard to change technically, but because they represent accumulated human preferences and habits. You can regenerate a component overnight. You cannot regenerate a user's trust, muscle memory, or workflow expectations.

**Constraints can flow upward.** In the traditional model, the spec constrains the realization, the realization constrains the configuration, the configuration constrains the user. The user is at the bottom — the most constrained, the least powerful.

![Constraint flow inversion — from top-down to bottom-up](/assets/images/blog/2026/03/18/constraint-flow.png)

The 4-layer model makes a different flow possible. A user can say: "These are my preferences, and they are non-negotiable." Now the configuration must satisfy the user's profile. The realization must support that configuration. The spec must accommodate that realization. The user — not the architect — defines the ground truth.

Think of it in terms of governance. The traditional model works like top-down law: a constitution constrains legislation, legislation constrains policy, policy constrains individual choice. The individual has the least freedom. The inverted model works differently: the individual states their needs, and the system adapts upward — policy adjusts, legislation accommodates, the constitution evolves to serve.

Because all four layers exist as specs before materialization, this upward flow becomes tractable. AI can take a user preference, propagate it upward through configuration and realization, and validate whether the current specification accommodates it — all in spec space. If the spec needs to change, the change is a spec change validated against the other layers, not a rebuild.

This is not fully practical today. A user preference that seems simple — "I want thoroughness over speed" — might require a different scheduling algorithm, a different realization entirely, a different spec. The tooling does not exist yet. But in the old world, even imagining this was absurd. In the new world, where layers are structured as substitution boundaries over specs, it becomes a question of tooling maturity, not architectural possibility.

**Entire categories of cost shrink dramatically — and the work stays in-house.** Consider a company that builds both hardware and the software that runs on it. Today, the software layer is a permanent cost — maintaining drivers, SDKs, and tooling across versions and platforms. With Spec-Driven Development, the hardware is described by a spec. The software layer is described by a spec. When a new hardware version ships, the software does not need to be manually rewritten — AI validates the existing software spec against the updated hardware spec, identifies what needs to change, and materializes the updated artifacts. For a small hardware product, the entire software stack can be generated and verified from the spec. For a large one, the spec still reduces the engineering effort to the parts that are genuinely novel — the rest is derived. Take this further: a company like Apple builds the hardware and the OS, but has always relied on third-party developers for the long tail of end-user applications. With the 4-layer model, that changes. Apple can define specs for far more of that surface — productivity tools, utilities, domain-specific apps — and materialize them in-house. The same architecture that lets them generate drivers from a hardware spec lets them generate applications from a product spec. The app ecosystem does not disappear, but the dependency on it shrinks. The platform owner can cover more ground with fewer people.

This has a second-order effect that matters as much as the cost reduction: the work that used to require consultants and third-party vendors can now happen inside the organization. Each layer transition — spec to realization, realization to configuration — used to demand specialists who understood both sides of the bridge. That expertise was expensive and external. When AI handles the transitions and the entire system is defined in spec space, the organization's own domain experts can author, validate, and iterate on every layer. The knowledge stays internal. The dependency on external vendors shrinks to the genuinely novel — not the routine translation between layers.

Now apply this to the UX problem from the previous post. A team defines the base product as specs — Layers 1 and 2. AI handles Layers 3 and 4, configuring the product for each user's mental model and materializing the personalized interface when the product ships or when the user first interacts with it. The cost of personalization drops from "dedicated team per variant" to "spec plus prompt." The marketplace model I described in the previous post — where a company delivers base software and a coding agent generates the personalized UX layer at purchase time — is just the 4-layer model applied to the two-spec product, with materialization happening at the point of delivery.

---

## Two Teams, One Product

The spec-driven model enables an organizational structure that was not practical before: spec development and artifact validation as two parallel teams.

![Two Teams, One Product — spec team runs ahead, artifact team follows](/assets/images/blog/2026/03/18/two-teams.png)

The spec development team works in spec space — defining, iterating, and validating layers against each other using AI. They can run several months ahead of the artifact team, because their output is specs, not code. They are not waiting for builds. They are not blocked by integration. They are designing the next version of the product while the current one is still being materialized.

The artifact team takes validated specs and materializes them — building, testing, and shipping production code. When issues surface during artifact validation, the feedback goes back to the spec development team, who incorporate it into the next spec version. The loop is tight but the teams are decoupled.

This changes what gets shipped per iteration. In the old model, a single team defined, built, tested, and iterated — sequentially. The number of features per release was constrained by the speed of that sequential pipeline. In the spec-driven model, the spec team can define and validate multiple features in parallel while the artifact team materializes the previous batch. The result is more features per iteration and a more mature product at each release.

It also changes what stays in-house and what gets outsourced. Spec development — the high-leverage work of defining what the product is and how it behaves — stays internal. The domain knowledge, the architectural decisions, the design intent: all of it lives in the specs, owned by the organization. Artifact materialization — the translation of validated specs into production code — becomes the layer that can be outsourced if needed. The spec is the source of truth. Whoever materializes it is executing against a validated design, not making design decisions.

This is the inverse of how outsourcing has traditionally worked. Companies used to keep the code in-house and outsource the "thinking" to consultants — architecture reviews, configuration engagements, integration projects. In the spec-driven model, the thinking is the product. The code is the output.

---

## Why This Was Not Possible Before

The 4-layer model is not new as an idea. Software architecture has always aspired to separation of concerns, pluggable components, and configuration-driven behavior. What is new is the ability to define all layers as specs and validate the system end-to-end before building it.

| Dimension | Before AI | After AI |
|---|---|---|
| Development cycle | Define a layer → build it → test it → discover problems → rebuild (months per cycle) | Define all layers as specs → AI validates interactions between layers → iterate in spec space → materialize when validated (days per cycle) |
| Testing without building | Not possible; you had to materialize each layer before you could test its interactions with the others | AI mocks any layer and tests end-to-end behavior against the specs. You see how the system behaves before you build it. |
| Who can define layers | Only engineers who could produce and maintain artifacts at each layer | Anyone who can write or review a spec — domain experts, users, AI agents |
| Organizational dependency | Layer transitions required external consultants and third-party specialists | Organizations own the full stack in spec space; external dependency shrinks to the genuinely novel |
| Personalization depth | Settings page: themes, feature flags, notification preferences. Cosmetic, not structural | Structural adaptation: different realizations materialized per user, per context, per deployment |
| Cost model | Permanent teams maintaining materialized artifacts at each layer and the bridges between them | Spec authorship and verification; AI handles validation and materialization |

The one-size-fits-all model won not because it was better, but because every layer had to be built before it could be tested. If you wanted four independent layers, you needed four sets of artifacts — maintained, tested, and integrated by four sets of teams. The total cost of building before validating exceeded the cost of just shipping one thing to everyone.

AI changes the equation by decoupling validation from materialization. You can define all four layers as specs, validate their interactions end-to-end, and iterate on the design — all before producing a single artifact. The roles that existed to bridge abstraction layers — to turn one layer's spec into the next layer's artifact — are exactly the roles that AI collapses. What remains is the need to think clearly at each layer: what must hold, what makes it real, what to tune, what the user wants.

---

## The Bigger Picture

![Today vs Tomorrow — from one-size-fits-all to composition](/assets/images/blog/2026/03/18/today-vs-tomorrow.png)

The previous post argued that the OS should own the user's mental model — store it, standardize it, make it portable. This post provides the architecture that makes that ownership meaningful. Without the 4-layer model, a portable mental model spec has nowhere to plug in. The OS can store it, but applications cannot use it structurally. With the 4-layer model, the mental model spec is Layer 4 — and any application built on this architecture can read it, apply it, and materialize an adapted experience accordingly.

This is why Spec-Driven Development is not just a productivity technique. It is the structural prerequisite for the 4-layer model — and "spec driven" means exactly what it says. Every layer is driven by a spec first. The system is defined, validated, and iterated on in spec space. AI handles the visualization, the validation, and ultimately the materialization. I wrote about this in [the first NLSpec post](https://sddiv.github.io/blog/2026/02/23/from-tokens-to-specs-why-i-formalized-nlspec/): "When intelligence is commoditized and tokens are a unit of intelligence, the leverage isn't in the code. It's in the spec."

The one-size-fits-all model was an economic necessity, not a design ideal. AI removes the necessity — not by making artifacts cheaper to produce, but by making it possible to validate the system in spec space before committing to materialization. Spec-Driven Development provides the structural guarantee. Together, they make the 4-layer composition model viable for the first time — not as an industry standard, but as an architectural choice available to any organization willing to adopt it.

One spec. Many realizations. Many configurations. Many user experiences. Each layer defined as a spec. Each interaction validated before materialization. Each constraint traceable to the layer above — or, when the user defines the ground truth, flowing upward from below.

How do you actually test a system that exists as specs? How do you mock a layer, validate end-to-end behavior, and build confidence in a product before writing production code? That is the subject of the next post.

---

**[NLSpec Specification](https://github.com/sddiv/NLSpec-Specification)** | **[OpSpec Specification](https://github.com/sddiv/OpSpec-Specification)**
