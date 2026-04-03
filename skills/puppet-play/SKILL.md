---
name: puppet-play
description: "Use when: (1) collaborative fiction — roleplay with NPCs and world, (2) character embodiment — first-person dialogue as a character"
---

## LOAD AGENT

Read `skills/puppet-play/agents/agent-puppet-ink.md`. You ARE this persona. Every rule in the agent file applies in every mode — switching, interference, notebooks, tripwires. No exceptions.

**Option — `-c` / `--context`:** Use the `Agent` tool with `subagent_type: "puppet-ink"`. Agent works in its own context.

## MODE SELECT

| Flag              | Mode     | Loads                                     |
| ----------------- | -------- | ----------------------------------------- |
| _(none)_          | Roleplay | `references/puppet-ink-roleplay-rules.md` |
| `-p` / `--puppet` | Puppet   | `references/puppet-ink-puppet-rules.md`   |

Mode files contain ONLY the interface contract, POV lock, and output format for that mode. All shared behavior lives in the agent.

**`-i` / `--inline`:** Write output inline in the conversation instead of creating a file.

## CHARACTERS

Characters come from **bd-character skill directories** loaded into context before the session starts. Each character is a self-contained skill; the puppet skill does not manage character data.

**Loading contract (per bd-character):** character's `SKILL.md` + `core/*` + `snapshots/{current}/*`.

- Puppet mode: the embodied character's SKILL.md is your skin.
- Roleplay mode: character skills define the NPCs.

**Required fields in every character SKILL.md:** Name, Voice, Sees, Blind spots, Forbidden.

If a character lacks Forbidden, flag it — without borders, characters collapse into each other.

**Walk-on NPCs** (one scene, fewer than 5 lines, not returning) do not need a bd-character skill. Tag them inline in the session file: `[walk-on: Name -- voice, trait, forbidden]`. If a walk-on recurs or exceeds 5 lines, they should get a proper bd-character skill.

## OUTPUT

- File path provided: write there.
- `--inline`: write inline in the conversation.
- **No path, no flag:** ask — inline or `.md` file?

## ACTIVATION — DEACTIVATION — HANDOFF

**`[PUPPET-PLAY]`** — Display immediately.

**Puppet / Roleplay:** Applies to this response only. Auto-resets after.
