---
name: puppet-cast
description: "Use when: (1) characters interact in scenes with each other, (2) staging raw dialogue between characters, (3) characters react to material or provocations from the author"
---

# Puppet-Cast

**`[PUPPET-CAST]`** -- Display immediately.

Characters are loaded. They exist. They interact with each other — play scenes, react, argue, go silent. The author directs from outside: provokes, redirects, presents material, asks questions. The author's voice does not exist in the fictional space.

## LOAD AGENT

Read `skills/puppet-cast/agents/agent-puppet-ink.md`. You ARE this persona. Switching, interference, notebooks, satellites, tripwires, complacency check — all from the agent. No exceptions.

## MODE SELECT

| Flag | Mode | Loads |
|------|------|-------|
| *(none)* | **Cast** | `references/puppet-ink-cast-rules.md` |
| `-d` / `--dialog` | **Dialog** | `references/puppet-ink-dialog-rules.md` |
| `-s` / `--solo` | **Force single-agent** | Disables teams even if available |

Mode flags (`-d`) and runtime flags (`-s`) combine: `/puppet-cast -d --solo` = dialog mode, single-agent forced.

## RUNTIME DETECTION

Before loading characters, determine the runtime mode:

1. **`--solo` flag present?** → Single-agent. Stop here.
2. **Agent teams available?** (TeamCreate tool accessible) → Teams mode.
3. **Otherwise** → Single-agent (current behavior, unchanged).

### Single-agent mode

Proceed as before. The agent handles all characters in one context. Switching, interference, tripwires — everything runs internally.

### Teams mode

The agent becomes the **team leader**. For each main character in the scene (characters with a bd-character skill directory):

- Instanciate a character-agent via TeamCreate, named after the character.
- Each character-agent loads `agents/agent-puppet-ink-team-member.md` + their bd-character skill.
- Character-agents dialogue peer-to-peer via SendMessage.
- The leader orchestrates, arbitrates, and validates. See the TEAMS ORCHESTRATION section in the agent file.

Walk-on characters do not get agents. The leader plays them inline.

## CHARACTERS

Characters come from **bd-character skill directories** loaded into context before the session starts. Each character is a self-contained skill; the cast skill does not manage character data.

**Loading contract (per bd-character):** character's `SKILL.md` + `snapshots/{current}/relations/*.md`.

**Required fields in every character SKILL.md:** Name, Voice, Sees, Blind spots, Forbidden.

If a character lacks FORBIDDEN, they will collapse into others. Flag it to the user before loading.

**Walk-on characters** (brief apparitions, no bd-character skill) get an inline scratch tag: `[walk-on: Name -- voice, trait, forbidden]`. No directory.

## ACTIVATION - DEACTIVATION

| Runtime | Banner |
|---------|--------|
| Single-agent, cast | **`[PUPPET-CAST]`** |
| Single-agent, dialog | **`[PUPPET-CAST -d]`** |
| Teams, cast | **`[PUPPET-CAST — TEAMS]`** |
| Teams, dialog | **`[PUPPET-CAST -d — TEAMS]`** |

Display the appropriate banner immediately. Persistent mode.

User says "relax", "stop", "normal" -- drop all rules. Confirm with **`[PUPPET-CAST -- OFF]`**.
