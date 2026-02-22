---
title: How AI Agents Work
---

# How AI Agents Work

A plain-language guide for non-engineers.

---

## What is an AI Agent?

An AI agent is a program that can **think, decide, and act** to complete a goal — not just answer a single question.

Think of the difference between a search engine and a personal assistant. A search engine responds to exactly what you type. A personal assistant understands what you're trying to achieve, figures out the steps needed, takes actions on your behalf, and adjusts when things don't go as planned.

That's what an agent does.

---

## The Core Idea: A Loop of Reason and Action

At its heart, every agent follows a simple cycle:

1. **Receive a goal** — someone gives the agent a task in plain language
2. **Think** — the agent works out what it needs to do next
3. **Act** — it performs an action (asks a question, looks something up, runs a calculation, calls another system)
4. **Observe** — it sees the result of that action
5. **Repeat** — it thinks again, decides what to do next, and keeps going until the goal is complete

This loop continues until the agent decides the task is done — or until it hits a limit you've set.

A basic agent with no special capabilities at all can still be useful. It can hold a conversation, answer questions, summarise information, and draft text — purely using its built-in language understanding. This is the starting point.

---

## Tools: Giving Agents Capabilities

A plain agent is like a very knowledgeable person locked in a room with no phone, no computer, and no access to the outside world. They can reason well, but they can't look anything up, check the current time, or do anything in the real world.

**Tools** are how you give an agent access to the outside world.

A tool is any capability you attach to an agent. Examples:

- **Look up the weather** for a given city
- **Check the current time** in a timezone
- **Search the web** for up-to-date information
- **Run a calculation**
- **Read or write a file**
- **Send an email or message**
- **Query a database**
- **Call an external API** (a service your company uses)

When an agent needs information it doesn't have, or needs to do something in the real world, it picks the right tool, uses it, gets the result, and carries on.

The agent decides **which tool to use and when** — you don't have to tell it step by step. You just describe the tools available to it and what they do. The agent figures out the rest.

### Built-in vs. Custom Tools

Some platforms come with **built-in tools** that are ready to use out of the box — web search being a common example. You just switch them on.

**Custom tools** are ones you build yourself, specific to your business or workflow. If you want an agent to look up customer records in your CRM, check inventory levels, or submit a support ticket, someone writes a small function that does that, and it becomes a tool the agent can use.

---

## Agents as Tools: Specialists You Can Call On

As tasks become more complex, a single agent with a list of tools can get unwieldy. A better approach is to build **specialist agents** — each one focused on a narrow domain — and let a coordinating agent call on them as needed.

In this model, one agent acts as a kind of **orchestrator or manager**. When it needs something done, instead of doing it itself, it delegates to a specialist:

- "I need the latest news on this topic" → calls the research specialist
- "I need to turn this data into a chart" → calls the data analyst specialist
- "I need to write this up professionally" → calls the writing specialist

From the orchestrator's perspective, each specialist looks just like a tool — it sends a request and gets a result back. The orchestrator doesn't need to know *how* the specialist does its job, only what it's good at.

This keeps each agent simple and focused while allowing the overall system to handle complex, multi-step work.

---

## Multi-Agent Systems: Teams of Agents

When multiple agents work together on shared goals, you have a **multi-agent system**. This introduces a few important concepts:

### Hierarchy

Agents can be arranged in a hierarchy — a parent agent manages child agents. The parent understands the big picture; the children handle the details. The parent can pass work down, collect results, and synthesise them into a final output.

### Shared Context

Agents in a system can share a common memory or state — a kind of shared notepad. One agent writes something down ("I found these five sources"), and another picks it up later without needing to be told directly. This is how results flow from one stage of a workflow to the next.

### Dynamic Delegation

Rather than following a fixed script, a smart orchestrator agent can decide *on the fly* which agent to involve next, based on what's happened so far. This makes the system adaptive — it can handle situations that weren't explicitly anticipated.

---

## Workflow Patterns

Multi-agent systems often follow recognisable patterns. The three most common are:

### Sequential (Pipeline)

Agents work one after another, each building on the previous agent's output.

**Example:** A content pipeline where Agent A researches a topic, Agent B drafts an article based on that research, and Agent C edits and polishes the draft.

Think of it like an assembly line — each station does its job, then passes the work to the next.

### Parallel

Multiple agents work at the same time on independent tasks, and their results are combined at the end.

**Example:** You need a market overview covering five different countries. Five research agents each investigate one country simultaneously, then a synthesis agent merges their findings into a single report.

This is significantly faster than doing it sequentially when the tasks don't depend on each other.

### Loop (Iterative Refinement)

An agent (or group of agents) repeats a cycle until a quality bar is met or a stopping condition is reached.

**Example:** A writing agent produces a draft. A critic agent reviews it and flags issues. A revision agent improves the draft. This cycle repeats until the critic is satisfied, at which point the loop ends and the final output is returned.

This mirrors how humans iteratively refine work — draft, review, improve, repeat.

---

## Callbacks and Guardrails: Staying in Control

As agents become more capable and autonomous, it becomes important to have **oversight mechanisms** — ways to inspect what's happening, intervene when needed, and enforce rules.

**Callbacks** are functions that run automatically at specific moments in the agent's lifecycle. They let you hook into the process without disrupting it. Common points where you might want to intervene:

### Before the agent thinks

You can inspect the request before the AI even starts processing it. This lets you:
- Block certain types of requests entirely
- Modify or sanitise the input
- Log what's coming in for auditing purposes

### After the agent thinks (before it acts)

You can review what the agent is about to say or do, and change or block it if needed. This is a safety net — catch problems before they have real-world effects.

### Before a tool is used

You can intercept a tool call, inspect the arguments the agent is about to pass, and either allow it, modify it, or block it entirely. Useful for enforcing business rules ("never query production data directly") or redirecting requests ("use the approved data source, not that one").

### After a tool returns a result

You can inspect or modify what a tool returns before the agent sees it. Useful for data masking, filtering sensitive information, or enriching results.

### Before or after an entire sub-agent runs

In multi-agent systems, you can wrap an entire specialist agent with logic that decides whether it should run at all, or that transforms its output before it's used.

### Why this matters

Without guardrails, autonomous agents can go off-script, make unintended changes, or expose data they shouldn't. Callbacks give you a structured way to build in safety, compliance, and observability — without having to rewrite the agent's core logic every time a rule changes.

---

## Putting It All Together

Here's how these concepts stack up from simple to sophisticated:

| Complexity | What it looks like |
|---|---|
| Basic agent | Converses and reasons using built-in knowledge only |
| Agent with tools | Can interact with the real world — look things up, take actions |
| Agent using specialist agents | Delegates to focused sub-agents, handles complex compound tasks |
| Multi-agent system | A coordinated team with shared memory, dynamic delegation, and defined roles |
| Workflow-driven system | Structured pipelines — sequential, parallel, or iterative — for reliable, repeatable processes |
| Governed system | All of the above, with callbacks providing safety, oversight, and compliance at every layer |

---

## Key Takeaways

- An agent is not a chatbot. It pursues goals, takes actions, and adapts — not just responds.
- Tools are what give agents real-world capabilities. Without them, an agent is knowledgeable but isolated.
- Specialist agents are a way to manage complexity — divide responsibility, keep each agent focused.
- Multi-agent systems can tackle work that no single agent could handle well on its own.
- Sequential, parallel, and loop patterns are the building blocks of reliable agent workflows.
- Callbacks and guardrails are how you maintain control, enforce rules, and ensure safety as agents become more autonomous.

The underlying AI model — and the specific framework a developer uses to build with it — are implementation details. These concepts apply regardless of which platform or provider is involved.
