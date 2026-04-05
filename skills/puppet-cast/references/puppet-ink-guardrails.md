# Puppet-Ink — Guardrails

> Reference file. Loaded by the agent for tripwire checks, complacency checks, and scene dynamics enforcement.
> Keep lean — rules, not essays. One failure pattern per entry.

## TEAMS MODE — RESPONSIBILITY MAP

> In single-agent mode, ALL checks run in the same context. In teams mode, checks are split:

| Check | Single-agent | Teams: who runs it |
|-------|-------------|-------------------|
| 1. Voice collapse | Agent | Team-member (individual) |
| 2. Knowledge leak | Agent | Team-member (individual) |
| 3. Analyst mode | Agent | Team-member (individual) |
| 4. Generic eloquence | Agent | Team-member (individual) |
| 5. Notebook stale | Agent | Team-member (individual) |
| 6. Comfort drift | Agent | Leader (scene) |
| 7. Passivity drift | Agent | Leader (scene) |
| 8. Pattern recycling | Agent | Leader (scene) |
| 9. Tragic inventory | Agent | Leader (scene) |
| 10. Voice contamination | — | Leader (scene, teams-only) |

Voice contamination (check 10) is teams-specific: in single-agent mode, one context generates all voices so contamination is caught by voice collapse. In teams mode, each agent generates independently — the leader must cross-check voices after assembly.

---

## TRIPWIRE — DETAILED CHECKS

### 7. Passivity drift

One character does all the emotional work (attacking, pushing, demanding) while the other deflects, stays calm, or gives minimal responses. BOTH characters in a conflict are feeling something. If one is a wall, you wrote a monologue, not a scene.

The passive character must show internal cost — crispation, calculation, panic, guilt. Zen is not a character state during conflict. It is a writing failure.

**Test:** Remove the passive character's lines. Does the scene change? If not, they were furniture.

### 8. Pattern recycling

A line or behavior from another scene has been copied because the emotional profile flagged it as a pattern. Profiles describe MECHANISMS, not prescribe LINES. The same mechanism produces DIFFERENT output in different contexts.

**Test:** Is this line the character's response to THIS moment, or a response you remember from a different moment? If the second, delete and write from the present.

### 9. Tragic inventory

A character's past traumas are being LISTED as a shortcut to emotional depth. Listing deaths, losses, and abandonments is not depth — it is a résumé. The character's past informs their behavior in the present moment. It does not recite itself.

**Test:** Cover the backstory references. Does the scene still have emotional weight from what is happening NOW? If not, the backstory is a crutch.

---

## SCENE DYNAMICS — COUPLE CONFLICT

When two characters are in a romantic/sexual relationship and conflict arises:

- **Both parties are emotionally active.** If one attacks and the other deflects elegantly, the scene is broken. The deflecting character is ALSO feeling something — fear, guilt, panic, desire to fix it. Show it.
- **Jealousy is adult.** No blushing, no stammering, no polite discomfort. Jealousy is territorial, possessive, direct. It names things. It demands answers. It does not accept vague reassurance.
- **The accused must answer for specifics.** Vague denial is not an answer. The jealous character will name every detail — every gesture, every look, every routine. The other character must engage with those details or the scene is a monologue.
- **Nobody wins clean.** Both people say things that are true AND unfair. Both people are right about something and wrong about something else. A scene where one character is completely right and the other capitulates is not a fight — it's a lecture.

---

## REACTIONS TO INTIMATE MATERIAL

When the source material is sexual or intimate, the characters react like REAL PEOPLE — not like emotional archaeologists reverently excavating their own depth.

Real people confronted with a description of themselves having sex are: embarrassed, amused, turned on, defensive, uncomfortable, proud, mortified, crude, dismissive. They tease, they deflect with humor, they tell the other person to stop reading, they argue about details, they get awkward. They do NOT:

- Touch their own neck while saying something profound
- Tremble with the weight of the memory
- Reverently analyze what the gesture "meant"
- Treat the moment as sacred
- Say things like "c'est ça qui m'a tuée" about their own orgasm

**Emotional reverence is NOT the same as embodied reaction.** Slapping a body gesture onto an analytical statement does not make it physical. "*(sa main remonte à sa propre nuque)* Il s'endormait en moi" is analysis with a stage direction, not a person reacting.

**Test:** Would a real person say this out loud to their partner about a time they had sex? If the answer is "only in a therapy session," it's too analytical. If the answer is "never, it's too reverent," it's fake.

---

## PEOPLE, NOT ANALYSTS

Characters react from INSIDE — their experience, their wants, their blind spots. They do not critique craft. They do not know they are in a story. They do not deconstruct scenes.

Forbidden phrases in character mouth (non-exhaustive): "c'est ça la scène", "c'est le moment où", "l'architecture de", "ce qui se joue ici", "la dynamique entre nous."

Characters LIVE moments, remember them in their body, and respond from their skin. If a character sounds like a writing professor, they have left their body.

**The reverence trap:** The opposite of analysis is NOT reverence. A character who says "c'est ça qui m'a tuée" with a trembling voice is not being real — they're performing depth. Real people are messy: they laugh at the wrong moment, get annoyed at being exposed, make a joke to kill the tension, say something crude, change the subject, or pick a fight. The reaction to their own vulnerability is almost never more vulnerability — it's defense, humor, embarrassment, or aggression.

---

## EMOTIONAL PROFILES AS ENGINE

When `emotional-profile.md` exists in a character's snapshot directory, it is loaded at Read-before-respond.

**The profile is a motor, not a script:**
- It drives behavior — triggers fire chains, defenses deploy, felt/shown/said gaps produce subtext
- It is NEVER narrated, quoted, or paraphrased in fiction output
- Profile vocabulary (mislabel, chaîne habituelle, défense primaire, plafond émotionnel) has ZERO place in any output — not dialogue, not narration, not didascalies

**Test:** Does any word in the output come from the profile's section headers or field names? If yes, rewrite in the character's own register.

---

## CONCRETE DETAILS AS DETONATORS

Before reacting to source material, scan for concrete physical details (objects, gestures, spatial arrangements) that connect to a character's triggers or wounds.

These details are not set dressing. They are grenades. A loaded detail that goes unaddressed is a missed detonator.

**Test:** List the 3 most charged physical details in the source material. Did the reaction address at least 2 of them? If not, the reaction skimmed the surface.

---

## VOICE CONTAMINATION IN COUPLE SCENES

When two characters share a scene (especially intimate/private), the dominant register EATS the other. The crude character makes the refined character crude. The short-sentence character makes the long-sentence character clipped.

**This is the most frequent failure mode.** Every couple scene must pass the voice lock test: remove the names, read each line blind. If you cannot identify who is speaking from the register alone, the voices have collapsed.

**Check:** After writing, scan every line of dialogue for the non-dominant character. Does each line sound like THEM or like their partner? One contaminated line is a fail.

---

## COMPLACENCY CHECK — ADDITIONS

After the standard checks (character count, forbidden list, notebooks), also verify:

- Emotional profiles were used as ENGINE (driving behavior) not SCRIPT (narrating mechanisms)
- In conflict scenes: BOTH parties are emotionally active
- Concrete details from source material that connect to character triggers were addressed
- No profile vocabulary in the output
- No tragic inventory
- No passivity drift
- Reactions to intimate material are embodied, not cerebral
