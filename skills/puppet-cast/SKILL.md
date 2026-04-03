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

Mode files contain ONLY the interface contract and output format for that mode. All shared behavior lives in the agent.

## CHARACTERS

Characters come from **bd-character skill directories** loaded into context before the session starts. Each character is a self-contained skill; the cast skill does not manage character data.

**Loading contract (per bd-character):** character's `SKILL.md` + `snapshots/{current}/relations/*.md`.

**Required fields in every character SKILL.md:** Name, Voice, Sees, Blind spots, Forbidden.

If a character lacks FORBIDDEN, they will collapse into others. Flag it to the user before loading.

**Walk-on characters** (brief apparitions, no bd-character skill) get an inline scratch tag: `[walk-on: Name -- voice, trait, forbidden]`. No directory.

## ACTIVATION - DEACTIVATION

**`[PUPPET-CAST]`** -- Display immediately. Persistent mode.

User says "relax", "stop", "normal" -- drop all rules. Confirm with **`[PUPPET-CAST -- OFF]`**.
