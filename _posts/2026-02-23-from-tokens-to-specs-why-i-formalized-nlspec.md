---
layout: post
title: "From Tokens to Specs: Why I Formalized NLSpec into a Specification"
date: 2026-02-23
author: Divyendu Singh
---

## Context

### The five levels of AI coding

Dan Shapiro wrote [the definitive framing](https://www.danshapiro.com/blog/2026/01/the-five-levels-from-spicy-autocomplete-to-the-software-factory/) of the five levels of AI coding — modeled on the NHTSA's five levels of driving automation:

| Level | Analogy | What you are |
|-------|---------|--------------|
| **0** | Your parents' Volvo | Manual coder |
| **1** | Lane-keeping assist | Occasional AI user |
| **2** | Highway Autopilot | AI pair programmer |
| **3** | Waymo with safety driver | Manager drowning in diffs |
| **4** | Robotaxi | PM who writes specs and waits for tests |
| **5** | Dark Factory | A black box that turns specs into software |

> *"It's dark, because it's a place where humans are neither needed nor welcome."* — Dan Shapiro

I came across this post living between Level 3 and Level 4. At work — Level 3: the safety driver in the Waymo, reviewing diffs, the human in the loop on every decision. On POCs and hobby projects — Level 4: writing specs, leaving the agent to run, checking if tests pass. NLSpec itself is Level 4 work. Dan's framing was the wake-up call: even Level 4 feels like you're done. You're not.

<!--more-->

### Nate Jones Video

Then I watched a talk by Nate Jones — [go watch it](https://www.youtube.com/watch?v=-bQcWs1Z9a0). It added a critical dimension to the picture.

**The core argument:**
- Intelligence is being commoditized
- Tokens are a unit of intelligence
- Organizations are no longer driven by headcount — they're driven by a developer's ability to convert intelligence spend into business value
- The key metric: how many tokens can the business provision to every developer

**Three emerging developer career tracks:**

- **AI Architect** — foundational infrastructure, reliable systems on top of probabilistic AI, overall AI architecture
- **System Operator (Optimizer)** — manages velocity, AI-assisted coding process, the dark factory workflow
- **Domain Translator** — technical fluency + deep domain expertise, bridge between technology and the real world

### My two cents

This three-track model is transitional, not permanent. By H2 2027 into 2028, as AI development matures and becomes more framework-driven, I expect the tracks to begin re-converging into a familiar pattern:

| Today's AI Track | Tomorrow's Role |
|---|---|
| AI Architect | Systems Engineer |
| System Operator | Software Engineer |
| Domain Translator | Business Systems Analyst |

The one-person AI developer will exist — but as a niche, not the norm. And by late 2028 into early 2029? If the tooling matures the way I think it will, we may be riding a full AI-driven economic boom. Fingers crossed.

**I've seen this movie before — three times:**

- **Console gaming (1980s):** Atari bedroom coders → Nintendo's licensing model and cartridge costs locked out individuals → by the SNES/Genesis era it was almost entirely studios with capital
- **App Store (2008):** Explosion of indie developers → by 2012-2014, corporate teams with capital dominated the top charts — a solo developer's $5 app created in weeks no longer stood a chance
- **PC/Mobile indie (2010s):** Unity lowered the barrier → indie games had a golden window → studios with QA and marketing took over the top grossing charts

The platform matures. The economics consolidate. The lone wolf becomes the exception. **AI-driven development is on the same trajectory** — and the tools I build today need to scale beyond the solo developer.

---

## NLSpec

[StrongDM's Software Factory pattern](https://factory.strongdm.ai) is built for today's world — the 3-developer AI team. Their principles are the right foundation:

- **Seed** → the initial spec, PRD, or codebase
- **Validation** → end-to-end harness, as close to real environment as possible
- **Feedback loop** → output fed back into inputs, self-correcting, compounding correctness
- The loop runs until holdout scenarios pass — and stay passing

This is the right philosophy. But in 2-3 years, organizations will be running dozens of agents across hundreds of specifications. A markdown file handed to an agent won't scale.

**Spec-Driven Development (SDD) is the correct pattern. NLSpec is the formalization of it at organizational scale.**

- [StrongDM](https://factory.strongdm.ai/) coined the term "NLSpec" — a human-readable spec directly usable by coding agents
- I am adopting their terminology and formalizing it into an **evolving specification for organizational-scale AI development**
- NLSpec stands on StrongDM's shoulders, not in competition with them

---

## NLSpec Is Defined by NLSpec

The NLSpec specification — the document that defines what NLSpec is, how it works, what the element types are — **is itself written as an NLSpec.**

The spec for the spec is a spec. This isn't a cute trick. It's the bootstrap proof.

**Why this matters philosophically:**
- If NLSpec can describe itself completely and unambiguously, it proves the format is expressive enough to describe real systems
- It means you can load the NLSpec spec into a fresh MCP server and let agents reason about the system they're working inside

**Why this matters practically:**
- The 15-section structure was designed by using it to describe a real, complex system (itself)
- Every element type — RECORD, FUNCTION, SCENARIO, ENDPOINT, PIPELINE — appears in the NLSpec spec
- The cross-reference system (USES, USED BY, SEC tags) was exercised on a spec with dozens of interdependencies

Check the [repository](https://github.com/sddiv/NLSpec-Specification) — the framework spec is itself an NLSpec document. When the MCP server is built and the scenarios run, it should validate cleanly against the schema it defines. That's the next post.

---

## The Bootstrap Phases of NLSpec

NLSpec meets you where you are. Nobody starts with an organizational spec — everyone starts with one file. The phases describe how the tooling grows with you:

| Phase | What You Have | What You Get | When to Move On |
|---|---|---|---|
| **0** | 1 spec, 1 agent | Template + CLAUDE.md, no tooling | Spec exceeds 3,000 lines |
| **1** | 1 large spec | Bootstrap MCP server, 8 tools | Need to split by concern |
| **2** | N specs | Namespaces, cross-spec queries, decomposition | Multiple projects/teams |
| **3** | N projects, N teams | Org-scale management, A2A orchestration | — |

**Phase 0 is where everyone starts — and where NLSpec is right now.** Copy the template, fill it in, hand it to an agent. No server, no MCP, no namespaces. Just a markdown file. This already works with any agent today.

Each phase is self-contained. You don't need Phase 2 to get value from Phase 1. You don't need Phase 1 to get value from Phase 0.

## The 6 Agent Operating Modes

Within any phase, the agent operates in one of six modes. **The mode is determined by how you instruct the agent — not by the state of the codebase.**

| Mode | Trigger words | What the agent does | Modifies spec? | Modifies code? |
|---|---|---|---|---|
| **SPEC** | "spec", "refine", "write spec", "add scenarios" | Refines and improves the spec | Yes (with approval) | No |
| **DESCRIBE** | "explain", "walk me through", "what does this do" | Explains the spec in plain language | No | No |
| **IMPLEMENT** | "implement", "build", "create" | Generates codebase from spec | No | Yes |
| **FIX** | "fix", "bug", "broken", "failing" | Targeted bug fix | No | Yes |
| **VALIDATE** | "validate", "test", "verify" | Runs tests, reports results | No | No |
| **CONSOLIDATE** | "consolidate", "absorb patches", "clean up" | Absorbs patches, refactors | No | Yes |

**How the modes map to StrongDM's loop:**

- **Seed** → SPEC mode. You're defining the contract. The agent checks for missing elements, proposes scenarios, validates cross-references. No code written.
- **Validation** → IMPLEMENT mode. The agent reads the spec section by section, builds the full codebase, writes tests for every SCENARIO, and does not stop until all pass. The spec is the harness.
- **Feedback loop** → VALIDATE + FIX. The agent runs the suite, reports what's broken, makes targeted fixes. Does not refactor, does not add features.
- **Cleanup** → CONSOLIDATE. Accumulated patches are absorbed into clean structure. All scenarios must still pass.

**The key insight:** each mode has a hard boundary. SPEC mode never touches code. IMPLEMENT mode never touches the spec. FIX mode never refactors unrelated code. These boundaries are what keep agents from going rogue.

---

## The Template: Common Nouns and Verbs

Every NLSpec document follows a **15-section structure** with a controlled vocabulary of typed elements — parseable by both humans and agents.

**Element Types:**

| Element | What it is | Required fields |
|---|---|---|
| `RECORD` | Data structure | `USED BY` references |
| `FUNCTION` | Unit of behavior | `USES` + `THROWS` |
| `SCENARIO` | Test case | `[SEC:x.y]` tag + tier (`[SMOKE]`, `[AFFECTED]`, `[FULL]`) |
| `ENDPOINT` | API surface entry point | — |
| `PIPELINE` | CI/CD definition (inside the spec) | — |
| `CONFIG` | Runtime configuration value | — |
| `ENUM` | Constrained value set | — |

**Cross-reference system:**
- Every element carries typed relationships
- A FUNCTION that `USES` a RECORD creates a graph edge
- When an agent modifies a RECORD, it walks the graph to find every dependent FUNCTION — before making any change
- Agents assemble a minimal context slice by walking edges, not reading the whole document — this is how large specs stay manageable

**The 15-section order is deliberate:**

`Abstract → Architecture → Data Model → Core Functions → API Surface → Error Model → Scenarios → Configuration → File Structure → Build and Run`

An agent implementing from scratch works section by section with no forward dependencies.

---

## How NLSpec Differs from Existing Tools

Here's how NLSpec compares to the current landscape:

|  | StrongDM NLSpec | **NLSpec (this)** | GitHub Spec Kit | OpenSpec / BMAD / Kiro |
|---|---|---|---|---|
| **What it is** | 3 markdown files for one product | A specification | CLI + workflow scaffold | Workflow tools for SDD |
| **Spec format** | Implicit | Formalized 15-section template with typed elements | Freeform markdown | Freeform markdown |
| **Tooling model** | None — hand files to agent | MCP server (programmatic access) | Slash commands | Slash commands |
| **Element types** | Used but not defined | RECORD, FUNCTION, SCENARIO, ENDPOINT, PIPELINE — first-class, queryable | None | None |
| **Cross-references** | None | USES, USED BY, SEC tags — agents walk edges for context slicing | None | None |
| **Multi-spec** | Execution graph (pipeline nodes) | Spec composition graph (N specs with typed imports) | One spec per project | One spec per change |
| **CI/CD** | Not modeled | PIPELINE definitions, FILE_TO_SECTION_MAP | Not modeled | Not modeled |
| **Agent access** | File read | File read (Phase 0) → MCP tools: get, search, slice, create, patch (Phase 1+) | Slash commands | Slash commands |
| **Self-describing** | No | Yes | No | No |
| **Namespaces** | No | Yes — one server manages N specs | No | No |

**The core differentiators:**

- **StrongDM:** "Here are three spec files — hand them to an agent." *(A document.)*
- **GitHub Spec Kit:** "Here's a workflow to write specs and feed them to agents." *(A process.)*
- **NLSpec:** *(A formal, evolving specification.)*
  - **Grows with you** — Phase 0 starts with a markdown file, just like StrongDM. Phase 3 manages an entire organization. Same format at every phase, tooling added as you need it.
  - **Formal vocabulary in the spec** — typed elements (RECORD, FUNCTION, SCENARIO, ENDPOINT, PIPELINE) with controlled verbs (USES, USED BY, THROWS, SEC tags). Not freeform markdown — structured, queryable, composable.
  - **Formal vocabulary in the agent prompt** — six named modes (SPEC, DESCRIBE, IMPLEMENT, FIX, VALIDATE, CONSOLIDATE), each with defined triggers, boundaries, and behaviors. The agent knows exactly what it is allowed to do and what it is not.

StrongDM coined NLSpec. This work evolves and formalizes it as a specification — giving it structure, tooling, and a growth path to organizational scale.

---

## Conclusion: Skipping Ahead

**Where I was:** Between Level 3 and Level 4 — Level 3 at work, Level 4 on POCs and hobby projects. NLSpec itself is Level 4 work.

**Where I'm going:** Level 5. The Dark Factory.

**What that means in practice:** Every hobby project from now on is an NLSpec.

Dan Shapiro says he's at Level 4 — writing specs, leaving for 12 hours, checking if tests pass. NLSpec is what bridges Level 4 to Level 5:
- Level 4: hand a markdown file to an agent and hope it reads it right
- Level 5: give the agent a queryable, graph-traversable, MCP-accessible specification it can reason about programmatically

That's not an incremental improvement. It's a different substrate.

**When intelligence is commoditized and tokens are a unit of intelligence, the leverage isn't in the code. It's in the spec.**

**Where things stand today:**

The NLSpec specification is [published on GitHub](https://github.com/sddiv/NLSpec-Specification). The spec has been written — but not yet formally validated by implementing against it end to end. That is the next step: running the scenarios and proving the loop closes.

That said, I'm not starting from zero. NLSpec formalizes the same vocabulary and patterns [StrongDM](https://factory.strongdm.ai/) already proved out on Attractor — a real production system built entirely using their NLSpec format. The foundation is solid. What remains is validating the formalization itself.

If you want to get ahead of it — read the spec, try the template on your own project, and run it against an agent. I'd love to know what breaks. The spec is only as good as what survives contact with a real implementation, and the more people stress-testing it the better.

The MCP server is coming. More posts to follow.

---

*Have thoughts or found something that breaks? Find me on GitHub or drop a comment below.*
