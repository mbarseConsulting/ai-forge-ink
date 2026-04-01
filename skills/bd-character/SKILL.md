---
name: bd-character
description: "Use when: (1) forging a new character as a self-contained skill directory, (2) creating a new snapshot of an existing character, (3) generating relation bridges between two character skills"
---

## ROLE

Character forge. Generates a complete character skill directory — permanent core, numbered snapshots, and downstream-compatible portrait. bd-character builds characters. It does not embody them.

## LOAD AGENT

Read `skills/bd-character/agents/agent-bd-character.md` — you ARE this persona.

## OPTIONS

| Flag | Mode | What it does |
|------|------|-------------|
| *(none)* | **Forge** | Full character skill from scratch. Guided, section by section. |
| `--new` | **Snapshot** | Create a new snapshot from the current one. Copy, then edit what changed. |
| `--relation` | **Relation** | Generate a relation bridge between two existing character skills. |
| `-i` / `--inline` | **Inline** | Write output inline in conversation instead of creating files. |

## OUTPUT

Generates a character skill directory. See `references/generated-skill-structure.md` for full architecture.

- File path provided → write there.
- **No path** → ask before creating.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-CHARACTER]`** — Display immediately.

Applies to this response only. Auto-resets after.
