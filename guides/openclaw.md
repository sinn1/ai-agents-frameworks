---
title: How OpenClaw Works
---

*How the concepts behind AI agents show up in OpenClaw — a plain-language walkthrough.*

If you haven't read [How AI Agents Work](how-agents-work) yet, start there. This guide takes those same ideas and shows exactly where you'll find them in OpenClaw.

---

## What OpenClaw Is

OpenClaw is a personal AI assistant that runs on your own devices. You install it on your own hardware — a laptop, a home server, a phone — and it stays there. Your data doesn't pass through anyone else's servers.

It connects to the messaging apps you already use (WhatsApp, Telegram, Slack, Discord, iMessage, and others), so you interact with your assistant through whichever channel you prefer, rather than having to open a dedicated app.

---

## The Agent at the Centre

Recall the core idea from the previous guide: an agent runs a continuous loop — receive a goal, think, act, observe the result, think again, and keep going until the task is done.

In OpenClaw, this loop is handled by the **Pi agent framework**, running in what's called RPC mode. RPC stands for Remote Procedure Call — a technical term for "the agent can ask other parts of the system to do things on its behalf and get results back." In plain terms: the agent can reach out, get information, take actions, and carry on — exactly the loop described earlier.

You don't configure this loop yourself. It's built into OpenClaw. You interact with the result.

---

## The Gateway: OpenClaw's Control Room

Every message you send — whether through WhatsApp, Slack, or the command line — arrives at the same place: the **Gateway Control Plane**.

The Gateway is a local service running on your device. It:

- Receives messages from all your connected channels
- Manages your sessions (which conversation is which)
- Routes requests to the agent
- Sends responses back to the right channel

Because the Gateway runs locally, nothing leaves your device unless you've explicitly connected it to an external service. The Gateway is the reason OpenClaw can feel like a single assistant across multiple platforms — everything flows through one point.

---

## Skills: OpenClaw's Version of Tools

The previous guide explained that tools are how you give an agent real-world capabilities. Without tools, an agent is isolated — it can reason, but it can't look anything up, check live data, or take action outside the conversation.

In OpenClaw, tools are called **Skills**.

A skill is a packaged capability that the agent can call on during a conversation. Examples of what skills can do:

- Search the web for current information
- Read and write files on your device
- Control a browser to interact with websites
- Send a message on your behalf through a connected channel
- Integrate with apps and services you use

### ClawHub: The Skills Registry

OpenClaw has a built-in registry called **ClawHub** where skills are listed and managed. When the agent decides it needs a capability it doesn't currently have, it can discover and load the right skill automatically — without you having to manually configure anything.

Skills can be:
- **Bundled** — included with OpenClaw out of the box
- **Managed** — maintained and updated through ClawHub
- **Workspace-specific** — custom skills you've added for a particular context

This maps directly to the distinction in the earlier guide between built-in tools (ready immediately) and custom tools (built for specific needs).

---

## Multi-Agent Routing: Specialists in OpenClaw

The earlier guide introduced the idea of specialist agents — focused sub-agents that a coordinating agent can call on when needed. OpenClaw implements this through **multi-agent routing**.

Each agent in OpenClaw can operate in its own **isolated workspace** with its own session. The main agent can delegate to these specialists, get results back, and synthesise them — without the specialists needing to know anything about each other.

From a practical standpoint, this means you can have different agents set up for different purposes — one for research, one for writing, one for managing your calendar — and the system coordinates between them without you having to manually switch between them.

---

## Channels: Where You Meet the Agent

One of OpenClaw's distinctive features is that the agent meets you where you already are.

Rather than requiring a dedicated interface, OpenClaw connects to the messaging platforms you use daily. You send a message in WhatsApp or Slack, and your OpenClaw agent responds — just like a colleague would.

Behind the scenes, the Gateway maps each channel to the same underlying agent session. The channel is just the surface; the intelligence is the same wherever you connect.

Supported channels include WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, and Matrix, among others.

---

## Voice and Canvas: Beyond Text

OpenClaw extends the standard text-based agent interaction in two directions:

**Voice** — OpenClaw supports wake-word detection and a Talk Mode for continuous conversation. This turns the agent into something closer to a voice assistant, useful when you're away from a keyboard.

**Canvas** — A visual workspace where the agent can build and display structured interfaces — not just send text replies, but present information visually, work through documents collaboratively, or display results in a richer format.

Both are extensions of the same underlying agent — the same loop, the same skills, just different surfaces for interaction.

---

## Local-First: What It Means in Practice

"Local-first" is OpenClaw's most significant architectural choice. Everything — the Gateway, the agent runtime, your conversation history, your skills — runs on your own hardware.

This has practical implications:

- **Privacy** — your conversations and data don't transit external servers
- **Control** — you decide what the agent can access
- **Reliability** — the system works even without internet access, for capabilities that don't require it

It also means OpenClaw behaves like the governed systems described in the earlier guide. Because you're running the infrastructure, you have full visibility into what the agent is doing and can configure guardrails at every layer.

---

## Putting the Concepts Together

| Concept from the previous guide | How it appears in OpenClaw |
| --- | --- |
| The reason-and-act loop | Pi agent framework in RPC mode |
| Tools | Skills, managed through ClawHub |
| Built-in vs. custom tools | Bundled/managed skills vs. workspace-specific skills |
| Specialist agents | Multi-agent routing with isolated workspaces |
| Control and guardrails | Local-first architecture; you own the infrastructure |
| Channels | WhatsApp, Slack, Telegram, iMessage, and others via the Gateway |

---

OpenClaw is a concrete example of how the abstract ideas behind agents — loops, tools, specialists, guardrails — show up in a real, deployable system. The concepts don't change; only the names and the interfaces do.
