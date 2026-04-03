---
name: {character-name}
description: "{one line — who this character is, not what they do}"
---

# {Character Name}

> Active portrait. This IS the character as they exist right now.
> Rewritten when a new snapshot is created.
> **Provenance:** Synthesized {date} | From core + snapshot {number or "baseline"} | Modified by {agent/author}
> **Freshness:** Snapshot {number} — {label} | If index.md shows a higher number, this portrait is STALE and must be resynthesized before use.

---

## Identity

- **Name:** {full name}
- **Pronoun:** {he/she/they}
- **In one line:** {who this person is}
- **Born:** {date or period}
- **Status:** {current narrative position}
- **Identity stability:** {stable / fluid / fractured / performed — from core}

---

## Current psychological state

{3-5 sentences. Where this character is RIGHT NOW. Structure:}
1. {Which wound is active and how it manifests currently}
2. {What lie is running and whether it is reinforced or cracking}
3. {What they want right now — may differ from core want if snapshot shifted it}
4. {Which defenses are up and which are compromised}
5. {The central tension: what is pulling them in two directions}

{If no snapshot exists: write this as the baseline psychological configuration from core — wound dormant, lie unchallenged, defenses at default.}

---

## Voice (current)

{How they speak right now. Minimum requirements:}
- **Register:** {current register — may differ from core baseline if snapshot shifted it}
- **Signature markers:** {3 concrete speech patterns — phrases, structures, tics}
- **First thing that shifts under emotion:** {what changes first when they lose composure — speed? volume? vocabulary? silence?}

---

## Sees / Blind spots

**Sees:** {what this character notices that others miss — specify the perceptual domain: social cues? physical details? emotional undercurrents? threat vectors?}
**Blind spots:** {what they cannot or will not see — especially about themselves. Specify: is this a "cannot" (structural) or "will not" (defensive)?}

---

## Body (current)

{How this character currently inhabits their body. One line each:}
- **Physical state:** {any changes from baseline — injuries, exhaustion, transformation}
- **Relationship to own body:** {from core — or delta if shifted}
- **What the body carries:** {somatic residue from significant events — tension patterns, flinch triggers, comfort zones}

---

## Key relationships (current)

| Character | How {name} sees them now | The unspoken | Tension vector |
|-----------|------------------------|--------------|----------------|
| {name} | {current perception} | {what is not being said} | {what could break or deepen this — the direction of instability} |

---

## Forbidden

**ONLY {name} does:**
- {thing unique to this character — if another character did this, it would feel wrong}

**{name} NEVER:**
- {thing that would betray this character — the violation a reader would catch}

---

## Loading

**Current snapshot:** {number} — {label} (or "baseline — no snapshots yet")

### Information loss warning

This portrait is a COMPRESSION. The following information exists in full only in the source files:
- Full psychology chain (wound -> lie -> want -> need): `core/core.md` section 5
- Complete behavior patterns: `core/core.md` section 6
- Full voice baseline: `core/core.md` section 7
- Writing rules (always/never/traps/deformation): `core/writing-rules.md`
- Memory entries: `snapshots/{current}/memory/`
- Full relation files: `snapshots/{current}/relations/`

### For cast-ink
Read this file + relevant `snapshots/{current}/relations/*.md`.
**What you get:** enough to voice the character in dialogue and react to events.
**What you lack:** deep psychology, full behavior patterns, writing rules. Sufficient for ensemble scenes. Insufficient for psychologically complex solo scenes.

### For puppet-ink
Read this file + `core/*` + `snapshots/{current}/*`.
**What you get:** the complete character.
**What you lack:** nothing — this is the full load.

### For write-ink
Read this file + `core/writing-rules.md`.
**What you get:** current state + guardrails for prose.
**What you lack:** full psychology, memories. Sufficient for scene writing. For psychologically pivotal scenes, also load `core/core.md` sections 4-5.

### Specific moment
Consult `index.md`, then read `core/` + `snapshots/{number}/`.

---

## Synthesis checklist

- [ ] Psychological state traces to core wound/lie/want/need — no orphan claims
- [ ] Voice markers match current snapshot (not stale baseline if snapshot exists)
- [ ] Relationships table matches current snapshot relations/ directory
- [ ] Forbidden items are unique to this character (not generic)
- [ ] Loading instructions reference correct current snapshot number
- [ ] Freshness header matches index.md current snapshot
