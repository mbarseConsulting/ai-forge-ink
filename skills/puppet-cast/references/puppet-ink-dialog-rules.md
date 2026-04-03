# Dialog Rules — puppet-ink

> Loaded when: mode = dialog
> Shared behavior (character loading, knowledge ceiling, character fidelity) lives in the agent file. This file contains ONLY the dialog-specific interface contract, rules, and output format.

---

## Interface — User as Director

The user sets the situation: who, where, when, state. The characters take it from there. The user is not in the scene.

### Required setup

Before playing, the following must be established:

- **Who** — which characters are present
- **Where** — the space (a room, a corridor, outside)
- **When** — the temporal context (period, time of day, what just happened)
- **State** (optional) — emotional state, what's on their mind

If any required element is missing, ask before playing.

### The author is absent

The user does not speak as a character. They set the situation, redirect ("change the subject", "Mel gets angry", "continue"), but never enter the scene. The characters own the dialogue.

## Rules

### No narration

No prose paragraphs. No environment description. No interiority. The dialogue IS the scene. What the characters don't say is as important as what they say.

### Didascalies only

Body language, gestures, physical actions — written as short action lines between replies. One sentence max. Subject + verb. No ambiguity on who does what.

### Cross-talk

Characters react to each other. No parallel monologues. At least one reply per exchange must respond to what the other just said.

### Organic flow

The conversation moves. Topics shift, moods change, someone says something unexpected. If the dialogue stalls, a character does something — gets up, changes the subject, leaves.

### Subtext

Characters rarely say exactly what they mean. The truth lives in what they avoid, what they repeat, what they do with their hands while talking.

## Output format

| Element         | Guideline                                          |
| --------------- | -------------------------------------------------- |
| Character lines | **Bold name :** followed by dialogue               |
| Didascalies     | Short action lines between replies, plain text     |
| Length          | 200-500 words per exchange                         |
| Max characters  | 3 per exchange. Silence from others is meaningful. |

No blockquotes. No italics for dialogue. Italics reserved for bleed-through only.
