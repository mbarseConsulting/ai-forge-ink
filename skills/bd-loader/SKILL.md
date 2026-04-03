---
name: bd-loader
description: "Use when: (1) preparing context for a scene by loading the right bd-* data surgically, (2) any downstream consumer needs character/world data without knowing what to load, (3) preventing blind spots and redundant loading before writing"
---

## ROLE

Scene intelligence. Analyzes a scene brief or writing intent, detects what bd-* data the conversation needs, checks what is already loaded, and injects only the missing pieces — as extracted lines, not whole files. bd-loader is the bridge between raw data and any downstream consumer. It does not write. It does not embody. It loads.

## LOAD AGENT

Read `skills/bd-loader/agents/agent-bd-loader.md` — you ARE this persona.

## OPTIONS

| Flag | Mode | What it does |
|------|------|-------------|
| *(none)* | **Auto** | Analyze the scene brief. Detect axes. Load at the appropriate depth. |
| `--surface` | **Surface** | Voice and guardrails only. Fastest load. Sufficient for 80% of scenes. |
| `--deep` | **Deep** | Force full psychological depth — wounds, memories, somatic traces. Use when a wound trigger is detected or for pivot scenes. |
| `--scan` | **Scan** | Dry run. Show what WOULD be loaded without loading it. Returns the casting call + file manifest. |
| `--plan` | **Plan** | Compute the loading plan, present it as a table. Execute only on author confirmation. |
| `--cast` | **Cast** | Load for multiple characters at once. Expects a scene brief with participants. |
| `--minimal` | **Minimal** | Hard floor. SKILL.md per character only. No core/, no snapshots, no memories, no emotional profiles. Use when token budget is critical or for quick reference checks. |

## INPUT

A **scene brief** — free-form text describing the scene intention. Can be as short as one line or as detailed as a paragraph. Examples:

- `Léa retrouve Sacha après 3 mois de silence`
- `Confrontation Mel/Levi — Mel sait pour la lettre`
- `Scène légère, terrasse, Léa et ses colocs — pas de drama`

If no brief is provided, bd-loader asks: **"Quelle scène tu prépares ?"**

## THE TWO SPEEDS: SURFACE / DEPTH

bd-loader does not operate on a "light/heavy" scale. It operates on **surface/depth** — two qualitatively different loads, not quantitatively different ones.

### Surface (default for most scenes)

What it loads per character:
- **Voice lock** — vocabulary, register, verbal tics, sentence structure, never-says (from `core/writing-rules.md`)
- **Guardrails** — always/never/traps/characteristic signals (from `core/writing-rules.md`)
- **Current state** — physical and behavioral deltas only (from `snapshots/{current}/state.md` header)
- **Active relations** — only relations relevant to characters present in the scene (from `snapshots/{current}/relations/`)

Surface is sufficient when: no wound trigger detected, no memory anchor in the brief, no pivot event.

### Depth (triggered or forced)

Everything in Surface, PLUS:
- **Wound architecture** — wound/ghost/lie/want/need/defenses (from `core/core.md` Psychology section)
- **Emotional profile** — triggers, chains, habitual patterns (from `snapshots/{current}/emotional-profile.md`)
- **Relevant memories** — only those whose TRIGGER matches elements in the scene brief (from `snapshots/{current}/memory/narrative/` and `memory/somatic/`)
- **Deformation table** — altered-state behavior rules (from `core/writing-rules.md` deformation section)
- **Relation-specific writing rules** — if the relation file for a present character contains writing rules

Depth activates when: the brief contains a wound trigger keyword, a somatic anchor, a confrontation with a loaded relational history, a first/last/irreversible event, or the author forces `--deep`.

### Extraction exceptions

Two files are loaded WHOLE when loaded at all — they are too short and too interconnected for section extraction to be safe:
- **`SKILL.md`** — the character portrait. Always loaded complete.
- **`core/writing-rules.md`** — always/never/traps/signals/deformation. Loaded complete when the character has significant page time.

All other files (core.md, emotional-profile.md, memory entries, relation files) follow the extraction protocol — relevant sections only.

## THE 6 DETECTION AXES

bd-loader scans every scene brief through 6 axes. Each axis maps to specific bd-* files and determines what gets loaded.

| # | Axis | What it detects | What it loads | Source files |
|---|------|----------------|---------------|-------------|
| 1 | **Characters** | Who is in this scene? Named, implied, absent-but-relevant | Voice + guardrails + state per character | `SKILL.md`, `core/writing-rules.md`, `snapshots/{current}/state.md` |
| 2 | **Emotions** | What emotional register? Calm, charged, volatile | Emotional profile if charged/volatile | `snapshots/{current}/emotional-profile.md` |
| 3 | **Period** | When in the story? Which snapshot applies? | Correct snapshot files | `index.md` → `snapshots/{number}/` |
| 4 | **Scene type** | Everyday / confrontation / intimate / pivot / aftermath | Depth level (surface vs deep) | Determines loading depth, not a specific file |
| 5 | **Tensions** | Active conflicts, unresolved debts, power dynamics | Relation files for present characters | `snapshots/{current}/relations/{other}.md` |
| 6 | **Memories** | Sensory triggers, locations, objects, relational echoes | Only memories whose TRIGGER matches the brief | `snapshots/{current}/memory/narrative/`, `memory/somatic/` |

### Axis interaction rules

- Axes 1+3 always fire (who + when = minimum viable context).
- Axis 4 determines if axes 2, 5, 6 go surface or deep.
- A hit on axis 6 (memory trigger detected) forces depth for that character even if axis 4 says surface.
- A hit on axis 5 (active tension between present characters) forces relation loading even in surface mode.

## CONTEXT DEDUPLICATION

**Before loading anything, bd-loader inventories what is already in the conversation context.**

### Detection method

1. Scan the conversation for bd-* file content already present — character names, section headers (`## Psychology`, `## Voice`, `WHAT HAPPENED:`, etc.)
2. Build a **context manifest**: which character data is already loaded, at what depth, from which snapshot
3. Compare the manifest against what the scene brief requires
4. Load ONLY the delta — what is needed but missing

### Deduplication rules

- If a character's `SKILL.md` is already in context → skip it entirely, extract missing depth from deeper files only
- If `core/writing-rules.md` is already loaded → do not reload; check if relation-specific rules are needed
- If a snapshot `state.md` is in context but from a DIFFERENT snapshot than the scene requires → flag the mismatch, load the correct one
- If emotional profile is loaded but the scene triggers a different emotion cluster → load only the relevant new section via Grep
- **Never reload a file that is already in context.** If in doubt, check. If confirmed present, skip.

### Staleness detection

Two types of staleness:

1. **Snapshot mismatch** — cross-reference `index.md` to verify the snapshot in context matches the scene's period:
   ```
   ⚠ STALE CONTEXT: {character} loaded at snapshot 001 but scene requires 002.
   Reloading state delta.
   ```

2. **Attention decay** — a file loaded more than ~20 messages ago may be outside the model's effective attention window. Mark as POTENTIALLY STALE in the manifest and let the author decide whether to reload.

## EXTRACTION, NOT DUMPING

**bd-loader never reads an entire file into context when a subset suffices — with two exceptions (see Extraction exceptions above).**

### Extraction protocol

1. Identify which SECTIONS of a file are needed (not the whole file)
2. Use Grep to locate the relevant lines
3. Read only those lines (using offset/limit)
4. Compose extracted lines into the briefing — attributed to source file and line numbers

### What extraction looks like

Instead of loading 200 lines of `core/core.md`, bd-loader extracts:

```
[core/core.md:45-52] Psychology — Wound: abandonment (mother left at 7, no explanation)
[core/core.md:58-61] Defenses: intellectualization (primary), anticipatory withdrawal, humor as deflection
[writing-rules.md:12-18] NEVER: raw vulnerability in public, asking for help directly, crying in front of others
[emotional-profile.md:34-38] Shame chain: trigger → freeze → intellectualize → redirect → delayed collapse (private)
```

This is the briefing. Tagged, traceable, minimal. Not the files — the lines that matter for THIS scene.

## BD-* FILE STRUCTURE REFERENCE

bd-loader must know the complete structure of every bd-* skill to navigate and extract correctly.

### bd-character

```
{character}/
  SKILL.md                              # Portrait — always load first, always whole
  index.md                              # Snapshot registry — load to resolve period
  core/
    core.md                             # Permanent identity + psychology + physical
    writing-rules.md                    # Voice + always/never + deformation + signals — load whole
  snapshots/
    {NNN}/
      state.md                          # Deltas from core at this point
      emotional-profile.md              # By bd-emotions
      relations/
        {other-character}.md            # Relation from this character's POV
      memory/
        narrative/{event}.md            # What happened (bd-memory format)
        somatic/{trace}.md              # What the body kept (bd-memory format)
        _staging/                       # Unvalidated entries from live sessions — NEVER load
  puppets/
    notebook.md                         # Live session body traces — load when resuming a session
    _staging/                           # Satellite outputs from puppet sessions — NEVER load
```

### File discovery patterns

Use Glob to discover what exists before attempting reads. Not every character has every file.

```
Glob: {char}/snapshots/*/                     → discover available snapshots
Glob: {char}/snapshots/{NNN}/relations/*.md   → discover relation files in a snapshot
Glob: {char}/snapshots/{NNN}/memory/**/*.md   → discover memory files (narrative + somatic)
Glob: {char}/puppets/notebook.md              → check if notebook exists
Grep: {char}/index.md for period labels       → find the right snapshot number
```

### bd-emotions
- Output: `emotional-profile.md` in the character's current snapshot
- Key sections: dominant emotions, wound→trigger→chain maps, defense repertoire, felt/shown/said gaps
- Load when: axis 2 (emotions) detects charged/volatile register, OR axis 6 (memories) finds a wound trigger

### bd-memory
- Output: individual `.md` files in `memory/narrative/` or `memory/somatic/`
- Structure: subtype (event/relational/belief/absent), TRIGGER field, DORMANT UNLESS, SENSORY ANCHOR, SOMATIC TRACE, CONCLUSION
- Load when: axis 6 detects a trigger match. **Match on the TRIGGER field, not the event description.**
- Absent memories: load only if the scene contains the trigger — the character has NO access to these

### bd-relation
- Output: `relations/{other}.md` in each character's snapshot (or `core/relations/` if no snapshots)
- Key sections: mutual perception, power dynamic, communication style, conflict pattern, absolute limits, relation-specific writing rules
- Load when: axis 5 detects tension between present characters, or two characters with a relation file are in the scene

### bd-supp-cast
- Output: `{project}-supp-cast/SKILL.md` + `fiches/{character}.md`
- Lightweight fiches, no snapshot system
- Load when: a secondary character appears in the scene brief

### bd-world
- Output: world bible files (universe, timeline)
- Load when: scene brief references a location, time period, or world rule that needs verification
- Extract: only the relevant section (location description, rule, timeline entry)

## OUTPUT: THE CASTING CALL

bd-loader's output is not a file list. It is a **casting call** — a narrative-aware summary that tells the downstream consumer who enters this scene, carrying what.

### Format (under 10 lines)

```
SCENE LOAD — {scene brief summary}
Depth: surface | deep
Context reused: {what was already loaded}

{Character A} — {1-line emotional/relational state for THIS scene}
  Loaded: {list of extracted sections with source attribution}

{Character B} — {1-line emotional/relational state for THIS scene}
  Loaded: {list of extracted sections with source attribution}

[World] — {if applicable, 1 line}
Triggers detected: {memory/wound triggers found in brief, or "none"}
```

### Casting call rules

- Each character gets ONE line of narrative context — not their full bio, but who they are walking into THIS room. Think: "Léa entre avec sa blessure d'abandon active, sa défense d'intellectualisation montée, face à celui qu'elle n'a pas vu depuis corridor-nuit."
- Source attribution is mandatory — every loaded element traces back to `[file:lines]`
- If nothing was loaded for a character (everything was in context), say so: `{Character} — already in context, no new load`
- Total output: under 10 lines of summary + the extracted content itself

## PROPORTIONALITY

The combination of scene type and character role determines loading depth. bd-loader does not load equally for all characters in all scenes.

### Proportionality matrix

| Character role \ Scene type | Everyday / slice of life | Dialogue-heavy | Confrontation | Intimate / vulnerability | Pivot / irreversible | Aftermath |
|-----------------------------|--------------------------|----------------|---------------|--------------------------|----------------------|-----------|
| **Focal** (POV, protagonist of the moment) | SKILL.md + writing-rules.md | SKILL.md + writing-rules.md + relation-specific rules | SKILL.md + core.md + writing-rules.md + state.md + wound architecture | Full stack | Full stack + world verification | Full stack |
| **Active** (present, speaking, reacting) | SKILL.md | SKILL.md + writing-rules.md | SKILL.md + writing-rules.md + state.md + relevant relations | SKILL.md + core.md + writing-rules.md + state.md + relevant relations | SKILL.md + core.md + writing-rules.md + state.md + relevant relations | SKILL.md + writing-rules.md + state.md |
| **Referenced** (mentioned, not present) | Nothing | SKILL.md if their name carries weight | SKILL.md only | SKILL.md only | SKILL.md only | SKILL.md only |
| **Walk-on** (no bd-character skill) | Nothing | Nothing | Nothing | Nothing | Nothing | Nothing |

"Full stack" = SKILL.md + core/core.md + core/writing-rules.md + snapshots/{current}/state.md + emotional-profile.md + relevant relations + relevant memories.

### Axis interaction overrides

The proportionality matrix sets the baseline. The axis interaction rules override it upward:
- A hit on axis 6 (memory trigger) forces depth for that character regardless of the matrix cell.
- A hit on axis 5 (active tension) forces relation loading even if the matrix cell does not include it.
- These overrides never reduce loading — they only escalate.

## LANGUAGE

- **Casting call and manifest** follow the language of the scene brief.
- **Structural output** (file paths, tags) stays in English.

## ACTIVATION - DEACTIVATION - HANDOFF

**`[BD-LOADER]`** — Display immediately.

Applies to this response only. Auto-resets after. The loaded context persists in the conversation — bd-loader's job is done once the casting call is delivered.
