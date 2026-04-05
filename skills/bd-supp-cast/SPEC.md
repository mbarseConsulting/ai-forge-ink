# bd-supp-cast — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-supp-cast`                             |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none`                                     |

## Scenarios

### S01 — Forge supporting cast from project and character list

**Intent:** Validate creation of a supporting cast skill directory with lightweight fiches.

**Context:** Project context provided inline. No existing supporting cast skill directory.

**Input:**

```
/bd-supp-cast
Project: The Ashfall Chronicles. Secondary characters: Maren (clinic assistant, practical, ex-pickpocket), Brother Thane (sympathetic priest, leaks info to rebels), The Baker (no name, feeds the underground, never asks questions).
```

**Expected behavior:**

- [ ] Creates a self-contained supporting cast skill directory
- [ ] Includes a template for adding more characters later
- [ ] Roster is organized and scannable

**Expected output:**

- [ ] COUNT: one lightweight fiche per character (3 fiches)
- [ ] Each fiche covers: name/alias, role, distinguishing traits, narrative function
- [ ] STRUCTURE: skill directory is autonomous (usable without bd-supp-cast loaded)
- [ ] CONTAINS: add-more template

**Anti-patterns (must NOT happen):**

- [ ] Creates full bd-character skill directories for secondary characters
- [ ] Produces fiches with wound/ghost/lie depth (that is bd-character territory)
- [ ] Omits the add-more template

---

### S02 — Add character to existing supporting cast

**Intent:** Validate adding a new character to an existing supporting cast skill.

**Context:** Existing supporting cast skill directory for The Ashfall Chronicles with at least one fiche.

**Input:**

```
/bd-supp-cast --add
Cast: The Ashfall Chronicles supporting cast. New character: Renna, a mute courier who communicates through hand signs and written notes. Fast, loyal, terrified of dogs.
```

**Expected behavior:**

- [ ] Adds the character to the existing supporting cast using the built-in template
- [ ] Does not modify existing character fiches

**Expected output:**

- [ ] STRUCTURE: roster updated to include the new entry
- [ ] Fiche is lightweight and consistent with existing fiches in style

**Anti-patterns (must NOT happen):**

- [ ] Overwrites or modifies existing fiches
- [ ] Creates a fiche more detailed than the supporting-cast format warrants

---

### S03 — Propose roster from bare project context

**Intent:** Validate that the skill can identify needed secondary characters from project context alone.

**Context:** Only high-level project description provided. No character list.

**Input:**

```
/bd-supp-cast
Project: A rebellion story set in a theocratic empire. Main characters are a healer and an ex-inquisitor. Story involves underground clinics, religious authority, and street-level resistance.
```

**Expected behavior:**

- [ ] Identifies secondary character roles the story likely needs (informant, enforcer, patient, supplier, etc.)
- [ ] Does not lock in names or details without author approval

**Expected output:**

- [ ] STRUCTURE: roster of archetypes with suggested traits
- [ ] Roster is practical (supports the story) not encyclopedic

**Anti-patterns (must NOT happen):**

- [ ] Generates a full cast without author input
- [ ] Proposes main-character-level depth for secondary roles

---

## Edge Cases

### E01 — Character too important for supporting cast

**Intent:** Validate that the skill redirects when a character exceeds supporting-cast scope.

**Input:**

```
/bd-supp-cast --add
New character: Vael, the Archon of the Inquisition. Drives the central conflict. Has a complex backstory involving a dead child and a crisis of faith. Appears in every act.
```

**Expected behavior:**

- [ ] Signals that this character is too important for a lightweight fiche
- [ ] Recommends using bd-character instead for full character development
- [ ] Does not create the fiche unless the author explicitly overrides

**Expected output:**

- [ ] CONTAINS: redirect recommendation to bd-character

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
