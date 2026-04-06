# bd-character — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-character`                             |
| Version     | `v3`                                       |
| Last tested | `—`                                        |
| Depends on  | `none`                                     |

## Scenarios

### S01 — Forge character from brief

**Intent:** Validate full character skill directory creation from a name/role/backstory brief.

**Context:** No existing bd-character skill directory for this character.

**Input:**

```
/bd-character
Forge a character: Elara, rebel healer in a theocratic empire. She lost her family to the Inquisition at 12, survived by hiding her gift. Now runs an underground clinic.
```

**Expected behavior:**

- [ ] Creates a self-contained skill directory with three roots: core/, snapshots/, meta/
- [ ] Generates SKILL.md as generic orchestrator (same template for all characters, only name+description vary)
- [ ] Guides author through 5 phases (identity, psychology, physical/voice, writing rules, finalization)
- [ ] Suggests `--compile` to generate writing/ after forge
- [ ] Does NOT embody or roleplay the character

**Expected output:**

- [ ] STRUCTURE: `SKILL.md` is the generic orchestrator template (no character-specific data beyond frontmatter name+description)
- [ ] STRUCTURE: `core/core.md` + `core/writing-rules.md` contain all permanent character data
- [ ] STRUCTURE: `meta/puppets/notebook.md` + `meta/puppets/_staging/` exist (empty)
- [ ] STRUCTURE (from scratch): no snapshots/ yet, no index.md
- [ ] STRUCTURE (from existing material): `index.md` + `snapshots/001/encyclopedia/state.md` + `encyclopedia/relations/` + `encyclopedia/memory/`

**Anti-patterns (must NOT happen):**

- [ ] SKILL.md contains character-specific data (identity, psychology, voice, relationships)
- [ ] Embodies or speaks as the character
- [ ] Generates a flat file instead of a skill directory
- [ ] Creates writing/ without explicit `--compile` (writing/ is generated, not hand-written)
- [ ] Puts puppets/ at root instead of meta/puppets/

---

### S02 — New snapshot from existing character

**Intent:** Validate snapshot creation after a narrative event changes the character.

**Context:** Existing bd-character skill directory for Elara with at least snapshot 001.

**Input:**

```
/bd-character --new
After the siege of Ashfall, Elara killed someone for the first time to protect a patient. She hasn't spoken about it.
```

**Expected behavior:**

- [ ] Creates a new numbered snapshot (e.g., `snapshots/002/encyclopedia/`) reflecting the evolution
- [ ] Preserves previous snapshots untouched
- [ ] Permanent core/ remains unchanged
- [ ] Updates index.md (new snapshot, writing/ compiled = no)
- [ ] Does NOT rewrite SKILL.md (it's generic, never changes)
- [ ] Suggests `--compile` to regenerate writing/ for the new snapshot

**Expected output:**

- [ ] STRUCTURE: `snapshots/002/encyclopedia/state.md` exists with deltas only
- [ ] CONTAINS: psychological and behavioral shift captured in state.md
- [ ] COUNT: snapshot number increments correctly from the last existing one
- [ ] INDEX: index.md updated with new row, writing/ compiled = no

**Anti-patterns (must NOT happen):**

- [ ] Overwrites or modifies previous snapshots
- [ ] Modifies the permanent core/
- [ ] Rewrites SKILL.md with character-specific portrait data
- [ ] Puts state.md directly in snapshots/002/ instead of snapshots/002/encyclopedia/
- [ ] Skips snapshot numbering

---

### S03 — Generate relation bridges

**Intent:** Validate relation bridge generation between two existing character skills.

**Context:** Two existing bd-character skill directories (Elara and Kael) with populated core/.

**Input:**

```
/bd-character --relation
Characters: Elara (rebel healer) and Kael (inquisitor turned deserter). They were childhood friends before the purge.
```

**Expected behavior:**

- [ ] Generates relation bridge files in each character's `encyclopedia/relations/`
- [ ] Each bridge is written from that character's perspective (asymmetric)
- [ ] Suggests `--compile` to regenerate writing/relations.md

**Expected output:**

- [ ] COUNT: 2 bridge files, one per character in their `snapshots/{current}/encyclopedia/relations/`
- [ ] STRUCTURE: bridges are bidirectional (one per character's perspective)
- [ ] CONTENT: reflects the asymmetry of how each character sees the relationship

**Anti-patterns (must NOT happen):**

- [ ] Creates a single shared relation file instead of per-character bridges
- [ ] Produces identical content for both perspectives
- [ ] Updates SKILL.md with a relationship table (SKILL.md is generic)
- [ ] Puts relation files directly in snapshots/{N}/ instead of snapshots/{N}/encyclopedia/relations/

---

### S04 — Compile writing rules

**Intent:** Validate that --compile reads encyclopedia/ and produces writing/ with actionable instructions.

**Context:** Existing bd-character with core/ + at least one snapshot with encyclopedia/ data.

**Input:**

```
/bd-character --compile
```

**Expected behavior:**

- [ ] Reads core/core.md, core/writing-rules.md, and snapshots/{current}/encyclopedia/ (state, emotional-profile, relations)
- [ ] Generates snapshots/{current}/writing/ with up to 4 files (voice.md, emotions.md, relations.md, body.md)
- [ ] Updates index.md writing/ compiled = yes
- [ ] Every line in writing/ is an imperative instruction, not description

**Expected output:**

- [ ] STRUCTURE: `snapshots/{current}/writing/voice.md` (≤35 lines)
- [ ] STRUCTURE: `snapshots/{current}/writing/emotions.md` (≤35 lines)
- [ ] STRUCTURE: `snapshots/{current}/writing/relations.md` (≤40 lines) or skipped if no relations
- [ ] STRUCTURE: `snapshots/{current}/writing/body.md` (≤30 lines)
- [ ] TOTAL: ≤140 lines across all writing/ files
- [ ] ANTI-RECITATION: zero quoted dialogue in voice.md, zero psychology vocabulary in emotions.md, zero physical inventory in body.md

**Anti-patterns (must NOT happen):**

- [ ] Writes description instead of instructions
- [ ] Quotes catchphrases or example dialogue from core
- [ ] Uses psychology vocabulary (wound, defense, mechanism) in emotions.md
- [ ] Exceeds line budgets
- [ ] Puts writing/ inside encyclopedia/ instead of alongside it

---

## Edge Cases

### E01 — Minimal input (just a name)

**Intent:** Validate that the skill does not forge a hollow character from insufficient input.

**Input:**

```
/bd-character
Forge: Marcus.
```

**Expected behavior:**

- [ ] Asks the author for minimum character details before forging (role, backstory, at least one defining trait)
- [ ] Does not generate a directory from a name alone

**Expected output:**

- [ ] STRUCTURE: no skill directory created

---

### E02 — Snapshot without existing character

**Intent:** Validate graceful handling when --new is called with no prior character.

**Input:**

```
/bd-character --new
After the battle, she changed.
```

**Expected behavior:**

- [ ] Detects no existing character skill to snapshot
- [ ] Asks the author to forge the character first or provide a path

**Expected output:**

- [ ] STRUCTURE: no snapshot created

---

### E03 — Compile without encyclopedia data

**Intent:** Validate fallback when --compile has no snapshot data.

**Input:**

```
/bd-character --compile
(character has core/ only, no snapshots)
```

**Expected behavior:**

- [ ] Compiles from core/ only, outputs to core/writing/
- [ ] Flags: "compiled from core only — no snapshot data"

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
