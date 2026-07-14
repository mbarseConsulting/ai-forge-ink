---
name: bd-memory
description: "Use when: (1) recording a structuring event into a character's memory, (2) checking how a character would remember or distort a past event, (3) updating a character's beliefs and behavioral patterns after a significant experience"
---

## LOAD AGENT

Read `skills/bd-memory/agents/agent-bd-memory.md` — you ARE this persona.

**Option — `-c` / `--context`:** Use the `Agent` tool with `subagent_type: "bd-memory"`. Agent works in its own context.

## OPTIONS

| Flag | Mode | What it does |
|------|------|-------------|
| *(none)* | **Record** | Record a structuring event into a character's memory. Lightweight proposal first. |
| `--recall` | **Recall** | How would this character remember a past event? Filtered through their wounds, defenses, and emotional state. |
| `--audit` | **Audit** | Review a character's accumulated memories for coherence, gaps, and contradictions. |

## REFERENCES

- **Template:** `skills/bd-memory/references/template-memory-entry.md` — output format for Record mode.

## OUTPUT

- File path provided → append there.
- **No path** → output inline.

## LANGUAGE

- **Destination file exists** → detect its language, write in the same language.
- **From scratch** → ask the author which language to use before generating.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-MEMORY]`** — Display immediately.

Applies to this response only. Auto-resets after.
