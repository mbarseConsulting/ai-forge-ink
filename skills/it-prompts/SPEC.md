# it-prompts — Spec

## Meta

| Field       | Value                                      |
| ----------- | ------------------------------------------ |
| Skill       | `it-prompts`                               |
| Version     | `v2`                                       |
| Last tested | `—`                                        |
| Depends on  | `none`                                     |

## Scenarios

### S01 — Image prompt from character description

**Intent:** Validate generation of a detailed image prompt from a character's physical description.

**Context:** Character physical description provided inline. No reference image.

**Input:**

```
/it-prompts
Character: Elara, mid-20s, dark skin, close-cropped silver hair (premature), sharp cheekbones, calloused hands. Wears a stained healer's apron over rough-spun clothes. Always has a leather satchel.
```

**Expected behavior:**

- [ ] Displays `[PROMPT-INK]` tag
- [ ] Translates literary description to concrete visual tags

**Expected output:**

- [ ] STRUCTURE: detailed image generation prompt with appearance, pose, style, lighting
- [ ] CONTAINS: suggested art style and mood
- [ ] Prompt is specific enough to produce a consistent result across generations
- [ ] CONTAINS: key distinguishing features (silver hair, calloused hands, satchel)

**Anti-patterns (must NOT happen):**

- [ ] Invents physical features not in the description
- [ ] Produces a vague or generic prompt ("a woman standing")
- [ ] Omits key distinguishing features (silver hair, calloused hands, satchel)

---

### S02 — Image prompt from scene description

**Intent:** Validate scene-composition prompt generation with mood and framing.

**Context:** Scene description with mood and tension provided inline. No reference image.

**Input:**

```
/it-prompts
Scene: A narrow underground clinic lit by oil lamps. Rows of cots with wounded patients. Elara bends over a patient, hands glowing faintly. Shadows on the stone walls. Tension — a patrol is passing overhead.
```

**Expected behavior:**

- [ ] Translates narrative tension into visual elements (lighting contrast, shadow emphasis)

**Expected output:**

- [ ] STRUCTURE: scene-composition prompt with framing, mood, and color palette
- [ ] CONTAINS: composition details (foreground action, background depth, light source direction)
- [ ] CONTAINS: atmosphere tags (claustrophobic, warm vs. cold light zones)

**Anti-patterns (must NOT happen):**

- [ ] Ignores the mood/tension and produces a neutral scene prompt
- [ ] Describes the scene in prose instead of visual generation tags
- [ ] Omits composition and lighting direction

---

### S03 — img2img prompt from reference image

**Intent:** Validate prompt generation that preserves a reference while applying modifications.

**Context:** Reference image provided. Modification direction specified.

**Input:**

```
/it-prompts --img2img
Reference: [image of a character portrait]
Direction: Same character but older, with a scar across the left temple. More weathered expression. Keep the same art style.
```

**Expected behavior:**

- [ ] Maintains art style consistency with the reference

**Expected output:**

- [ ] STRUCTURE: img2img prompt that preserves the reference's core identity
- [ ] CONTAINS: requested modifications (aging, scar, weathered expression)
- [ ] CONTAINS: denoising/strength guidance appropriate for the changes requested

**Anti-patterns (must NOT happen):**

- [ ] Ignores the reference and generates a prompt from scratch
- [ ] Loses the character's visual identity in the modifications
- [ ] Omits img2img-specific parameters (strength, seed guidance)

---

## Edge Cases

### E01 — Abstract concept with no visual anchor

**Intent:** Validate that the skill asks for direction when input lacks visual specificity.

**Input:**

```
/it-prompts
The feeling of betrayal after discovering a friend's lie.
```

**Expected behavior:**

- [ ] Does not generate a prompt from an abstract concept alone
- [ ] Asks for visual direction: character, setting, symbolic representation, or art style

**Expected output:**

- [ ] CONTAINS: question asking for visual direction
- [ ] Proposes possible visual interpretations for the author to choose from

---

## Regression Log

| Date       | Runner  | Scope | Result | Failures         |
| ---------- | ------- | ----- | ------ | ---------------- |
