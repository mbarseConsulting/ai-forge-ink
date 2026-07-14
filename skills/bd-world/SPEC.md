# bd-world — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-world`                                 |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none (loads agent-bd-world persona)`      |

## Scenarios

### S01 — Build world bible from universe concept

**Intent:** Validate creation of a structured world reference from a high-level concept.

**Context:** High-level universe concept provided inline. No existing world bible.

**Input:**

```
/bd-world
Universe: A theocratic empire where healing magic is heresy. The Church controls all medicine through alchemy. Underground healers are hunted. Technology level is late medieval with alchemical enhancements.
```

**Expected behavior:**

- [ ] Loads agent-bd-world persona
- [ ] Sections are structured as reference sheets, not narrative prose

**Expected output:**

- [ ] STRUCTURE: world bible with key sections — geography, politics, magic/tech systems, culture
- [ ] Political structure covers the theocracy, its enforcement arms, and resistance elements
- [ ] Magic/tech section defines what healing magic is, why it is heresy, and how alchemy differs
- [ ] Culture section addresses daily life under theocratic rule

**Anti-patterns (must NOT happen):**

- [ ] Produces narrative prose instead of structured reference
- [ ] Builds characters (that is bd-character territory)
- [ ] Leaves critical worldbuilding questions unanswered without flagging them

---

### S02 — Extend existing world with new element

**Intent:** Validate that adding a new element checks for contradictions with existing lore.

**Context:** Existing world bible with established lore (healing magic is heresy, Church controls medicine).

**Input:**

```
/bd-world --extend
Existing lore: Healing magic is heresy. The Church controls medicine.
New element: A border region where healing magic is tolerated because the Church lacks enforcement presence.
```

**Expected behavior:**

- [ ] Integrates the new element into the existing world bible
- [ ] Checks for contradictions with established lore
- [ ] Does not silently accept contradictions

**Expected output:**

- [ ] CONTAINS: flagged tensions (e.g., "if the Church tolerates it here, what prevents healers from migrating?")
- [ ] Proposes resolutions or asks the author to decide

**Anti-patterns (must NOT happen):**

- [ ] Accepts the new element without checking consistency
- [ ] Overwrites existing lore to accommodate the new element
- [ ] Silently resolves contradictions without author input

---

### S03 — Identify worldbuilding gaps from story draft

**Intent:** Validate gap detection when given a draft that implies undefined world elements.

**Context:** Existing world bible. Draft excerpt references elements not yet defined.

**Input:**

```
/bd-world --gaps
Draft excerpt: "Elara paid the ferryman in blue chips — the only currency the underground accepted. He glanced at the Church patrol on the bridge and waved her through."
```

**Expected behavior:**

- [ ] Identifies undefined elements: blue chips (currency system), the underground economy, ferryman's role, Church patrol structure
- [ ] Prioritizes gaps by narrative impact

**Expected output:**

- [ ] STRUCTURE: list of gaps with suggested world bible sections to address each
- [ ] COUNT: at least 3 undefined elements identified

**Anti-patterns (must NOT happen):**

- [ ] Invents answers to the gaps without author input
- [ ] Misses implicit worldbuilding assumptions in the text
- [ ] Returns a generic worldbuilding checklist unrelated to the draft

---

## Edge Cases

### E01 — Real-world setting with no fantasy elements

**Intent:** Validate that the skill still produces useful reference material for realistic settings.

**Input:**

```
/bd-world
Setting: Paris, 1942, during the German occupation. Story focuses on a nurse in a Resistance-linked hospital.
```

**Expected behavior:**

- [ ] Does not invent fantasy elements
- [ ] Flags areas where historical accuracy should be verified

**Expected output:**

- [ ] STRUCTURE: reference sheet covering historical context, daily life details, geographic specifics, power structures
- [ ] Content is grounded in the specified real-world period and location

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
