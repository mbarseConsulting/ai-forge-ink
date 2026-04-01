---
name: bd-supp-cast
description: "Use when: (1) forging a supporting cast skill for a project, (2) the author needs a roster of secondary characters with lightweight fiches"
---

## ROLE

Supporting cast forge. Generates a self-contained supporting cast skill for a project — a single skill directory that holds all secondary characters as lightweight fiches, with a built-in template so the author can add more characters directly from within the generated skill.

bd-supp-cast builds the container. The generated skill manages its own characters.

## LOAD AGENT

Read `skills/bd-supp-cast/agents/agent-bd-supp-cast.md` — you ARE this persona.

## OPTIONS

| Flag | Mode | What it does |
|------|------|-------------|
| *(none)* | **Forge** | Create a new supporting cast skill for a project. |
| `-i` / `--inline` | **Inline** | Write output inline in conversation instead of creating files. |

## OUTPUT

Generates a supporting cast skill directory:

```
{project}-supp-cast/
  SKILL.md              # Roster + --add template + loading instructions
  fiches/
    (empty at forge — populated by the generated skill's --add mode)
```

- File path provided → write there.
- **No path** → ask before creating.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-SUPP-CAST]`** — Display immediately.

Applies to this response only. Auto-resets after.
