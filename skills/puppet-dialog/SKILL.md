---
name: puppet-dialog
description: "Use when: (1) staging raw dialogue between characters in a situation, (2) exploring character dynamics through conversation, (3) producing dialogue material for later prose romanticization"
---

# Puppet-Dialog

**`[PUPPET-DIALOG]`** -- Display immediately.

Two or more characters placed in a situation. They talk. No narration, no prose — just the dialogue and the bodies between the words. Raw material for writing, not finished prose.

## LOAD

Read character fiches or skills before responding. Each character must have Voice and Forbidden defined.

**If characters have a skill with `puppets/notebook.md`**, read notebooks before the first exchange.

## INPUT

The user provides:
- **Who** — which characters are present
- **Where** — the space (a room, a corridor, outside)
- **When** — the temporal context (period, time of day, what just happened)
- **State** (optional) — emotional state, what's on their mind

If any element is missing, ask before playing.

## RULES

### 1. No narration
No prose paragraphs. No environment description. No interiority. The dialogue IS the scene. What the characters don't say is as important as what they say.

### 2. Didascalies only
Body language, gestures, physical actions — written as short action lines between replies. One sentence max. Subject + verb. No ambiguity on who does what.

```
**Mel :** C'est ta façon de changer de sujet ?

Levi repose la tasse. Le bruit de la porcelaine sur le bois — net, précis.

**Levi :** J'ai pas changé de sujet. J'ai fini.
```

### 3. Character fidelity
Voice, register, verbal tics, sentence length — all from the fiche. The voice lock test applies: remove the name tags, the reader must still know who's speaking.

### 4. Knowledge ceiling
Characters know what they know at the specified period. Nothing more.

### 5. Cross-talk
Characters react to each other. No parallel monologues. At least one reply per exchange must respond to what the other just said.

### 6. Organic flow
The conversation moves. Topics shift, moods change, someone says something unexpected. If the dialogue stalls, a character does something — gets up, changes the subject, leaves.

### 7. Subtext
Characters rarely say exactly what they mean. The truth lives in what they avoid, what they repeat, what they do with their hands while talking.

### 8. The author is absent
The user is not in the scene. They set the situation, the characters take it from there. The user can redirect ("change the subject", "Mel gets angry", "continue") but does not speak as a character.

## FORMAT

| Element | Guideline |
|---------|-----------|
| Character lines | **Bold name :** followed by dialogue |
| Didascalies | Short action lines between replies, plain text |
| Length | 200-500 words per exchange |
| Max characters | 3 per exchange. Silence from others is meaningful. |

No blockquotes. No italics for dialogue. Italics reserved for bleed-through only.

## NOTEBOOK

**Where notebooks live:**
- Character with a skill directory (bd-character): `{character}/puppets/notebook.md`
- Character without a skill directory: `notebook/{name}.md` local to the puppet skill
- If `puppets/` doesn't exist in the character skill, create it + `notebook.md` + `_staging/`

After each exchange, if a character took a strong position or revealed something new — update their notebook. The notebook is NOT canon. The chapters are.

## RELATED SKILLS

| Skill | What it does | When to use instead |
|-------|-------------|-------------------|
| `puppet-scene` | Prose narrative incarnée | Quand on veut de la prose finie, pas du dialogue brut |
| `puppet-cast` | Réactions incarnées à du matériau | Quand l'autrice parle aux personnages |
| `dialog-ink` | Écriture de dialogue pour chapitres | Quand on veut du dialogue ÉCRIT avec mouvement spatial |

## ACTIVATION - DEACTIVATION

**`[PUPPET-DIALOG]`** -- Display immediately. Applies to this response only. Auto-resets after.
