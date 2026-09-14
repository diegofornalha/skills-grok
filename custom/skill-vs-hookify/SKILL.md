---
name: skill-vs-hookify
description: >-
  Use this when deciding whether something should be a Skill or a Hookify hook,
  or when the user is confused about skill vs hookify.
---
# Skill vs Hookify — when to use which

## One-line difference
- **Skill** = playbook the agent *reads and follows* when the task matches (“how we do X”).
- **Hookify hook** = automatic brake that *fires on tool use* matching a pattern (“stop/warn if X happens”), without waiting for the agent to remember.

The hookify **plugin** includes both: a skill to *write* rules (`writing-hookify-rules`) and **hooks** that *enforce* those rules.

## Use a Skill when
- You want a repeatable multi-step workflow (publish app, triage inbox, release checklist).
- The agent should choose tools and adapt (“do the job”).
- You’re capturing a standard like “IP/localhost → HTTPS subdomain”.
- You need explanation, steps, and anti-patterns — not a hard block.

Examples: `ip-com-subdominio-https`, inventário de skills, onboarding de domínio.

## Use a Hookify rule (hook) when
- You need a **guardrail** that runs even if the agent is about to do the wrong thing.
- The trigger is a **concrete pattern**: `rm`, edit `.env`, `console.log`, dangerous deploy command.
- You want **warn** or **block** at PreToolUse / file edit / stop — not a tutorial.
- The user said “never do X without asking” and X can be matched by regex/path.

Examples: confirm before delete; block `rm -rf`; warn on `.env` edits.

## Decision checklist
1. Is the goal “teach/do a workflow”? → **Skill**
2. Is the goal “automatically stop or warn on a bad action”? → **Hookify rule**
3. Need both? Common pattern:
   - Skill documents the policy and how to set it up
   - Hookify rule enforces the dangerous edge (delete, secrets, prod)
4. Still unsure? Prefer **Skill** for process; add **Hookify** only for the risky verb (delete, force-push, secrets).

## What NOT to confuse
| | Skill | Hookify hook |
|---|---|---|
| Triggers | Agent decides it applies | Tool event matches pattern |
| Feels like | Recipe / SOP | Seatbelt |
| Stored as | `SKILL.md` / workflows | `.claude/hookify.*.local.md` |
| Good for | “How we publish” | “Don’t delete without OK” |
| Bad for | Hard-blocking `rm` alone | Long multi-step publishing guide |

## Inventory helpers (for humans)
- Agent **Skills** → list skills inventory
- Agent **Hookify** → list hookify rules and explain skill vs hook

## When the user asks “should this be a skill or a hook?”
Answer with:
1. Goal in one sentence
2. Skill / Hook / Both
3. If Both: what the skill covers vs what the hook blocks
4. Offer to create the missing piece
