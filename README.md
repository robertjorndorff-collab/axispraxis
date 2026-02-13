# AXIS PRAXIS

### A Governing Constitution for AI-Assisted Software Development

> *"Silent failures are load-bearing walls you can't see. Before you remove one, understand what it's holding up."*

---

**TL;DR:** Drop a `CLAUDE.md` in your repo root. Every AI agent reads it before writing a single line of code. Every rule in it was written because something broke in production.

---

## What This Is

The Axis Praxis Constitution is a governance framework for teams building software with AI agents (Claude Code, Cursor, Copilot, Windsurf, Aider — any of them). It defines chain of command, code quality law, testing obligations, database governance, debugging hierarchy, known AI failure modes, and a prohibited actions list.

It is not a style guide. It is not a suggestion. It is law for your AI agents.

One human stays in charge.

## What It Covers

| Article | Subject |
|---------|---------|
| I | Chain of Command — sovereignty, role separation, escalation |
| II | Doctrine of Deliberate Action — mandatory planning, impact analysis |
| III | Code Quality Amendments — silent failure prohibition, response verification |
| IV | Build and Deploy Discipline — commit verification, deploy monitoring |
| V | Testing and Quality Assurance — human-is-not-QA principle |
| VI | Critical Path Protection — registries, compound change review |
| VII | Diagnosis and Investigation — evidence-first doctrine, three strikes rule, Shainin's Red X |
| VIII | Database and Migration Governance — read-write separation |
| IX | Tools and Automation — skills are mandatory |
| X | Known AI Failure Modes — documented production incidents |
| XI | Prohibited Actions — the 14 nevers |
| XII | Amendment Process — grows only through failure |
| XIII | Purpose and Jurisdiction — respect the scar tissue |

## Quick Start

### Option 1: Copy the template (fastest)

1. Copy [`CLAUDE.md`](CLAUDE.md) into your repo root
2. Fill in the `[BRACKETED]` values in the Project Configuration section
3. Commit it
4. Every AI session starts by reading it

### Option 2: Fork this repo

1. Fork `axispraxis/constitution`
2. Edit the Project Configuration section in `CLAUDE.md`
3. Delete this `README.md` or keep it — your call

### Option 3: Use the Setup Wizard

If you have a Claude account, the [AXIS PRAXIS Setup Wizard](https://claude.ai/share/e4ac36fe-e841-4c48-95f5-4375ff0c0dee) interviews you about your stack, repo, and AI tools, then generates a complete `CLAUDE.md` tailored to your project.

## How It Works

The `CLAUDE.md` file has two sections:

**1. Project Configuration** (you customize this)
- Your stack, repo, build commands
- Your agent roster — which AI tools, which roles
- Your critical paths and forbidden commands
- Your MCP servers

**2. The Constitution** (you don't touch this)
- 13 articles of governance law
- Universal rules that apply to any stack, any AI provider, any team size
- Amendment log for your project-specific additions

AI agents read the whole file at session start. The configuration tells them where they are. The Constitution tells them how to behave.

## Team Structure

The Constitution defines three roles. Your team can have any number of agents in any role — scale is unlimited, but separation of concerns is absolute:

| Role | Can Do | Cannot Do |
|------|--------|-----------|
| **Coding Agent** | Write, modify, commit code | Make product decisions |
| **Advisory Agent** | Read code, diagnose, write specs | Write production code |
| **Strategic Agent** | Analyze, recommend, counsel | Access filesystem |

The number of agents grows; the walls between roles do not move.

## The Three Rules That Matter Most

If you read nothing else:

1. **§3.1 — The Silent Failure Prohibition.** Every error handler shall handle or log. No empty catch blocks. Ever.

2. **§5.1 — The Human-Is-Not-QA Principle.** The AI ships working code. The human evaluates whether it's the *right* code. The human does not find your bugs for you.

3. **§7.3 — The Three Strikes Escalation Rule.** Three failed attempts at the same fix? Stop writing code. Escalate. The Coding Agent is an executor, not a theorist.

## Amendment Process

The Constitution is a living document. It grows only through failure.

- Any production incident may give rise to a new amendment
- Amendments are proposed by any agent, ratified only by the human
- Each amendment cites the incident that necessitated it
- Amendments are append-only — nothing gets deleted

Add project-specific amendments to the table at the bottom of your `CLAUDE.md`.

## FAQ

**Does this work with [insert AI tool]?**
Yes. The Constitution is tool-agnostic. If it writes code, it's a Coding Agent. If it advises, it's an Advisory Agent. The roles map to any AI tool.

**Is this overkill for a solo developer?**
No. Solo developers with AI agents are the *primary* audience. You're the Human Principal. Your AI is the team. You need governance more than anyone because there's no one else catching mistakes.

**Can I modify the Constitution?**
Add to it via amendments. Don't remove articles — supersede them. The history matters.

**Why "Constitution" and not "guidelines"?**
Guidelines get ignored. Laws get followed. Every rule here was written because a guideline wasn't enough.

## License

MIT. Use it, fork it, adapt it. Attribution appreciated but not required.

## Origin

Every clause was written in response to a real failure. Respect the scar tissue.

Built by [Axis Praxis](https://www.axispraxis.ai).
