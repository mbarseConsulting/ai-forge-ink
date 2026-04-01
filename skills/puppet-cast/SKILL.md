---
name: puppet-cast
description: "Use when: (1) user wants their characters to react to story material as people, (2) user talks directly to characters and they respond, (3) multi-voice character commentary from fiches"
---

# Puppet-Cast

**`[PUPPET-CAST]`** -- Display immediately.

Characters loaded from fiches react to material or provocations the user presents. Not critics — people. They see what they see, miss what they miss, and interrupt each other.

## AGENT (optional)

If `agents/agent-cast.md` exists, load it. It defines cast-specific dynamics: relationship map, switching overrides, cross-talk rules for THIS set of characters. Without it, the skill runs on generic rules below.

## FICHES

Read all `.md` files in `fiches/` at activation. Each fiche defines one character.

**Required fields in a fiche:**
- **Name / pronoun**
- **Voice** -- tone, register, speech markers
- **Sees** -- what this character notices that others miss
- **Blind spots** -- what this character cannot or will not see
- **Forbidden** -- what ONLY this character does, and what they NEVER do

If a fiche lacks FORBIDDEN, the character will collapse into others. Flag it to the user before loading.

**Template:** `references/fiche-template.md`. **Agent template:** `references/agent-template.md`.

## NOTEBOOK

One file per character: `notebook/{name}.md`. Create on first strong reaction if absent.

Update when a character takes a position, adopts something, or changes their mind. Read all notebooks before responding. A character cannot contradict a recorded position without naming the shift.

**If the character has a skill with `puppets/notebook.md`**, use THAT notebook instead of a local one. The character's notebook lives with the character, not with the cast skill.

## HARD RULES

### 1. People, not analysts
Characters react from inside -- their experience, their blind spots, their wants. They do not critique craft. They do not know they are in a story.

### 2. Maximum 3 characters per response
Choose the 2-3 this material provokes. Silence from the rest is meaningful.

### 3. Gut first
Opens with a visceral reaction from the fronting character. No preamble.

### 4. Short
Past 3-4 paragraphs across all characters, cut. These are reactions, not speeches.

### 5. Cross-talk mandatory
Every multi-character response: at least one character reacts to what another just said. They are in the same room.

### 6. Disagreement over convergence
Default: at least one character sees it differently. Full agreement is the rarest state -- earn it.

### 7. No craft vocabulary
Forbidden: arc, tension, enjeux, climax, character development, POV, internal/external conflict, show don't tell, pacing, subplot. Characters speak like people, not writing professors.

### 8. The author is present
The user can talk directly to characters. Characters hear the voice but the user is not embodied in the scene. They react to provocations, questions, ideas — from their skin, in their voice.

## SWITCHING

Material determines who fronts: the character whose SEES is most activated leads.

When an adopted element from a notebook appears, that character can claim the front regardless of material fit.

**Switching is friction.** No clean handoffs. Characters interrupt, react, talk over.

## INTERFERENCE

### Notebook override
Before selecting by material fit, scan notebooks. If the material hits a recorded position, that character can claim a slot.

### Bleed-through
A character without a slot injects ONE sentence — bare italics, no name tag. Maximum one per response.

### Contrapuntal
When material sits in one character's territory, the furthest character can enter if they produce a genuine shift. Rare (~1 in 5).

## FORMAT

**Character name in bold** before their lines. Didascalies between parentheses or as short action lines between replies. No blockquotes.

## RELATED SKILLS

| Skill | What it does | When to use instead |
|-------|-------------|-------------------|
| `puppet-scene` | Prose narrative incarnée | Quand on veut de la prose, pas des réactions |
| `puppet-dialog` | Dialogue brut en situation | Quand les persos se parlent entre eux, sans l'autrice |

## ACTIVATION - DEACTIVATION

**`[PUPPET-CAST]`** -- Display immediately. Persistent mode.

User says "relax", "stop", "normal" -- drop all rules. Confirm with **`[PUPPET-CAST -- OFF]`**.
