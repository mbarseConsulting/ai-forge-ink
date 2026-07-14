# bd-emotions — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-emotions`                              |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none (loads agent-bd-emotions persona)`   |

## Scenarios

### S01 — Build emotional profile from backstory

**Intent:** Validate construction of a structured emotional profile from a character's fiche and backstory.

**Context:** Character fiche or backstory provided inline. No pre-existing emotional profile.

**Input:**

```
/bd-emotions
Character: Elara. Lost her family at 12 to the Inquisition. Survived by hiding. Healer who can't stand helplessness. Overworks to avoid stillness.
```

**Expected behavior:**

- [ ] Loads agent-bd-emotions persona
- [ ] Identifies core emotional triggers tied to backstory (loss, helplessness, hiding)
- [ ] Maps defense mechanisms (overwork, avoidance of stillness)

**Expected output:**

- [ ] STRUCTURE: structured emotional profile with sections for triggers, defenses, expression patterns
- [ ] Expression patterns are specific to this character, not generic
- [ ] Triggers are linked to backstory events

**Anti-patterns (must NOT happen):**

- [ ] Produces a generic profile that could belong to any character
- [ ] Lists emotions without linking them to backstory events
- [ ] Embodies or roleplays the character

---

### S02 — Check emotional coherence in a scene

**Intent:** Validate that emotional reactions in a scene are checked against an established profile.

**Context:** Existing emotional profile for the character. Scene excerpt provided.

**Input:**

```
/bd-emotions --check
Scene: Elara watches a patient die on her table. She calmly cleans her tools and moves to the next patient without a word.
Profile: triggers on helplessness, defends by overworking, avoids stillness.
```

**Expected behavior:**

- [ ] Evaluates whether the reaction is coherent with the established profile
- [ ] Identifies that calm efficiency is consistent with her defense pattern
- [ ] Notes whether the absence of visible emotion is a defense or a gap
- [ ] References specific profile elements in the assessment

**Expected output:**

- [ ] CONTAINS: coherence verdict (consistent, inconsistent, or ambiguous)
- [ ] CONTAINS: reference to at least one specific profile element (trigger, defense, or pattern)

**Anti-patterns (must NOT happen):**

- [ ] Invents profile data that was not provided
- [ ] Gives a blanket "looks fine" without referencing the profile
- [ ] Rewrites the scene instead of diagnosing

---

### S03 — Diagnose shallow emotional expression in prose

**Intent:** Validate detection of cliche or shallow emotional writing.

**Context:** Prose excerpt provided. No character profile required (generic diagnostic).

**Input:**

```
/bd-emotions --diagnose
"Her heart hammered in her chest. Fear gripped her like a vice. She felt a chill run down her spine as the door creaked open."
```

**Expected behavior:**

- [ ] Identifies specific cliche expressions ("heart hammered," "gripped like a vice," "chill down spine")
- [ ] Explains why each is shallow (stock imagery, no character specificity)
- [ ] Suggests depth: what would THIS character feel, physically and psychologically

**Expected output:**

- [ ] COUNT: at least 3 cliches identified
- [ ] Each flagged cliche includes an explanation of why it is shallow
- [ ] Proposes alternatives grounded in the character's psychology when profile is available

**Anti-patterns (must NOT happen):**

- [ ] Gives generic writing advice unrelated to emotional depth
- [ ] Rewrites the passage (diagnoses only)
- [ ] Approves stock phrases as adequate

---

## Edge Cases

### E01 — Character with no backstory provided

**Intent:** Validate profile building when only observable behavior is available.

**Input:**

```
/bd-emotions
Character: Dren. No backstory. Here is a scene: Dren flinches when anyone raises their voice, but speaks softly even when furious. Orders food for others before himself. Sleeps with the light on.
```

**Expected behavior:**

- [ ] Builds a provisional emotional profile from observable behavior only
- [ ] Does not invent backstory to explain the behavior
- [ ] Marks inferences as hypotheses, not facts

**Expected output:**

- [ ] STRUCTURE: profile distinguishes observable facts from inferred hypotheses
- [ ] Notes what is observable vs. what would need backstory confirmation

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
