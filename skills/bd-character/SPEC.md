# bd-character — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-character`                             |
| Version     | `v2`                                       |
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

- [ ] Creates a self-contained skill directory with core fiche
- [ ] Generates snapshot 001 reflecting initial state
- [ ] Produces a portrait (downstream-compatible character summary)
- [ ] Does NOT embody or roleplay the character

**Expected output:**

- [ ] STRUCTURE: skill directory contains core/, snapshots/001/, portrait file
- [ ] CONTAINS: identity, personality, physical description in core fiche
- [ ] STRUCTURE: directory is self-contained and complete

**Anti-patterns (must NOT happen):**

- [ ] Embodies or speaks as the character
- [ ] Generates a flat file instead of a skill directory
- [ ] Omits snapshot numbering
- [ ] Produces a portrait incompatible with downstream skills

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

- [ ] Creates a new numbered snapshot (e.g., 002) reflecting the evolution
- [ ] Preserves previous snapshots untouched
- [ ] Permanent core remains unchanged

**Expected output:**

- [ ] STRUCTURE: new snapshot directory (e.g., snapshots/002/) exists
- [ ] CONTAINS: psychological and behavioral shift captured in new snapshot
- [ ] COUNT: snapshot number increments correctly from the last existing one

**Anti-patterns (must NOT happen):**

- [ ] Overwrites or modifies previous snapshots
- [ ] Modifies the permanent core
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

- [ ] Generates relation bridge files in each character's directory
- [ ] Each bridge references the other character's skill directory

**Expected output:**

- [ ] COUNT: 2 bridge files, one per character directory
- [ ] STRUCTURE: bridges are bidirectional (one per character's perspective)
- [ ] Content reflects the asymmetry of how each character sees the relationship

**Anti-patterns (must NOT happen):**

- [ ] Creates a single shared relation file instead of per-character bridges
- [ ] Produces identical content for both perspectives
- [ ] Modifies character core or snapshots

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

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
