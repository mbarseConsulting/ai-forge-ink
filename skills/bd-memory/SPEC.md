# bd-memory — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-memory`                                |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none (loads agent-bd-memory persona)`     |

## Scenarios

### S01 — Record a structuring event into memory

**Intent:** Validate that a significant event is recorded with subjective distortion appropriate to the character.

**Context:** Character fiche and backstory provided inline. No pre-existing memory entries for this event.

**Input:**

```
/bd-memory
Character: Elara (healer, lost family at 12, avoids helplessness).
Event: During the siege, Elara's patient bled out while she was fetching supplies. She heard the flatline from the corridor.
```

**Expected behavior:**

- [ ] Loads agent-bd-memory persona
- [ ] Records the event in the character's memory layer
- [ ] Applies subjective distortion: what Elara remembers is filtered through her psychology
- [ ] Memory emphasizes the corridor sound (sensory anchor) and helplessness trigger

**Expected output:**

- [ ] STRUCTURE: output distinguishes what happened from what the character retained
- [ ] Distortion reflects her specific wound (may amplify her absence, minimize the inevitability)
- [ ] CONTAINS: sensory anchor (corridor sound)

**Anti-patterns (must NOT happen):**

- [ ] Records the event as objective fact without distortion
- [ ] Produces a memory that could belong to any character
- [ ] Writes prose-ready text instead of structured memory data

---

### S02 — Produce distorted recall

**Intent:** Validate that "how would X remember Y?" produces subjective, fragmented recall.

**Context:** Character has an established emotional profile and memory layer. Event referenced is from early backstory.

**Input:**

```
/bd-memory --recall
How would Elara remember the night of the Inquisition purge when she was 12?
```

**Expected behavior:**

- [ ] Returns what the character REMEMBERS, not what happened
- [ ] Recall is filtered through wounds, defenses, and current emotional state
- [ ] The distortion is consistent with established character psychology

**Expected output:**

- [ ] STRUCTURE: memory is fragmented — sensory flashes, body reactions, emotional residue
- [ ] Missing pieces are genuinely absent, not summarized
- [ ] No complete, coherent narrative of the event

**Anti-patterns (must NOT happen):**

- [ ] Returns a complete, coherent narrative of the event
- [ ] Returns objective facts about what happened
- [ ] Fills gaps with invented details the character would not have

---

### S03 — Update beliefs after major event

**Intent:** Validate that a major event triggers belief and behavioral pattern updates.

**Context:** Character has established beliefs provided inline. A major event contradicts those beliefs.

**Input:**

```
/bd-memory --update
Event: Elara successfully defended the clinic alone, killing an attacker. First time she used violence.
Current beliefs: "I save people, I don't harm them." "Violence is what they do, not what I do."
```

**Expected behavior:**

- [ ] Updates the character's belief system to reflect the event
- [ ] Shows the tension between old beliefs and new evidence
- [ ] Does not erase old beliefs — shows them cracking or adapting

**Expected output:**

- [ ] STRUCTURE: maps behavioral pattern shifts (new reflexes, new avoidances)
- [ ] Tracks what the character tells herself vs. what changed underneath
- [ ] CONTAINS: explicit tension between old identity and new action

**Anti-patterns (must NOT happen):**

- [ ] Replaces old beliefs with new ones cleanly (beliefs are messy)
- [ ] Ignores the contradiction between old identity and new action
- [ ] Produces a therapist's summary instead of internal character data

---

## Edge Cases

### E01 — Trivial event flagged as structuring

**Intent:** Validate that the skill gates recording when an event is not truly structuring.

**Input:**

```
/bd-memory
Character: Elara. Event: She bought bread at the market and had a pleasant conversation with the baker.
```

**Expected behavior:**

- [ ] Challenges whether this event is truly structuring for the character
- [ ] Explains criteria for a structuring event (changes beliefs, installs patterns, leaves traces)
- [ ] Does not record the event unless the author justifies its significance

**Expected output:**

- [ ] CONTAINS: challenge or question about the event's structuring significance
- [ ] Offers to record it if the author provides the structuring dimension

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
