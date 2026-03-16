---
layout: post
title: "Mapping Mental Models: How AI Can Redefine UX Development"
date: 2026-03-15
author: Divyendu Singh
---

How many times have you had to learn a new app from scratch? A new project management tool, a new calendar, a new way to do the same thing you already knew how to do. The interface is different. The mental model is different. The shortcuts you built up over years are gone. You adapt to the software. The software does not adapt to you.

Why is that? We can change themes, rearrange a dashboard, pick a notification preference. But these are cosmetic. The architecture underneath — the workflows, the interaction patterns, the assumptions about how you think — is identical for every user. Very few products are truly intuitive, and the ones that feel intuitive only feel that way because you learned to think like them, not because they learned to think like you.

---

## Mental Models Can Be Specified

Here is the thing: we know how to describe good UX. Don Norman formalized mental models, affordances, and feedback loops in *The Design of Everyday Things* decades ago. The principles are well-understood. Doors should signal whether to push or pull. Controls should map spatially to the things they affect. Feedback should be immediate and proportional.

If intelligence can be captured in a neural network, mental models can be captured in a specification. And they can be written in plain English.

Here is an example. My mental model of AI is this: it is layers of light bulbs, with each layer connected to the layers above and below by wires. When you press a button on one end — ask a question, make a choice — bulbs light up across each layer, revealing a path through the wires. Press a different button, and an entirely different path illuminates. Press buttons in combination, and the paths multiply — each combination producing a unique circuit through the layers. The same question asked differently by two people lights up different pathways, because the input is shaped by different minds. If you have seen the Enigma machine demo in *The Imitation Game* — rotors turning, contacts closing, a unique circuit forming for each letter — it is something like that, but at a scale that makes every interaction unique.

I just wrote that in plain English. That is a mental model spec. Not a technical diagram. Not a formal notation. Just a description of how I think about something, captured in natural language. And it is precise enough that a product could use it — an AI tutor that explains concepts to me could lean on this model, presenting information as paths and illumination rather than as databases and retrieval.

This is the key insight: mental models can be written in English. A UX spec — not a mockup, not a wireframe, but a formal description of how a class of product should think — is entirely possible. Every calendar app could share a common mental model for what "scheduling" means. Every project management tool could agree on what "task completion" looks like cognitively. The spec would not dictate pixels. It would dictate the structure of interaction — the affordances, the feedback loops, the conceptual model that a user builds in their head.

AI should be viewed as an extension of a human brain, not a replacement for one. It does not produce one fixed answer. It responds to the specific mind engaging with it. That makes it a natural tool not just for *executing* mental models, but for *discovering* them — because it is already responding to them.

<!--more-->

We have had the vocabulary for this since the 1980s. *About Face* by Alan Cooper gave us goal-directed design. *Don't Make Me Think* by Steve Krug gave us the usability heuristics. The knowledge exists. It was never captured in a form that could drive implementation at scale.

---

## There Is No Universal Human

But even these mental models assume a universal human. There is no universal human.

Culture shapes how people read layouts. A user in an Arabic-speaking country reads right-to-left — the natural starting point of a page, the direction of scanning, the placement of primary actions are all mirrored. Color carries different weight: red signals danger in the West and prosperity in China. Information density that feels clean in Scandinavia feels sparse in Japan. Hierarchy that feels natural in one culture feels rigid in another. Every "obvious" design choice encodes cultural assumptions.

Neurodiversity makes it deeper still. A person on the spectrum may need explicit structure, predictable patterns, and literal labels where a neurotypical user prefers implied flow, progressive disclosure, and contextual cues. A user with ADHD may need aggressive focus mechanisms and minimal distraction surfaces where another user wants ambient information and multiple parallel streams. An elderly user needs larger touch targets, higher contrast, and slower transitions — not because they are less capable, but because the perceptual defaults the interface was designed for are not theirs.

The "intuitive" interface is intuitive for one kind of mind, shaped by one culture, designed for one set of perceptual defaults. Everyone else adapts. And we call that "good UX."

---

## The Real Problem Is Cost

So the problem is deeper than we thought. It is not just that we ship one product to every user. We ship one mental model to every user.

And we could not afford to do otherwise. Every layer of genuine flexibility — not cosmetic, but structural — required a team to build, maintain, and support. A culturally-aware layout system needs a team. A neurodiversity-sensitive interaction layer needs a team. An age-adaptive interface needs a team. A system where all three could vary independently, per user, was economically unthinkable.

The constraint was not imagination. The Design of Everyday Things was published in 1988. The principles have been known for nearly forty years. The constraint was that implementing those principles differently for different humans was too expensive. So we picked one mental model — the one that fit the largest addressable market — and shipped it to everyone.

---

## AI Changes the Cost

AI does not invent better UX principles. The books listed above already did that. What AI changes is the cost of translating a UX specification into a working interface — and the cost of producing *variants* of that interface for different users.

Today, a design system is built once and maintained by a team. With AI, a UX spec — a formal description of the mental model, the affordances, the feedback patterns — can be realized into multiple interfaces by a coding agent. One realization for a right-to-left culture. Another for high-density information preferences. Another for explicit-structure cognitive styles. Each realization satisfies the same spec. Each one thinks the same way at the conceptual level. But each one speaks the user's perceptual language.

The spec is the mental model. The realizations are how that model gets expressed for different humans. The user profile captures which expression fits.

But where does the user profile come from? A user can describe how they think — as I did above with the light bulb example. But more powerfully, AI can observe how they behave and write the description for them.

AI can observe how a user interacts with an interface in real time — what they click first, where they hesitate, what they skip, what they undo — and infer a mental model from that behavior. Not a static preferences file. A living model, written in natural language, that updates as the user works.

Consider a project management tool. A new user opens it for the first time. The AI observes: they immediately look for a list view, not a board view. They try to create sub-tasks before creating a parent task — they think bottom-up, not top-down. They ignore the timeline feature entirely but keep opening the search bar — they navigate by recall, not by browsing. They attempt to drag items between columns and pause when nothing happens — they expect direct manipulation. Within a few minutes of observation, the AI has a behavioral sketch: this user thinks in lists, builds bottom-up, navigates by search, and expects drag-and-drop. That sketch is a mental model — not one that was designed by a UX team, but one that was *discovered* from the user's actual behavior.

Now the system can adapt. It can foreground list views, default to bottom-up task creation, make search the primary navigation, and enable direct manipulation everywhere. Not because someone configured these preferences in a settings page. Because the AI inferred them from how the user actually thinks. And as the user's behavior changes — as they start using the timeline view after a few weeks, as they shift from search to browsing once the project structure becomes familiar — the model updates. The interface evolves with the user.

This closes the loop. The UX spec defines what the product must do. AI generates multiple realizations for different mental models. And AI observing real-time behavior figures out which mental model fits each user — and keeps refining it. The user never fills out a preferences form. They just use the product, and the product learns to think like them.

This is not science fiction. It is an architecture problem, and the economics of that architecture have changed. The cost of producing a variant that used to require a dedicated team now requires a spec and a prompt — at least for systems of moderate complexity. For large systems the cost is still significant, but it is no longer prohibitive.

---

## Store It, Standardize It, Carry It With You

Discovering a user's mental model is only half the problem. The other half is the one we started with: what happens when they switch to a different app?

Today, everything is lost. Your preferences, your learned shortcuts, your carefully arranged workspace — gone. You start over. But if the AI has mapped your mental model, that model does not have to die with the product. It can be stored.

Think about how AI memory works. A conversation context builds up over time — the model remembers what you said, how you said it, what you care about. That memory persists across turns. Some systems now persist it across sessions. The same principle applies to mental models. The AI observes you, builds a model of how you think, and writes it to a profile — not as vague preferences like "prefers dark mode," but as structural descriptions: navigates by search, thinks bottom-up, expects direct manipulation, prefers explicit labels over contextual cues.

Now standardize it. If mental models can be specified — and we argued that they can — then the format of that stored model can be a spec too. A portable spec. A user mental model specification that any product can read. When you move from one project management tool to another, your mental model travels with you. The new tool reads the spec: this user thinks in lists, builds bottom-up, navigates by search. It configures itself accordingly. Not because someone manually migrated your settings, but because the spec describes how you think, and any product that implements the spec knows what to do with that description.

This is analogous to how web standards work. Any browser can render the same HTML because HTML is a standardized spec. Any product could adapt to the same user because the mental model is a standardized spec. The difference is that the mental model spec is not authored by the user — it is discovered by AI and refined continuously.

The implication is significant. Software stops being something you learn. It becomes something that learns you — once. And that knowledge follows you everywhere.

---

## The Opersting System Should Own This

If mental model specs are portable and standardized, the question becomes: where do they live?

Not inside individual apps. An app is the wrong custodian for something this personal. If your mental model lives inside your project management tool, it dies when you switch tools. If it lives inside your browser, it does not help your desktop apps. The mental model needs to live at a layer that spans all applications.

That layer is the operating system.

This changes how operating systems like iOS, Android, and desktop platforms should be built. The OS should safely capture, store, and manage a user's mental model specs — the same way it manages contacts, credentials, or accessibility settings today. When you install a new app, the OS provides your mental model spec to it (with your permission). The app configures itself accordingly. When the AI observes your behavior and refines the model, the update flows back to the OS, and every app benefits.

The OS becomes the custodian of how you think. Not what you like — that is a preferences file. How you *think* — navigation patterns, cognitive style, information density preferences, interaction expectations. This is more intimate than a settings page and more useful than any personalization feature an individual app could build.

Privacy matters here. A mental model spec is deeply personal — arguably more revealing than browsing history. The OS must treat it with the same seriousness as biometric data: encrypted at rest, explicit consent for sharing, user-controlled access per app. But the infrastructure already exists for this kind of sensitive data management. What does not exist is the spec itself, or the AI pipeline to populate it.

---

## Two Specs, One Product

So now there are two specs. A mental model spec — how the user thinks. And a product spec — what the software does. The development team's job is to combine the two. Feed both specs to a coding agent, write the right prompts, and generate a product that does what it needs to do *in the way the user thinks about it*.

But doing this from scratch for every user is not economical. The key is that not all layers of the product need to vary. The base layer — contracts, interfaces, data models, business logic — is the same regardless of who uses it. A calendar stores events, resolves conflicts, sends reminders. That does not change based on how the user thinks. What changes is how those capabilities are surfaced: the interaction patterns, the navigation model, the information hierarchy, the feedback behavior.

So the product splits naturally. The lower layers are built once from the product spec — common infrastructure that every variant shares. The upper layers are where the mental model spec gets laced in, generating the UX that matches a specific way of thinking. The base is expensive. The UX layer on top is where AI brings the cost down.

This opens up a marketplace model. A company delivers the base software — fully functional, spec-verified, common to all users. A marketplace accepts mental model specs through upload. When a user purchases the product, the marketplace runs the final step: a coding agent takes the base software and the user's mental model spec, generates the personalized UX layer, and delivers the finished product. The user gets software that works the way they think, without the company having to build every variant in advance.

Alternatively, the company can go the other direction. Collect mental model specs in advance — from research, from AI observation of early users, from published profiles — and generate multiple versions of the product, each tailored to a different cognitive style. List view thinkers. Visual-spatial thinkers. Search-first navigators. These go on the marketplace as variants. When a new user arrives, the marketplace matches their stored mental model spec to the closest available version and installs it. No generation step at purchase time — just matching.

This is not as new as it sounds. The paint industry has done this for decades: mix-your-own-color at the point of sale. The base product (paint) is common. The customization (pigment ratios) happens at the last step, driven by a spec (the color code). Software marketplaces already do a version of this with themes, plugins, and configuration bundles. The difference is that mental model customization is structural, not cosmetic. It changes how the product thinks, not just how it looks.

---

## What Comes Next

Everything described in this post — portable mental model specs, AI-discovered preferences, two-spec product models — is structurally and culturally drastic. It asks the entire software industry to rethink how products are built, sold, and experienced. That will not happen overnight.
But there are things that can happen first, without waiting for the full vision to arrive.

The operating system should start asking users what they want. Not which wallpaper — what kind of thinker they are. Do they prefer lists or spatial layouts? Do they search first or browse first? Do they want dense information or progressive disclosure? These preferences exist today in every user's head. The OS just never asks. If it did — and stored the answers as a standardized profile — every app on the device could read that profile on first launch and adapt accordingly.

Marketplaces should allow customization at install time. When a user downloads an app, the marketplace could match their stored preferences to available configurations. No new architecture required. Just a standard format for user preferences and a willingness to read it.

And when software launches for the first time, it should apply what it already knows. If the OS has a mental model profile, the app should use it on the get-go — map the user's cognitive preferences to its existing configuration surface. Not a blank slate. Not a tutorial. A product that already fits.

This is where we start. These are incremental steps that work within today's software stack. As AI adoption deepens — as coding agents get better, as specs become the primary artifact, as the economics of variation continue to drop — we expand beyond configuration into structural personalization. The architecture for that expansion is the subject of the next post: a 4-layer composition model that makes deep personalization economically viable for the first time.
---

**[NLSpec Specification](https://github.com/sddiv/NLSpec-Specification)** | **[OpSpec Specification](https://github.com/sddiv/OpSpec-Specification)**
