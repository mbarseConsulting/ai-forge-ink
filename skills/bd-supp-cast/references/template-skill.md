---
name: {project}-supp-cast
description: "Supporting cast for {project}. Secondary characters roster with lightweight fiches."
---

# {Project} — Supporting Cast

> Autonomous roster. Use `--add` to create characters, `--evolve {name}` to update them.

## Roster

| Name | Role | Status | Tags |
|------|------|--------|------|

## Adding a character

Use `--add` to create a new supporting character. Guided, one field at a time.

### Fiche template

```markdown
---
name: {character-name}
role: {narrative function — informant, obstacle, mirror, comic relief, etc.}
status: {active / background / exited}
tags: [{optional context tags}]
---

# {Character Name}

**Pronoun:** {he/she/they}
**In one line:** {who they are — not their role, the person}

## Appearance

{2-3 lines. What makes them recognizable. Physical presence, distinctive trait, first impression.}

## Facade / Core

**Facade:** {what they project — the social surface}
**Core:** {who they really are — the crack under the surface}

## Voice

**Register:** {formal / casual / technical / slang — dominant tone}
**Sentence style:** {short and clipped / long and winding / fragmented / other}
**Verbal tic:** {a word, expression, or pattern that marks their speech}
**What they never say:** {avoided words, sidestepped subjects, impossible formulations}
**How they lie:** {omission / redirection / silence / over-explanation / humor}

## Behavior

{How they act. Default mode, under pressure, in group. 2-3 lines max.}

## Key emotion (show-don't-tell)

**Dominant emotion:** {the emotion most often running under the surface}
**How it shows:** {physical signal + behavioral signal — what a camera would see}
**How they mask it:** {what they do to hide it}

## Relationships

| Character | How {name} sees them | The tension |
|-----------|---------------------|-------------|
| {main character} | {perception — from THIS character's perspective} | {what creates friction or dependency} |

## Forbidden

**Never:** {1-2 things that would betray this character}

## Notes

{Anything else the author needs to remember. Sticky-note facts.}
```

Write the fiche to `fiches/{character-slug}.md` and update the roster table.

## Evolving a character

Use `--evolve {name}` to update an existing fiche. Read the current fiche, ask what changed, edit in place. No delta files — secondary characters evolve by direct editing.

If a character outgrows this roster → promote them to a full `/bd-character` skill.

## Loading

### For cast-ink
Read this file (roster) + the fiches of characters present in the scene.

### For puppet-ink
Read the character's fiche. For secondary characters, the fiche is sufficient.

### For write-ink
Read the character's fiche. The Forbidden and Voice sections are the guardrails.

## Promotion

If a secondary character needs full depth (psychology, voice-emotion map, evolution layers, memory):
1. Run `/bd-character` to forge a full character skill
2. Use this fiche as input — it covers the basics
3. Remove the fiche from this roster and update the table
