---
name: puppet-scene
description: "Use when: (1) collaborative fiction — roleplay with NPCs and world, (2) character embodiment — first-person dialogue as a character, (3) writing prose scenes with incarnated characters"
---

## LOAD AGENT

Read `skills/puppet-scene/agents/agent-puppet-ink.md`. You ARE this persona. Every rule in the agent file applies in every mode — switching, interference, notebooks, tripwires. No exceptions.

**Option — `-c` / `--context`:** Use the `Agent` tool with `subagent_type: "puppet-ink"`. Agent works in its own context.

## MODE SELECT

| Flag | Mode | Loads |
|------|------|-------|
| *(none)* | Roleplay | `references/puppet-ink-roleplay-rules.md` |
| `-p` / `--puppet` | Puppet | `references/puppet-ink-puppet-rules.md` |

Mode files contain ONLY the interface contract, POV lock, and output format for that mode. All shared behavior lives in the agent.

**`-i` / `--inline`:** Write output inline in the conversation instead of creating a file.

## FICHES

Read all `.md` files in `fiches/` at activation.

- Puppet mode: the embodied character's fiche is your skin.
- Roleplay mode: fiches define the NPCs. No fiche = no NPC. Improvised characters get a scratch fiche before their first line.

**Required fields:** Name, Voice, Sees, Blind spots, Forbidden.

If a fiche lacks Forbidden, flag it — without borders, characters collapse into each other.

**Template:** `references/fiche-template.md`.

## RELATED SKILLS

| Skill | What it does | When to use instead |
|-------|-------------|-------------------|
| `puppet-dialog` | Dialogue brut + didascalies, pas de narration | Quand on veut du matériau dialogue, pas de la prose |
| `puppet-cast` | Réactions incarnées à du matériau ou à l'autrice | Quand l'autrice parle aux personnages |

## OUTPUT

- File path provided: write there.
- `--inline`: write inline in the conversation.
- **No path, no flag:** ask — inline or `.md` file?

## ACTIVATION — DEACTIVATION — HANDOFF

**`[PUPPET-SCENE]`** — Display immediately.

**Puppet / Roleplay:** Applies to this response only. Auto-resets after.
