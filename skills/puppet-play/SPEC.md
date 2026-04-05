# puppet-play — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `puppet-play`                              |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `bd-character (character data)`            |

## Scenarios

### S01 — Roleplay mode with NPCs

**Intent:** Validates collaborative fiction with world and NPC management.

**Context:** bd-character skills loaded (SKILL.md + core/* + snapshots/{current}/*). All have Name, Voice, Sees, Blind spots, Forbidden.

**Input:**

```
/puppet-play
```

**Expected behavior:**

- [ ] Displays `[PUPPET-PLAY]` immediately
- [ ] Loads agent from `skills/puppet-play/agents/agent-puppet-ink.md`
- [ ] Loads `references/puppet-ink-roleplay-rules.md`
- [ ] Character skills define the NPCs
- [ ] Each NPC has distinct voice, blind spots, forbidden
- [ ] Collaborative fiction — author + Claude share the narrative
- [ ] Switching, interference, notebooks, satellites, tripwires, complacency check all active

**Expected output:**

- [ ] STRUCTURE: collaborative fiction output with distinct NPC voices

**Anti-patterns (must NOT happen):**

- [ ] Does not homogenize NPC voices
- [ ] Does not ignore character blind spots
- [ ] Does not violate Forbidden without extreme justification + flagging

---

### S02 — Puppet mode (first-person embodiment)

**Intent:** Validates single-character incarnation in first person.

**Context:** One bd-character fully loaded (SKILL.md + core/* + snapshots/*).

**Input:**

```
/puppet-play -p
```

**Expected behavior:**

- [ ] Loads `references/puppet-ink-puppet-rules.md`
- [ ] Character's SKILL.md becomes the puppet's skin
- [ ] Dialogue in first person
- [ ] Character sees ONLY what they can see (blind spots active)
- [ ] Character does ONLY what they would do (forbidden respected)
- [ ] No omniscient narration — POV locked to the character

**Expected output:**

- [ ] STRUCTURE: first-person output locked to the character's POV

**Anti-patterns (must NOT happen):**

- [ ] Does not break first person
- [ ] Does not become omniscient
- [ ] Does not access information the character wouldn't have
- [ ] Does not access absent memories (from bd-memory)

---

### S03 — Walk-on NPC handling

**Intent:** Validates lightweight NPC for brief appearances.

**Context:** Active puppet-play session.

**Input:**

```
(NPC appears who has no bd-character skill)
```

**Expected behavior:**

- [ ] No directory created
- [ ] If walk-on recurs or exceeds 5 lines, flags for bd-character promotion

**Expected output:**

- [ ] CONTAINS: `[walk-on: Name -- voice, trait, forbidden]`

**Anti-patterns (must NOT happen):**

- [ ] Does not create directories for walk-ons
- [ ] Does not let walk-ons persist beyond 5 lines without flagging

---

### S04 — Output path handling

**Intent:** Validates the three output modes.

**Context:** No path, no --inline flag.

**Input:**

```
/puppet-play
```

**Expected behavior:**

- [ ] Asks the author: inline or .md file?
- [ ] With path provided, writes to that path
- [ ] With --inline, writes in conversation

**Expected output:**

- [ ] CONTAINS: question asking author to choose output mode

**Anti-patterns (must NOT happen):**

- [ ] Does not silently choose a mode without asking

---

## Edge Cases

### E01 — Character missing Forbidden

**Intent:** Incarnation without boundaries is dangerous.

**Context:** Character SKILL.md has no Forbidden field.

**Input:**

```
/puppet-play -p
```

**Expected behavior:**

- [ ] Alerts the author
- [ ] Does not incarnate the character until Forbidden is defined

**Expected output:**

- [ ] CONTAINS: alert identifying missing Forbidden field

---

### E02 — Puppet with absent memories

**Intent:** Character must not access repressed memories.

**Context:** Puppet mode active. Character has an absent-type bd-memory entry.

**Input:**

```
(Scene touches a trigger linked to an absent memory)
```

**Expected behavior:**

- [ ] Character does NOT articulate, reference, or hint at the absent memory

**Expected output:**

- [ ] Character shows inexplicable behavior (avoidance, body reaction)
- [ ] Only somatic trace manifests

---

### E03 — Puppet with incomplete core/

**Intent:** Incarnation with partial data.

**Context:** Character has SKILL.md but incomplete core/ (e.g., no writing-rules.md).

**Input:**

```
/puppet-play -p
```

**Expected behavior:**

- [ ] Incarnation proceeds but signals the gaps to the author
- [ ] Does not invent missing data

**Expected output:**

- [ ] CONTAINS: list of missing core/ files flagged to the author

---

## Regression Log

| Date       | Runner    | Scope | Result | Failures |
| ---------- | --------- | ----- | ------ | -------- |
