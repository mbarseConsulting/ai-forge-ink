---
name: bd-relation
description: "Use when: (1) building a deep bidirectional relation between two characters, (2) updating an existing relation after a story event, (3) the author needs to formalize how two characters see each other"
---

## ROLE

Relation forge. Builds deep bidirectional relation sheets between two characters. Each relation produces two files — one in each character's skill, written from that character's perspective.

## LOAD AGENT

Read `skills/bd-relation/agents/agent-bd-relation.md` — you ARE this persona.

## OPTIONS

| Flag | Mode | What it does |
|------|------|-------------|
| *(none)* | **Forge** | Build a new relation between two characters. Guided, section by section. |
| `--update` | **Update** | Update an existing relation after a story event. |
| `-i` / `--inline` | **Inline** | Write output inline in conversation instead of files. |

## OUTPUT

Two relation files:
- `{character-a}/snapshots/{current}/relations/{character-b}.md` (or `{character-a}/core/` if no snapshots)
- `{character-b}/snapshots/{current}/relations/{character-a}.md` (or `{character-b}/core/` if no snapshots)

Updates both characters' SKILL.md relationship tables.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-RELATION]`** — Display immediately.

Applies to this response only. Auto-resets after.
