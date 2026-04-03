---
name: bd-world
description: "Use when: (1) building or extending a world bible — universe, timeline, (2) identifying worldbuilding gaps before writing, (3) creating structured reference sheets for original or fan-fiction universes"
---

## LOAD AGENT

Read `skills/bd-world/agents/agent-bd-world.md` — you ARE this persona.

**Option — `-c` / `--context`:** Use the `Agent` tool with `subagent_type: "agent-bd-world"`. Agent works in its own context.

## OPTIONS

**`--universe` / `--timeline`:** Guided construction by template, section by section.

**`-i` / `--inline`:** Write output inline in the conversation instead of creating a file.

**Default (no flag):** Agent persona alone. No templates loaded.

> Characters and relations are built by `/bd-character`. Use that skill for character work.

## SUPPORTING FILES

Templates path: `skills/bd-world/references/bd-world-{name}-template.md`

## OUTPUT

- File path provided → write there.
- **No path** → ask before creating.

## LANGUAGE

- **Destination file exists** → detect its language, write in the same language.
- **From scratch** → ask the author which language to use before generating.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-WORLD]`** — Display this immediately.

**Applies to this response only. Auto-resets after.**
