---
layout: post
title: "Why I Rewrote NLSpec Within 24 Hours of Writing It"
date: 2026-02-27
author: Divyendu Singh
---

We are entering the era where the spec *is* the product. I wrote [NLSpec](https://github.com/sddiv/NLSpec-Specification) — a specification system for AI coding agents — and then threw it out and rewrote it from scratch the next day. Here's why.

---

## The Context: Specification Engineering Is the Job Now

If you're a software engineer in 2026 and you are still using Vibe Coding or worst coding by hand you are way behind. Vibe Coding is what you do to produce a spec now using a Research AI like Opus 4.6. The software is built using a Coding Agent using your Spec.

StrongDM coined the term "nlspec" for human-readable specifications that coding agents consume directly. GitHub shipped Spec Kit. Kiro, OpenSpec, BMAD — everyone is converging on the same idea: spec-driven development (SDD). You write a detailed specification, hand it to an agent, and get a working system back.

To be clear: the idea of NLSpec is not mine. StrongDM originated the concept and demonstrated it with their [Attractor project](https://github.com/strongdm/attractor) — three markdown files that a coding agent could implement from directly. What I did was formalize and extend that idea. I took the implicit structure (RECORD, FUNCTION, SCENARIO) that StrongDM used and turned it into a complete, typed specification system with a template, composable spec graphs, dependency contracts, MCP tooling, and a phased growth path from a single file to organizational scale.

But most of the tools in this space — including StrongDM's original approach — treat specs as documents. A markdown file. One spec, one agent, one project. That works for a solo developer building a side project. It does not work when you have 50 agents across 200 specs with cross-cutting compliance, security, and platform concerns.

NLSpec formalizes the idea further — treating specs as structured, queryable, composable data that agents consume at organizational scale. Specs that form dependency graphs. Specs that export contracts and seed each other with deterministic initialization state. A system that grows from a single markdown file to an org-wide spec graph, with MCP tooling at every phase.

I wrote the first version. It was clean, tight, internally consistent. It worked. And within 24 hours, I decided we could do better. That's when my version of NLSpec completely forked from StrongDM's original.

---

## Why I Forked: The Original Worked, But We Could Do Better

The original NLSpec had a rigid 16-section numbered template. Every spec was "Section 1: Abstract" through "Section 16: Dependency Contracts." Every cross-reference used numbers — `[SEC:5.3]`, `IMPORT Token FROM auth-spec.md Section 4.1`. Six agent operating modes. One spec type. A fixed structure that assumed every specification in every domain would fit into exactly 16 boxes.

It was a solid specification system. It addressed the problems I could see at that moment: how to structure a spec so an agent could implement it, how to slice context efficiently, how to manage patches and versioning. For a single backend system written in Rust or TypeScript, it worked beautifully.

But it couldn't build a user-facing web application.

### The spec couldn't describe what real applications need

More than the 16-section rigidity, the fundamental problem was that the original spec had no way to express what user-facing applications are actually made of. A web application isn't just a running service — it's a service composed with a design system (color tokens, typography rules, icon libraries, accessibility constraints), architectural patterns (some well-known like Repository, some novel ones you invent for your domain), and static assets with usage rules that have nothing to do with FUNCTION definitions.

The original template had no place for any of this. The Functions section was for FUNCTION definitions. The FileStructure section was for directory layouts. Neither concept applies to a design system or a reusable architectural pattern. You couldn't spec a React app that needed a component library with design tokens, a novel state management pattern, and an icon asset pack — the template simply didn't have the vocabulary for it.

The template needed to support three spec types, not one: SYSTEM for running code, PATTERN for reusable architectural blueprints, and ASSET for static resources with design constraints. A PATTERN spec's Scenarios section validates constraints and interface contracts, not end-to-end system behavior. An ASSET spec's Functions section becomes a style guide — `RULE` and `TOKEN` blocks instead of `FUNCTION` blocks. The template format stays the same. What goes inside it changes based on what you're specifying.

### Numbered sections would create brittle references

Every cross-reference in the original was a number. `[SEC:5.3]` meant "Core Functions, subsection 3." But what happens when you add a section? Or reorder them? Or when one spec needs a SystemManifest section for hardware requirements and another doesn't? Numbered sections assume a fixed, ordered list. The moment the structure becomes flexible — which it must, to support different spec types and different domains — numbered references break.

Named sections solve this. `[SEC:Functions.3]` means "the third subsection of Functions" regardless of where Functions appears in the document. You can add, remove, or reorder sections without breaking a single cross-reference. A SECTIONS declaration block at the top serves as the contract — but it's optional. Specs that don't have one still work; the parser discovers sections from `##` headers. The system meets the spec where it is, instead of demanding the spec meet the system.

### One format, no tolerance

The original expected every spec to be well-structured. All 16 sections present. Every FUNCTION with USES and THROWS declarations. Every RECORD with USED BY references. The SPEC mode in CLAUDE.md checked: "Are all 16 sections present?"

Real specs don't work that way. Sometimes you start with a minimal spec — an abstract, some function signatures, a few behavioral notes. Sometimes you have a detailed spec but it uses prose instead of formal RECORD/FUNCTION blocks. The original system would flag everything as incomplete and demand the human fix it before proceeding. That's fine for well-structured specs, but it limits adoption.

The rewrite introduces spec tolerance. The agent handles well-structured specs, loose specs, and minimal specs. Gap detection is advisory — CRITICAL, WARNING, INFO — not blocking. The agent never refuses to work with a spec because it lacks structure. It infers what it can and reports what it can't.

---

## Details Matter: Walking Through the Changes

The rewrite wasn't just philosophical. It produced concrete, specific changes that address real failure modes I hit while trying to use the system.

### Dependencies: trust the install, not training data

The original Dependencies section was five fields: name, version, required, interface, fallback. That's a description of what you need, not a protocol for getting it right.

The rewrite turns Dependencies into a full anti-hallucination system. Every dependency now declares a `category` (runtime, build, external-asset), an `install` command, a `verify` command, and `platform` constraints. Version pinning rules distinguish exact versions from ranges from "latest." But the critical addition is the post-install verification protocol:

After installing any dependency, the agent must verify its generated code against the *actual* installed artifact — not training knowledge. For libraries, it reads the installed type definitions. For CLIs, it runs `--help` and checks that the flags used in generated scripts actually exist. For asset packs like icon libraries, it lists the actual available icons and compares every icon import in the codebase against what's really there.

This matters because agents hallucinate dependency APIs constantly. The agent installs `lucide-react@0.263.1` but writes code using icon names from a different version because that's what its training data contains. The verify step catches this before tests even run.

### Architecture.3: composition over duplication

The original Architecture section had Component Inventory and Data Flow. The rewrite adds Architecture.3 — a formal composition layer:

```
USES PATTERN: Repository
  applied_to  : data access layer
  customization: "All repositories are async, return Result types"

USES ASSET: DesignSystem FROM design-system-spec.md
  applied_to  : all UI components
```

For prior art patterns — Repository, CircuitBreaker, Observer — the agent uses training knowledge. Just name the pattern and the customization. For novel patterns defined in their own PATTERN spec, the agent reads the full spec. For assets, the agent reads the ASSET spec to discover file locations and usage constraints.

This is how specs compose without duplication. The design system is defined once in an ASSET spec. Every SYSTEM spec that declares `USES ASSET: DesignSystem` inherits its rules and tokens. Change the primary color in one place, and every consuming spec picks it up.

### ARTIFACT declarations: defining "done"

The original BuildAndRun section was just commands: build, test, run, verify. The rewrite adds ARTIFACT declarations — the machine-checkable definition of what a successful build produces:

```
ARTIFACT server-binary:
  type        : BINARY
  path        : target/release/kv-server
  produced_by : cargo build --release
  checkable   : file exists AND file is executable
```

This sounds small, but it closes a real gap. Without it, the agent could pass all tests but produce no deployable artifact — tests run against an intermediate build state, the final binary is never compiled, and "IMPLEMENT succeeded" is a lie. Artifacts are verified after IMPLEMENT and again after VALIDATE.

### Dark factory mode: autonomous execution

The original had no concept of unattended execution. An agent failed, and a human decided what to do.

The rewrite adds a full autonomous execution pipeline — what I call "dark factory mode." The agent chains modes together: SPEC VALIDATION → IMPLEMENT → VALIDATE → DECISION GATE → FIX (if needed) → EXIT. Every failure is classified: SPEC_GAP (the spec is incomplete), IMPL_BUG (the code is wrong), ENV_ISSUE (the environment is broken), or AMBIGUITY (the spec can be read two ways). Each category triggers a different response — retries for IMPL_BUG, patches for SPEC_GAP, immediate escalation for ENV_ISSUE.

Guard rails prevent degenerate behavior: max 3 retries per failing scenario, max 10 total fix attempts across all scenarios, never modify the spec, never proceed past an environment issue. Everything is logged to structured JSON. A human reviewing the output can trace exactly what happened and why.

This is what makes the "3 engineers producing hundreds of patches per day" vision practical. The agents run autonomously. The humans write specs and review escalation reports.

### Drift detection: keeping spec and code in sync

The rewrite adds spec-code drift detection across five dimensions: API surface, data model, error types, config schema, and artifacts. During VALIDATE mode, the agent compares the code's actual public interface against the spec's declarations and reports any mismatches.

Drift isn't always a bug — sometimes the code evolved correctly and the spec didn't keep up. But detecting it is essential. Without drift detection, the spec gradually becomes fiction, and you're back to code being the source of truth.

---

## Conclusion

The first version of NLSpec worked. It addressed a real problem and it did it cleanly. But the rewrite pushes it further — systems composed of patterns and assets, not just services. Agents that verify instead of hallucinate. Autonomous pipelines that classify failures and act accordingly. Specs that flex to accommodate what you actually need to describe, instead of forcing everything into 16 numbered boxes.

The first version taught me exactly where the boundaries are. The rewrite is where my formalization of NLSpec fully diverged from StrongDM's original concept and became its own thing. When you see a path to something meaningfully better, the only honest response is to take it — even if it means starting over within 24 hours.

The spec is the source of truth. Even the spec for specs.

---

**[NLSpec Specification](https://github.com/sddiv/NLSpec-Specification)**
