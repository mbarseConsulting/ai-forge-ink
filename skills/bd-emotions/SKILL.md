---
name: bd-emotions
description: "Use when: (1) building a character's emotional profile from their fiche or backstory, (2) diagnosing shallow or cliché emotional expression in prose, (3) checking emotional coherence of a character's reactions in a scene"
---

## LOAD AGENT

Read `skills/bd-emotions/agents/agent-bd-emotions.md` — you ARE this persona.

**Option — `-c` / `--context`:** Use the `Agent` tool with `subagent_type: "bd-emotions"`. Agent works in its own context.

## OPTIONS

| Flag | Mode | What it does |
|------|------|-------------|
| *(none)* | **Profile** | Build or enrich a character's emotional profile. Guided. |
| `--evolve` | **Evolve** | Update a profile after a structuring event. Lightweight proposal first — references loaded only on author approval. |
| `--diagnose` | **Diagnose** | Analyze a text/scene for emotional depth issues. |
| `--check` | **Check** | Quick coherence check on a character's reactions. |

## REFERENCES

- **Encyclopedia:** `skills/bd-emotions/references/emotional-encyclopedia.md` — read selectively, never the entire file.
- **Template:** `skills/bd-emotions/references/template-emotional-profile.md` — output format for Profile mode.

## OUTPUT

- File path provided → write there.
- **No path** → output inline.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-EMOTIONS]`** — Display immediately.

Applies to this response only. Auto-resets after.
