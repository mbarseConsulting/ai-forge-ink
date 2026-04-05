# bd-loader — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-loader`                                |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `bd-character (data source)`               |

## Scenarios

### S01 — Auto load from scene brief

**Intent:** Validates full auto-detection: 6 axes, depth selection, casting call output.

**Context:** bd-character skills for Lea and Sacha exist with core/, snapshots, relations.

**Input:**

```
/bd-loader Lea meets Sacha again after 3 months of silence
```

**Expected behavior:**

- [ ] Displays `[BD-LOADER]` immediately
- [ ] Loads agent from `skills/bd-loader/agents/agent-bd-loader.md`
- [ ] Detects both characters (axis 1)
- [ ] Resolves correct snapshot period (axis 3)
- [ ] Classifies scene type — confrontation or intimate (axis 4)
- [ ] Detects tension from 3-month silence (axis 5)
- [ ] Checks for memory triggers matching "silence", "reunion" (axis 6)
- [ ] Does not write prose or embody characters

**Expected output:**

- [ ] STRUCTURE: casting call under 10 lines
- [ ] Each character gets 1 line of narrative context for THIS scene
- [ ] CONTAINS: source attribution `[file:lines]` for every loaded element
- [ ] CONTAINS: depth declared (surface or deep)

**Anti-patterns (must NOT happen):**

- [ ] Does not load entire files when a subset suffices (except SKILL.md and writing-rules.md)
- [ ] Does not load `memory/_staging/` or `puppets/_staging/`
- [ ] Does not reload files already in conversation context

---

### S02 — Scan mode (dry run)

**Intent:** Validates that scan shows the plan without loading anything.

**Context:** bd-character skills for Mel and Levi exist.

**Input:**

```
/bd-loader --scan Confrontation Mel/Levi — Mel knows about the letter
```

**Expected behavior:**

- [ ] Does NOT read any character files into context

**Expected output:**

- [ ] STRUCTURE: casting call + file manifest displayed
- [ ] Lists what WOULD be loaded per character with file paths

**Anti-patterns (must NOT happen):**

- [ ] Does not actually load any data into context

---

### S03 — Surface vs Deep escalation

**Intent:** Validates that wound triggers force depth escalation.

**Context:** Lea has a wound trigger for "abandonment". Brief contains no wound triggers.

**Input:**

```
/bd-loader Light scene, terrace, Lea and her roommates — no drama
```

**Expected behavior:**

- [ ] Selects SURFACE depth (no wound triggers in brief)
- [ ] Does NOT load wound architecture, emotional profile, or memories

**Expected output:**

- [ ] CONTAINS: depth = surface
- [ ] Loads: writing rules (or fallback), guardrails, current state only

**Anti-patterns (must NOT happen):**

- [ ] Does not load deep data for a surface scene

---

### S04 — Context deduplication

**Intent:** Validates that already-loaded data is not reloaded.

**Context:** Lea's SKILL.md and writing-rules.md already loaded in conversation from a previous bd-loader call.

**Input:**

```
/bd-loader Lea and Sacha at the cafe
```

**Expected behavior:**

- [ ] Scans conversation for already-present bd-* data
- [ ] Skips Lea's SKILL.md and writing-rules.md
- [ ] Loads only the delta (new data for this scene)
- [ ] Loads Sacha's data normally

**Expected output:**

- [ ] CONTAINS: indication that Lea is already in context (e.g., `Lea — already in context, no new load` or loads only missing pieces)

**Anti-patterns (must NOT happen):**

- [ ] Does not reload files already present in context

---

### S05 — Plan mode with confirmation gate

**Intent:** Validates that plan mode waits for author approval.

**Context:** bd-character skills for Lea and Sacha exist.

**Input:**

```
/bd-loader --plan Lea meets Sacha again
```

**Expected behavior:**

- [ ] Waits for explicit author confirmation
- [ ] Executes only after confirmation

**Expected output:**

- [ ] STRUCTURE: loading plan presented as a table

**Anti-patterns (must NOT happen):**

- [ ] Does not auto-execute without author saying yes

---

## Edge Cases

### E01 — No scene brief provided

**Intent:** Loader must ask for a brief, not guess.

**Input:**

```
/bd-loader
```

**Expected behavior:**

- [ ] Asks for a scene brief (e.g., "What scene are you preparing?")
- [ ] Does not invent a scene brief

**Expected output:**

- [ ] CONTAINS: question asking for a scene brief

---

### E02 — Character without snapshots

**Intent:** Handles characters at baseline (core only).

**Context:** Nouvel has `core/` only, no `snapshots/` directory.

**Input:**

```
/bd-loader Scene with Nouvel — first arc
```

**Expected behavior:**

- [ ] Loads from core/ only
- [ ] Does not error or expect snapshots

**Expected output:**

- [ ] STRUCTURE: casting call with data sourced from core/ only

---

### E03 — Snapshot mismatch detection

**Intent:** Catches stale context from wrong snapshot period.

**Context:** Lea's snapshot 001 data already loaded, but chapter 12 requires snapshot 002.

**Input:**

```
/bd-loader Lea at chapter 12
```

**Expected behavior:**

- [ ] Flags the mismatch with a warning
- [ ] Loads the correct snapshot (002) data

**Expected output:**

- [ ] CONTAINS: mismatch warning referencing snapshot version

---

### E04 — Proportionality — referenced character

**Intent:** Referenced (not present) characters get minimal or no loading.

**Input:**

```
/bd-loader Lea talks about Sacha to her roommates — Sacha absent
```

**Expected behavior:**

- [ ] Lea: loaded as focal character
- [ ] Sacha: SKILL.md only if name carries weight, otherwise nothing
- [ ] Colocs: nothing (walk-on)

**Expected output:**

- [ ] STRUCTURE: casting call shows differentiated load levels per character

---

## Regression Log

| Date       | Runner    | Scope | Result | Failures |
| ---------- | --------- | ----- | ------ | -------- |
