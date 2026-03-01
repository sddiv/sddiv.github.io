---
layout: post
title: "NLSpec Alone Can’t Run Your Dark Factory"
date: 2026-02-28
author: Divyendu Singh
---

NLSpec tells agents what to build. But building is only half the problem. A true dark factory — agents running autonomously, producing artifacts, shipping to production — needs a specification for how to operationalize and run the whole pipeline. That's why I wrote [OpSpec](https://github.com/sddiv/OpSpec-Specification).

---

## The Gap: Code Specs Don't Operationalize

If you're a software engineer in 2026 and you are still using Vibe Coding or worst coding by hand you are way behind. Vibe Coding is what you do to produce a spec now using a Research AI like Opus 4.6. The software is built using a Coding Agent using your Spec. And now even continuous deployment and delivery will be done by an Agent.

Spec-driven development is converging fast. NLSpec, Spec Kit, Kiro, BMAD — everyone agrees on the core idea: write a specification, hand it to an agent, get a working system back. One spec, one agent, one artifact. That loop works.

But a production system is not one artifact. A software delivery pipeline produces a binary, a container image, a Kubernetes manifest, a database migration, and a monitoring config. A claims processing workflow produces an intake form, a fraud scoring model, an adjudication workflow, a payment instruction, and an audit report. Getting any one artifact wrong is a defect. Getting the coordination between them wrong is an outage.

NLSpec is declarative — it describes *what* a system does and trusts the agent to produce correct code. That works because each NLSpec produces one artifact with a bounded surface area. But who coordinates the five artifacts in the delivery pipeline? Who decides that the binary passed testing but the migration failed, so we rework the migration but don't roll back the binary? Who knows the order, the gates, the human sign-offs, and what to do when stage 3 fails?

NLSpec has no answer for this. It was never designed to. NLSpec says "here is what this one system does." It doesn't say "here is how you build it, test it, gate it, approve it, deploy it, monitor it, and roll it back when something breaks."

That's the gap. And it's not a small one. Without a specification for the operational pipeline itself, you end up with agents that can write code but can't ship it — or worse, agents that ship without gates, without approvals, without rollback plans. A dark factory without operational governance is just chaos running at machine speed.

---

## OpSpec: A Specification Language for Operational Workflows

OpSpec is an operational specification language. It is my original work — as far as I know, no one has published a formal specification language for operational workflows that agents consume directly.

The idea is symmetric with NLSpec:

```
NLSpec  →  coding agent  →  application code (Rust, Python, etc.)
OpSpec  →  coding agent  →  executor program (pipeline, controller, scripts, etc.)
```

NLSpec defines *what* to build. OpSpec defines *how* to deliver and operate it. A coding agent reads an OpSpec and produces the executor's program — a Temporal workflow definition, a GitHub Actions pipeline, a Python module, shell scripts, or whatever the target executor requires. The OpSpec is the specification; the produced program is the executable.

But OpSpec is not just for software delivery. The same primitives express workflows across any operational domain: insurance claims processing, loan origination, patient triage, content moderation, customer onboarding. Any process that has stages, decision gates, human interaction points, and the capacity to learn and adapt can be expressed as an OpSpec. That last part — the capacity to learn — is the key. You already have tools that can run stages and gates. Jenkins does that. Airflow does that. The reason you hand this to an agent instead is because an agent can learn from every pipeline run and improve the next one. That's what LEARNING RULE formalizes, and it's what no existing pipeline tool gives you.

---

## The Primitives: What Makes OpSpec Work

OpSpec has five primitives, each designed for a specific aspect of operational workflows.

**STAGE** — a discrete phase of work with entry conditions, concrete operations, exit conditions, and failure handling. Not a vague "do the thing" — a STAGE spells out exactly what happens, what it produces, and how long it should take. If a human can't follow it step by step, it's not a STAGE.

**GATE** — a three-band decision point between stages. Not binary pass/fail. Every GATE evaluates to PASS (proceed), REWORK (send back with context for another attempt), or FAIL (escalate to a human). The middle band — REWORK — is where most real-world iteration happens. Bounded by `max_cycles` so rework loops don't spin forever.

**BINDING** — an artifact template that the coding agent produces as part of the executor program. This is what makes OpSpec generative. A BINDING can be a PROMPT (agent instruction template with runtime variables), a RULE (deterministic check the executor enforces), an MCP_TOOL (tool integration), or a CONFIG (generated configuration). The OpSpec doesn't just describe steps — it specifies the actual prompts, rules, and configs that the executor will use at runtime.

**LEARNING RULE** — governed self-modification. This is the primitive that justifies using an agent for CI/CD in the first place. Jenkins, GitHub Actions, Airflow — they all run pipelines. They've done it for years. So why would you put an agent in charge? Because existing tools don't learn. They execute the same pipeline the same way every time, whether it's the first run or the ten thousandth. An agent running an OpSpec observes patterns across executions, accumulates evidence, and proposes changes to the OpSpec itself — but only within declared boundaries. If rework cycles at a particular gate keep hitting 3 out of 3 before passing, the agent notices and proposes raising the threshold or adjusting the upstream stage's operations. If a certain class of test failure always resolves on retry, the agent learns to auto-retry before escalating. If deployments to a specific environment consistently take 3x longer than expected, the agent proposes adjusting the timeout.

This is what static pipeline tools cannot do. They don't accumulate operational wisdom. Every pipeline run starts from zero. An OpSpec-driven agent gets smarter over time — but within governance. Some things are IMMUTABLE (approval gates can never be removed). Some are MUTABLE_WITH_APPROVAL (rework thresholds can change with human sign-off). Some are AUTO_TUNABLE (retry counts can self-adjust within bounds). The learning process can never modify its own boundaries. The pipeline improves without drifting into unsafe territory. That's the difference between a tool that runs your pipeline and an agent that operates it.

**APPROVAL** — a human interaction point where the executor pauses and waits. The pipeline runs autonomously until it hits an APPROVAL, then stops, notifies via the declared channel (Slack, email, dashboard), and waits for the required number of approvals. SLAs, escalation paths, and emergency bypass conditions are all declared explicitly.

---

## Human-in-the-Loop Is the Architecture, Not an Afterthought

This is the part most people get wrong about autonomous pipelines. The goal is not to remove humans. The goal is to put humans at the right control points with the right information at the right time.

OpSpec makes human-in-the-loop a first-class architectural concern. Every APPROVAL declares who approves, how they're notified, how long they have, what happens if they don't respond, and whether emergency bypass is allowed. Every GATE's FAIL band routes to a specific human role with specific context. Every LEARNING RULE that touches anything beyond auto-tuning requires human approval before the change takes effect.

The executor runs at machine speed between these control points. But the control points are non-negotiable. A pipeline that skips approvals is not faster — it's ungoverned. OpSpec ensures the governance is in the specification itself, not bolted on as a runtime afterthought.

---

## From NLSpec to OpSpec: The Full Picture

NLSpec alone gives you a coding agent that can produce any artifact from a specification. OpSpec alone gives you an operational pipeline that can coordinate many artifacts through a governed, human-approved workflow. Together, they give you the full dark factory: agents that know what to build AND how to build, test, gate, approve, deploy, monitor, and roll back — all from specifications that a human can read and verify.

The spec is the source of truth. NLSpec is the source of truth for what to build. OpSpec is the source of truth for how to run it.

---

**[NLSpec Specification](https://github.com/sddiv/NLSpec-Specification)** | **[OpSpec Specification](https://github.com/sddiv/OpSpec-Specification)**
