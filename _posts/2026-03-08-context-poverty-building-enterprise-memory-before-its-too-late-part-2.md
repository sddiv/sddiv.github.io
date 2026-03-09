---
layout: post
title: "Context Poverty Part 2: Building Enterprise Memory Before It's Too Late"
date: 2026-03-08
author: Divyendu Singh
---

Part 1 mapped the problem. Most enterprises are context poor — they have the artifacts but not the reasoning that produced them. By 2027, the gap between the organizations that captured why-data and the ones that did not will be visible to everyone.

This is what you do about it.

The answer is not a platform purchase. It is not a model upgrade. It is two problems that have to be solved in a specific order: a people problem and a technology problem. Get the order wrong and neither solution works.

## Context Thinking

Context Poverty is a people problem. There is no way around that. But the solution is not to ask people or processes to change overnight. It starts with two acceptances.

First, the organization has to accept that Context Poverty exists. This is harder than it sounds. Most organizations believe they have a data problem or a tooling problem. Recognizing that the real gap is the reasoning behind the artifacts — the why-data that was never captured or has been lost — requires looking at the problem differently.

Second, the organization has to treat Enterprise Memory as an asset. In the AI world, enterprise context is the main product. Everything else — the code, the data, the pipeline — is an artifact. This is a fundamental inversion of how most organizations think about what they own.

For some organizations, this means working backwards — converting artifacts back into context. Reverse-engineering business rules from test cases. Extracting architectural reasoning from code review history. Reconstructing decision rationale from the people who were in the room. This is slow, expensive, and imperfect. But it recovers some of what was lost.

For some, the context loss is so deep that the honest answer is starting over. Not rewriting the codebase — rebuilding the reasoning layer from scratch, treating every system as if it needs to be understood again for the first time.

And for all organizations, a hard truth: 100% context coverage is impossible. Context has always decayed — people leave, people retire, institutional memory walks out the door. In the past, this was an accepted cost of doing business. In the AI world, it is the difference between AI that works and AI that produces plausible-wrong outputs.

The real innovation is not capturing all context. It is minimizing context loss over time. Slowing the decay. Building systems and habits that capture why-data as a byproduct of work, so the graph gets denser every day instead of sparser.

I want to be honest about what I describe here. I am yet to try this but this feels like the only plausible solution. The innovation that will prove this theory will come next from others who think similarly and arrive at the same conclusion.

## Enterprise Memory

Enterprise Memory is the collective, persistent memory of an organization — not stored in any single person's head, not locked in any single tool, not scoped to any single AI session.

It is not an LLM's memory. LLM memory is personal, session-scoped, and model-dependent — it remembers what one user discussed in one conversation. Enterprise Memory is organizational, persistent, and tool-agnostic. It is what the organization knows, why it knows it, and how that knowledge connects.

Think of it as a graph. The nodes are artifacts — code, documents, systems, decisions, processes, people. The edges are why-data — the reasoning that connects one artifact to another. Why does the checkout service call the legacy payments API instead of the modern one? Because of a bank partnership signed in 2019. Why was that partnership signed? Because the company was entering a new market and needed local payment processing. Why was that market chosen? Because the board approved a growth strategy that prioritized transaction volume over margin.

One artifact — the checkout service — connects through three edges of reasoning to a board-level strategy decision. Without those edges, an AI looking at the checkout service sees an outdated API call. With them, it understands why it cannot be changed without renegotiating a partnership.

The artifacts are what most organizations already have. The edges are what most organizations have never captured. A graph with nodes but no edges is a collection of disconnected facts. It is not memory. Enterprise Memory is the edges.

The four context types from Part 1 map directly onto this graph. Data Context is the nodes themselves — what happened, what was built. Product Context, Process Context, and Company Context are the edges — the why-data that gives the nodes meaning. Context Poverty, in graph terms, is high node density and low edge density. Many artifacts. Almost no reasoning connecting them.

If context is a graph, then context loss is measurable. Graph density — the ratio of actual edges to possible edges — is a real-time metric. An organization can track its Enterprise Memory density the way it tracks code coverage or system uptime. When an engineer leaves and their undocumented reasoning goes with them, the graph gets sparser. When a team captures architectural decision records as part of their workflow, the graph gets denser. The trend line tells the organization whether its memory is growing or decaying — not in theory, but in numbers, tracked over time.

This changes the conversation. Context Poverty stops being a philosophical concern and becomes an operational metric. A team can report on it. A leader can set targets for it. An organization can see, in real time, whether its AI systems are getting more trustworthy or less.

Enterprise Memory is the asset that makes AI useful at the organizational level. When an AI agent queries Enterprise Memory, it does not just retrieve a document or a data point. It traverses the graph — following the edges from what was asked to why it matters, what it connects to, and what the organization knows about it. The richer the edges, the better the AI reasons.

## The Technology Problem

Even when an organization accepts Context Poverty and begins building Enterprise Memory, the technology landscape will work against them.

Every tool an enterprise uses — AI or otherwise — is a context silo. Copilot captures reasoning in Microsoft's graph. Claude in Anthropic's. Gemini in Google's. Jira in Atlassian's world. Slack in Salesforce's. Notion, Confluence, Linear — each with its own API, its own data model, its own retention policy. The why-data is being generated every day across all of them. None of them share it.

The natural response is to connect the silos. Wrap each system in an MCP server and let the AI query whichever tool it needs.

But how does the AI know what to query? MCP tools describe what the tool can do — "I can search Jira tickets," "I can fetch Confluence pages." The AI picks a tool based on the description. What happens when two tools can fetch the same data but neither holds the context you need? What happens when the answer requires understanding the order in which decisions were made — why the organization built product A before product B, why feature X was prioritized over feature Y? That reasoning is not in Jira. It is not in Confluence. It is not in any system that an MCP server can wrap.

MCP is as good as the data on the other end. Right now, nobody is capturing why-data. The tools hold artifacts — tickets, documents, messages, code. They do not hold the reasoning that connects those artifacts. Until organizations start capturing why-data, MCP gives fast access to disconnected facts. It does not give memory.

And when organizations do start capturing why-data — and they will have to — four problems surface immediately.

**A data pipeline is not Enterprise Memory.** A data engineer will look at this problem and see a familiar shape: data in multiple systems, bring it together. Build a pipeline. ETL the context into one place. But a pipeline that copies documents from Confluence into a data lake is not Enterprise Memory. It is a copy of artifacts without edges — the same disconnected nodes, just in a different location. Enterprise Memory is not about where the data lives. It is about the reasoning connections between the data that were never captured in any system. No pipeline can extract what was never written down.

**Distributed context cannot be measured.** When why-data stays scattered across ten systems, there is no way to measure Enterprise Memory density. No way to track context coverage. No way to see whether organizational memory is growing or decaying. What is not centralized cannot be measured. What cannot be measured cannot be managed.

**Your real product lives on someone else's infrastructure.** Why-data — the reasoning, the decisions, the institutional knowledge — is the most valuable asset an organization has in the AI world. And it is distributed across vendors who will keep it only as long as the contract is active. When you leave Slack, your decision threads leave with it. When you leave Confluence, your architectural reasoning leaves with it. The organization is distributing its real product to vendors who treat it as their data, not yours.

**The cost compounds with every query.** Every AI question that needs cross-system context hits multiple APIs. The AI calls Jira, then Slack, then Confluence, then GitHub — for a single question. And it makes the same calls next time, because there is no memory of what it already learned. No caching of context. No graph to traverse. Just repeated, expensive, redundant API calls to systems that charge by usage. At enterprise scale, this is not just slow. It is unsustainable.

The logic leads to one place. MCP is useless without why-data. When organizations start capturing why-data, it will be scattered across every tool. If you are going to capture it anyway, put it in one place. And putting it in one place requires a standard.

That standard is what I am calling the Context Collection Protocol.

## Context Collection Protocol

The data engineering world solved this problem once before.

Before Open Table Formats — Iceberg, Delta Lake, Hudi — your data was locked to whatever engine you chose. Spark data stayed in Spark's format. Presto had its own assumptions. Moving between engines meant rewriting pipelines. OTF said: store data in an open format, and any engine can read it. The storage layer became vendor-neutral. The compute layer became a choice.

Enterprise Memory needs the same thing — not for data, but for why-data.

A Context Collection Protocol would standardize how tools emit why-data into Enterprise Memory. Not how AI calls tools — that is MCP. How tools emit context. The difference matters. MCP is pull: the AI asks for something. CCP is push: the tool emits reasoning as it is generated, whether or not an AI is asking for it right now.

Every tool in the enterprise stack already generates why-data as a side effect of work. A PR review contains architectural reasoning. A Slack thread contains decision rationale. A meeting transcript contains the tradeoffs that were discussed before the decision was made. Today, all of this stays in the source system, unstructured, unconnected, decaying. CCP would give each of these tools a standard way to emit that reasoning into Enterprise Memory — as nodes and edges in the graph.

Critically, CCP would filter at the protocol level — extracting why-data from raw communication in a neutral form. The graph captures *why* a decision was made without preserving the exact words someone used to describe it. This is not just good hygiene. It is what makes Enterprise Memory legally viable in organizations with strict data retention policies.

Like OTF, the protocol would decouple capture from retrieval. Any tool can emit. Any engine can query. The organization owns the graph. The vendors own the tools — but not the memory.

## What Changes When Enterprise Memory Exists

If why-data lives in a shared graph, then context specifications no longer need to carry all of the reasoning themselves.

An [NLSpec](link) is not an artifact — it is structured context. A product specification that captures intent, constraints, and reasoning in a form that both humans and AI can work from. An [OpSpec](link) does the same for operational processes. They are why-data, not output.

When Enterprise Memory exists, these specifications can point to the graph instead of embedding every business rule and constraint inline. A coding agent working from an NLSpec can query Enterprise Memory in real time — retrieving business rules, constraints, and tradeoffs at the moment it needs them, not because someone anticipated every possible question and wrote it into the spec.

The specs become leaner. The memory becomes richer. And they live together — the NLSpec, the OpSpec, and the why-data graph — as a unified system where the product definition, the operational definition, and the reasoning that produced both are all connected.

## What You Can Do Now

The tools do not exist yet. They will. But tools are the easy part. The hard part is getting an organization to believe that the product has changed. In the AI era, the product is the specification and the reasoning behind it. Provide that to an AI and it can produce the artifacts. The code, the pipeline, the dashboard — these are outputs, not assets. The why-data is the asset.

That is the conversation worth having now. Not about platforms. Not about protocols. About why the reasoning exists, why it should be preserved, and why treating it as disposable is the most expensive decision an organization can make in the AI era.

Go back to your organization and ask one question: can we explain why our critical systems are built the way they are — without asking someone? If the reasoning only exists in people's heads, it does not exist in a form that AI can use. That is your Context Poverty made visible.

The tools will follow. The organizational willingness to use them will not appear on its own. That is the work of now.

## Conclusion

Context Poverty is not a technology problem with a technology solution. It is an organizational condition that requires a shift in how enterprises think about what they produce.

The artifacts are not the product. The reasoning is.

Enterprise Memory — the collective, persistent, measurable graph of why-data — is the asset that will separate the organizations that succeed with AI from the ones that do not. The Context Collection Protocol is how that memory gets built. Neither exists as a product today. Both will.

The organizations that start capturing why-data in 2026 will not have a complete Enterprise Memory by 2027. They will have a denser graph than everyone who waited. In the AI world, that is enough.