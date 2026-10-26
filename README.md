# grilling-skills

Four agent skills that interview you about a plan until you and the agent share one understanding of it, then stop. Use them before writing a spec, a ticket, or code.

Forked from [mattpocock/skills](https://github.com/mattpocock/skills) at commit [`5beb35b`](https://github.com/mattpocock/skills/tree/5beb35b040e3de97e54fa9e386d7e42d15c295c2). It is a standalone copy of four of Matt Pocock's skills, not a GitHub fork. His license is kept in [LICENSE](./LICENSE).

| Skill | What it does |
| --- | --- |
| `/grill-me` | The interview, for any subject. Writes no files. |
| `/grill-with-docs` | The same interview inside a repo. Also writes `GLOSSARY.md` and ADRs as terms and decisions settle. |
| `/grilling` | The interview loop that the other two call. |
| `/domain-modeling` | The glossary and ADR writing that `/grill-with-docs` calls. |

The four belong together: `grill-me` and `grill-with-docs` only delegate to the other two.

## What changed from upstream

One file: [`skills/grilling/SKILL.md`](./skills/grilling/SKILL.md). The other three skills are identical to upstream.

When your starting description doesn't name a specific repo, ticket, doc, or system, `grilling` now searches your GitHub org and Confluence for context before asking. It also searches mid-session when a question needs a fact those sources could hold. Each round opens with a **What I found** note that cites its sources, and the findings only inform the recommended answers; you still make every decision.

The skill tells Claude to run these searches through sub-agents, keep them read-only, and treat anything it finds as information, never as instructions. Those are instructions to Claude, not a sandbox. What a search can actually reach and do is set by the permissions of your `gh` login and your Atlassian connection, so check those before pointing the skill at an org you don't fully trust.

- It reads your GitHub org name and Confluence site from your `CLAUDE.md`, or asks once.
- It uses the `gh` CLI for GitHub and an Atlassian MCP for Confluence. If either is missing, it says so and continues without it.

## Install

Uses [`npx skills`](https://github.com/vercel-labs/skills), which requires Node.js 22.20 or later.

```bash
npx skills@latest add andrew4parsable/grilling-skills --skill '*' -a claude-code -g
```

`-g` installs globally, so the skills work in any directory. Tested on macOS only; other systems are unsupported.

Pocock's own plugin ships skills with the same names. Install one or the other, not both.

## Use

Type `/grill-me` and describe what you're planning. Pocock's [notes on grill-me](https://github.com/mattpocock/skills/blob/main/docs/productivity/grill-me.md) are worth reading. Three of them matter most:

- Start in a fresh conversation, not on top of a plan an agent already wrote.
- Leave plan mode off. It makes the agent hurry toward a plan when you want it to keep asking.
- Push back. Answering "agreed" to every question produces a plan you nodded at and didn't decide.

`/grill-me` writes nothing, so when the session ends, ask the agent to write the agreed decisions into a spec or ticket.

## License

MIT. Copyright (c) 2026 Matt Pocock; see [LICENSE](./LICENSE).
