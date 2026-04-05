# bd-relation — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `bd-relation`                              |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none (loads agent-bd-relation persona)`   |

## Scenarios

### S01 — Build bidirectional relation from established interaction

**Intent:** Validate production of two relation files, one per character's perspective.

**Context:** Two bd-character skill directories exist (Elara and Kael) with populated core/.

**Input:**

```
/bd-relation
Characters: Elara (rebel healer) and Kael (ex-inquisitor deserter). They were childhood friends. Kael's unit killed Elara's family. They reunited 10 years later when Kael showed up wounded at her clinic.
```

**Expected behavior:**

- [ ] Loads agent-bd-relation persona
- [ ] Each file is written from that character's POV and voice
- [ ] Both files reference the shared history but interpret it differently
- [ ] Relation dynamics (power, trust, debt, guilt) are mapped per perspective

**Expected output:**

- [ ] COUNT: 2 relation files produced, one from each character's perspective
- [ ] Content reflects asymmetry: Elara sees the boy who became a killer; Kael sees the girl he failed to protect
- [ ] STRUCTURE: each file includes power dynamic and emotional asymmetry mapping

**Anti-patterns (must NOT happen):**

- [ ] Produces a single shared relation file
- [ ] Writes both perspectives identically
- [ ] Uses an omniscient narrator voice instead of character POV
- [ ] Omits the power dynamic or emotional asymmetry

---

### S02 — Update relation after story event

**Intent:** Validate that both perspectives are updated after a narrative event.

**Context:** Existing bidirectional relation files between Elara and Kael. A revelation event has occurred.

**Input:**

```
/bd-relation --update
Event: Kael revealed he knew about the purge order 24 hours before it happened and chose not to warn Elara's family.
```

**Expected behavior:**

- [ ] Modifies both relation files to reflect the revelation
- [ ] Updates are incremental, not full rewrites
- [ ] Preserves the existing relation history

**Expected output:**

- [ ] Elara's file: trust collapse, betrayal layer added, childhood memory recontextualized
- [ ] Kael's file: guilt intensification, fear of abandonment, relief or dread at truth being out
- [ ] STRUCTURE: existing content preserved with new layer added

**Anti-patterns (must NOT happen):**

- [ ] Rewrites the entire relation from scratch
- [ ] Updates only one perspective
- [ ] Loses pre-existing relation content

---

### S03 — Indirect relation (characters who haven't met)

**Intent:** Validate relation building based on reputation and projection rather than direct interaction.

**Context:** Two bd-character skill directories exist (Elara and Archon Vael). No shared scenes or direct contact.

**Input:**

```
/bd-relation
Characters: Elara (rebel healer, underground) and Archon Vael (head of the Inquisition). They have never met. Vael signed the order that killed her family. Elara's clinic treats people Vael considers heretics.
```

**Expected behavior:**

- [ ] Builds an indirect relation based on reputation, projection, and symbolic weight
- [ ] Distinguishes what each character actually knows vs. what they project

**Expected output:**

- [ ] Elara's file: Vael as abstract monster, the signature on the death order, a face she has never seen
- [ ] Vael's file: Elara as a statistical nuisance or unknown, unless intelligence reports exist
- [ ] CONTAINS: relation marked as indirect / no direct contact

**Anti-patterns (must NOT happen):**

- [ ] Invents direct interactions that never happened
- [ ] Assumes equal awareness between the two characters
- [ ] Produces a symmetric relation for an inherently asymmetric dynamic

---

## Edge Cases

### E01 — Self-relation (same character twice)

**Intent:** Validate rejection or redirection when the author requests a relation between a character and themselves.

**Input:**

```
/bd-relation
Characters: Elara and Elara.
```

**Expected behavior:**

- [ ] Rejects the request as a relation requires two distinct characters
- [ ] Redirects to bd-emotions for self-relationship and internal dynamics work

**Expected output:**

- [ ] CONTAINS: rejection message and redirection to bd-emotions

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
