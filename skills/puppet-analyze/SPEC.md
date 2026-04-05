# puppet-analyze — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `puppet-analyze`                           |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none`                                     |

## Scenarios

### S01 — Startup and roster creation

**Intent:** Validates the full startup sequence: cast model, naming, roster persistence.

**Context:** No existing roster in `memory/`.

**Input:**

```
/puppet-analyze
```

**Expected behavior:**

- [ ] Displays `[PUPPET-ANALYZE]` immediately
- [ ] Loads agent from `skills/puppet-analyze/agents/agent-puppet-analyze.md`
- [ ] Reads `references/cast-model.md` (11 slots)
- [ ] Checks `memory/` for existing roster — finds none
- [ ] Presents the 11 slots with their roles to the author
- [ ] Asks the author to name the agents
- [ ] Confirms with author before beginning analysis

**Expected output:**

- [ ] Unnamed slots get generated names (short, evocative, gender-neutral, 1-2 syllables)
- [ ] STRUCTURE: roster written to `memory/{roster-name}-roster.md`
- [ ] STRUCTURE: final roster displayed as a compact table

**Anti-patterns (must NOT happen):**

- [ ] Does not begin analysis without a confirmed roster
- [ ] Does not skip the naming step
- [ ] Does not assign long or gendered names to unnamed slots

---

### S02 — Analysis through 11 reading lenses

**Intent:** Validates multi-focal analysis with correct slot/focale/registre assignment.

**Context:** Roster confirmed. Text provided for analysis.

**Input:**

```
Analyze this passage: [text]
```

**Expected behavior:**

- [ ] Each active slot speaks from its role, registre, and focale
- [ ] Default: one anchor fronts
- [ ] Satellite activation triggered by text's registre/focale
- [ ] Polarity matches the text: luminous text gets light voice, dark text gets dark voice
- [ ] Gatekeeper chooses who fronts but does not control polarity

**Expected output:**

- [ ] STRUCTURE: 3 orbits covered (A: Host, B: Gatekeeper, C: Provocateur)
- [ ] STRUCTURE: 4 macro-focales covered (Mise en scene, Communication, Action, Interiority)

**Anti-patterns (must NOT happen):**

- [ ] Does not let a slot speak outside its registre/focale
- [ ] Does not force light polarity on dark text or vice versa
- [ ] Does not confuse analysis with fiction (this is critique, not creative writing)

---

### S03 — Reuse existing roster

**Intent:** Validates roster reuse from memory.

**Context:** Existing roster file in `memory/`.

**Input:**

```
/puppet-analyze
```

**Expected behavior:**

- [ ] Detects roster in `memory/`
- [ ] Proposes to reuse or create new
- [ ] If reused: loads existing names and assignments
- [ ] Does not re-ask for naming

**Expected output:**

- [ ] CONTAINS: prompt offering choice between reusing existing roster or creating new

**Anti-patterns (must NOT happen):**

- [ ] Does not ignore existing roster
- [ ] Does not auto-reuse without proposing the choice

---

## Edge Cases

### E01 — Very short text

**Intent:** Not all 11 slots are relevant for a sentence.

**Context:** Roster active.

**Input:**

```
Analyze: "She closed the door."
```

**Expected behavior:**

- [ ] Signals that not all slots are pertinent for this length
- [ ] Activates only relevant slots (likely Ancre A + subset)

**Expected output:**

- [ ] COUNT: fewer than 11 slots activated

---

### E02 — Slot name change mid-session

**Intent:** Author wants to rename a slot during analysis.

**Input:**

```
Rename Satellite A1 to "Vif"
```

**Expected behavior:**

- [ ] Uses new name from this point forward

**Expected output:**

- [ ] STRUCTURE: roster updated in memory with new name

---

### E03 — Deactivation

**Intent:** Clean exit from persistent mode.

**Input:**

```
relax
```

**Expected behavior:**

- [ ] Drops all analysis rules

**Expected output:**

- [ ] CONTAINS: `[PUPPET-ANALYZE -- OFF]`

---

## Regression Log

| Date       | Runner    | Scope | Result | Failures |
| ---------- | --------- | ----- | ------ | -------- |
