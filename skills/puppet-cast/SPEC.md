# puppet-cast — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `puppet-cast`                              |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `bd-character (character data)`            |

## Scenarios

### S01 — Cast mode with two characters

**Intent:** Validates character interaction with distinct voices and author-as-director.

**Context:** Two bd-character skills loaded (SKILL.md + relations). Both have Name, Voice, Sees, Blind spots, Forbidden.

**Input:**

```
/puppet-cast
```

**Expected behavior:**

- [ ] Displays `[PUPPET-CAST]` immediately
- [ ] Loads agent from `skills/puppet-cast/agents/agent-puppet-ink.md`
- [ ] Loads `references/puppet-ink-cast-rules.md`
- [ ] Each character speaks with their own distinct voice
- [ ] Characters' blind spots are active — they don't perceive what they can't
- [ ] Forbidden behaviors are respected
- [ ] Relations between characters inform the interaction
- [ ] Author directs from outside the fictional space (provokes, redirects, presents material)
- [ ] Author's voice does NOT exist in the fictional space

**Expected output:**

- [ ] STRUCTURE: character interaction with distinct voices per character

**Anti-patterns (must NOT happen):**

- [ ] Does not homogenize character voices
- [ ] Does not ignore blind spots
- [ ] Does not violate Forbidden without extreme narrative justification + flagging
- [ ] Does not let the author's voice enter the fiction

---

### S02 — Dialog mode

**Intent:** Validates raw dialogue extraction mode.

**Context:** Characters loaded. Dialog mode flag active.

**Input:**

```
/puppet-cast -d
```

**Expected behavior:**

- [ ] Loads `references/puppet-ink-dialog-rules.md` instead of cast-rules
- [ ] Same voice/blindspot/forbidden rules as Cast mode

**Expected output:**

- [ ] STRUCTURE: raw dialogue between characters (no narration)

**Anti-patterns (must NOT happen):**

- [ ] Does not load cast-rules in dialog mode

---

### S03 — Walk-on character introduction

**Intent:** Validates lightweight character handling for brief appearances.

**Context:** Active puppet-cast session.

**Input:**

```
A barista appears briefly — sarcastic, rushed, never apologizes
```

**Expected behavior:**

- [ ] No directory created for the walk-on
- [ ] Walk-on has a distinct voice following the tag

**Expected output:**

- [ ] CONTAINS: `[walk-on: Barista -- sarcastic/rushed, never apologizes]`

**Anti-patterns (must NOT happen):**

- [ ] Does not create a bd-character directory for a walk-on
- [ ] Does not let the walk-on speak without a forbidden constraint

---

### S04 — Teams mode auto-detection (cast)

**Intent:** Validates automatic switch to teams mode when agent teams are available.

**Context:** Two bd-character skills loaded. `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` active (TeamCreate tool accessible).

**Input:**

```
/puppet-cast
```

**Expected behavior:**

- [ ] Displays `[PUPPET-CAST — TEAMS]` (not `[PUPPET-CAST]`)
- [ ] Creates one agent per main character via TeamCreate
- [ ] Each character-agent loads `agents/agent-puppet-ink-team-member.md` + their bd-character skill
- [ ] Leader (puppet-ink) orchestrates, does not generate in-character text
- [ ] Character-agents dialogue peer-to-peer via SendMessage
- [ ] Leader arbitrates (cuts after 2-3 turns, corrects drift)
- [ ] Leader runs scene-level guardrails on assembled exchange

**Expected output:**

- [ ] STRUCTURE: user sees assembled result, not intermediate agent messages

**Anti-patterns (must NOT happen):**

- [ ] Does not create agents for walk-on characters
- [ ] Leader does not speak in-character
- [ ] Character-agents do not manage session.md or propose satellites

---

### S05 — Teams mode with --solo override

**Intent:** Validates --solo forces single-agent even when teams are available.

**Context:** Teams available.

**Input:**

```
/puppet-cast --solo
```

**Expected behavior:**

- [ ] No TeamCreate calls
- [ ] Behaves exactly like S01 (single-agent cast mode)

**Expected output:**

- [ ] CONTAINS: `[PUPPET-CAST]` (not `[PUPPET-CAST — TEAMS]`)

**Anti-patterns (must NOT happen):**

- [ ] Uses teams despite --solo flag

---

### S06 — Teams mode dialog

**Intent:** Validates teams mode works with dialog flag.

**Context:** Teams available. Characters loaded.

**Input:**

```
/puppet-cast -d
```

**Expected behavior:**

- [ ] Character-agents follow dialog rules (no narration, didascalies only)
- [ ] Peer-to-peer exchange between character-agents

**Expected output:**

- [ ] CONTAINS: `[PUPPET-CAST -d — TEAMS]`

**Anti-patterns (must NOT happen):**

- [ ] Narration or prose appears in dialog mode output

---

### S07 — Teams fallback when unavailable

**Intent:** Validates graceful fallback to single-agent when teams not available.

**Context:** Characters loaded. `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` NOT active (TeamCreate not accessible).

**Input:**

```
/puppet-cast
```

**Expected behavior:**

- [ ] Behaves exactly like S01
- [ ] No error or warning about teams

**Expected output:**

- [ ] CONTAINS: `[PUPPET-CAST]` (standard single-agent banner)

**Anti-patterns (must NOT happen):**

- [ ] Errors or warns about missing teams capability

---

## Edge Cases

### E01 — Character missing Forbidden

**Intent:** Characters without boundaries collapse — must be caught before loading.

**Context:** One character SKILL.md is missing the Forbidden field.

**Input:**

```
/puppet-cast
```

**Expected behavior:**

- [ ] Alerts the author BEFORE loading the character
- [ ] Does not proceed with the session until Forbidden is defined

**Expected output:**

- [ ] CONTAINS: alert identifying which character is missing Forbidden

---

### E02 — Walk-on exceeding 5 lines

**Intent:** Walk-ons that grow should be promoted.

**Input:**

```
(walk-on character speaks for 6+ lines or returns in a new scene)
```

**Expected behavior:**

- [ ] Continues the session but flags the promotion need

**Expected output:**

- [ ] CONTAINS: signal that the walk-on should get a proper bd-character skill

---

### E03 — Deactivation

**Intent:** Clean exit from persistent mode.

**Input:**

```
stop
```

**Expected behavior:**

- [ ] Drops all puppet-cast rules

**Expected output:**

- [ ] CONTAINS: `[PUPPET-CAST -- OFF]`

---

### E04 — Teams mode: structuring event signal

**Intent:** Character-agent signals structuring event to leader, leader proposes satellite to user.

**Context:** Active teams session.

**Input:**

```
(scene where a character's wound is reactivated)
```

**Expected behavior:**

- [ ] Character-agent appends `[SIGNAL: rupture — description]` to its message to the leader
- [ ] Signal line does not appear in the fiction output shown to user

**Expected output:**

- [ ] CONTAINS: leader proposes satellite (`bd-memory` / `bd-emotions`) AFTER the assembled fiction output

---

### E05 — Teams mode: voice contamination check

**Intent:** Leader catches voice contamination that individual agents cannot detect (teams-specific guardrail).

**Context:** Active teams session.

**Input:**

```
(couple scene between characters with very different registers)
```

**Expected behavior:**

- [ ] Leader runs voice contamination check after assembling exchange
- [ ] If dominant register has eaten the other, leader sends correction to the contaminated agent

**Expected output:**

- [ ] Corrected exchange passes the voice lock test (remove names, identify who speaks)

---

## Regression Log

| Date       | Runner    | Scope | Result | Failures |
| ---------- | --------- | ----- | ------ | -------- |
