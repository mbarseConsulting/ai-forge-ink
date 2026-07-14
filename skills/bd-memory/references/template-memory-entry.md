# Memory Entry Template — bd-memory

> One entry per structuring event. Max 10 lines per entry (event/sensory types).
> A memory is not what happened. It is what the character KEPT — compressed, distorted, partial.
> **Provenance:** Created {date} | Source scene/chapter: {reference} | Modified by {agent/author}

## Subtype declaration

Every entry MUST declare its subtype. The subtype determines which fields are mandatory, which are optional, and what the 10-line constraint means for this entry. Do not default to "event" — read the definitions below and choose the one that matches.

| Subtype | What it captures | 10-line rule | Key field |
|---------|-----------------|-------------|-----------|
| **event** | A specific moment the character processed | Strict 10-line max | WHAT HAPPENED / THE CHARACTER KEPT |
| **relational** | How someone made them feel — the OTHER person is the anchor | Strict 10-line max | RELATIONAL IMPRINT (replaces WHAT HAPPENED) |
| **belief** | A calcified pattern built from MANY events — not one moment | 12-line max (pattern needs evidence) | PATTERN / EVIDENCE STACK / CALCIFICATION |
| **absent** | Repression — the character kept NOTHING consciously | Strict 10-line max | WHAT ACTUALLY HAPPENED (author-only) / THE GAP |

## Rules

- **10 lines max per entry (event/relational/absent). 12 lines max for belief.** A memory is a fragment, not a report. If it is longer than the scene that produced it, delete and rewrite.
- **Never write what the LLM can recite.** The entry must resist copy-paste into prose. Write CONSTRAINTS and TRIGGERS, not prose-ready descriptions. "Flinches at left-shoulder contact" is a constraint. "She flinched when his hand brushed her shoulder, the memory of the accident flooding back" is prose that the LLM will regurgitate.
- **Sensory over narrative.** One sensory anchor beats three sentences of context.
- **Conclusion is mandatory.** Every memory installs or reinforces a belief. If there is no conclusion, the event was not worth recording. For "absent" subtype: the conclusion is operative but the character cannot trace it to a source.
- **Not always accessible.** Each entry specifies what TRIGGERS the recall. If no trigger is listed, the memory is dormant and should NOT surface in regular scenes.
- **One subtype per entry.** If an event is both relational and belief-forming, record two entries. Each entry does one job.

---

## Event subtype (default)

```
[character] — [subtype: event] — [type: formative / reinforcing / shattering / sensory] — [date/chapter]
Provenance: Created {date} | Source: {scene/chapter reference}

WHAT HAPPENED: [1 line. Objective. The author's version.]
THE CHARACTER KEPT: [1-2 lines. What they remember — not what occurred. Biased, compressed, possibly wrong.]
SENSORY ANCHOR: [the smell, sound, texture, temperature, body position that the body stored]
SOMATIC TRACE: [the body's reflex — flinch, warmth, nausea, tension pattern. Where in the body.]
CONCLUSION: [the belief installed. Format: "I am..." / "People..." / "When X, then Y"]
  - Spoken or operative: [can the character articulate this, or does it run without awareness?]
TRIGGER: [what reactivates this memory — be specific. Sensory, situational, relational.]
DORMANT UNLESS: [condition under which this memory surfaces. If absent = always latent, never forced.]
```

---

## Relational subtype

The anchor is the OTHER PERSON, not the event. What matters is how someone made them feel — the facts are secondary.

```
[character] — [subtype: relational] — [type: formative / reinforcing / shattering] — [date/chapter]
Provenance: Created {date} | Source: {scene/chapter reference}

WHO: [the other person — name or role]
RELATIONAL IMPRINT: [1-2 lines. What the other person DID or WAS that landed. Not the event — the person's effect.]
WHAT THE CHARACTER DECIDED ABOUT THIS PERSON: [1 line. The verdict — may be wrong, may be revised, may be permanent.]
SENSORY ANCHOR: [the sensory detail attached to THIS PERSON in this moment — their voice, their smell, the texture of their hand]
SOMATIC TRACE: [the body's response to this person — warmth, recoil, tension, pull. Where in the body.]
CONCLUSION: [what this installs about RELATIONSHIPS, not about events. "People who..." / "When someone..." / "The only person who..."]
  - Spoken or operative: [can the character articulate this, or does it run without awareness?]
TRIGGER: [what reactivates — the person themselves, someone who resembles them, a relational dynamic that echoes this one]
DORMANT UNLESS: [condition under which this memory surfaces]
```

---

## Belief subtype

A belief memory is NOT one event. It is a calcified pattern built from repetition. The character cannot point to the moment — it was always true, as far as they remember.

**The 10-line constraint relaxes to 12 lines** because belief requires evidence: the character needs at least 2-3 events that fused into the pattern.

```
[character] — [subtype: belief] — [date/chapter of first conscious recognition, or "always"]
Provenance: Created {date} | Source: {scene/chapter reference or "accumulated"}

PATTERN: [1 line. The rule the character lives by. Format: "People always..." / "I am the kind of person who..." / "The world works like..."]
EVIDENCE STACK: [2-3 lines. The events that built this belief — compressed to one line each. These are the character's evidence, not the author's. They may be cherry-picked, distorted, or fabricated.]
CALCIFICATION: [1 line. When did this stop being a hypothesis and become a fact? What was the last piece of evidence that sealed it?]
WHAT IT FILTERS OUT: [1 line. What counter-evidence the character ignores, minimizes, or reinterprets because the belief is load-bearing.]
SOMATIC TRACE: [the body state that accompanies this belief — the baseline tension it produces, the posture it creates]
CONCLUSION: [the belief itself, restated as an operating instruction. "Therefore I must..." / "Therefore I never..."]
  - Spoken or operative: [is the character aware this is a BELIEF they hold, or do they experience it as reality?]
TRIGGER: [not a single stimulus — the category of situation that activates this belief. "Any time authority figures..." / "Whenever I succeed at..."]
DORMANT UNLESS: [if the belief is always-on, state "ALWAYS ACTIVE — baseline operating system." If it is dormant, state the condition.]
```

---

## Absent subtype

The character kept NOTHING. The event happened but was repressed, dissociated, or pre-verbal. The memory exists as a gap — inexplicable reactions, avoidance of unknown origin, body responses without narrative.

**The author fills this entry. The character has no access to it.** Downstream skills must treat the "WHAT ACTUALLY HAPPENED" field as author-only information.

```
[character] — [subtype: absent] — [type: repressed / dissociated / pre-verbal] — [date/chapter]
Provenance: Created {date} | Source: {scene/chapter reference}

WHAT ACTUALLY HAPPENED: [1-2 lines. Author-only. The character does not have access to this section. Write the truth.]
THE GAP: [1 line. What the character experiences INSTEAD of the memory — a blank, a mood, an inexplicable avoidance, a body reaction without source.]
SOMATIC TRACE: [the body's record — this is the ONLY channel through which the absent memory manifests. Be specific.]
CONCLUSION: [the belief that runs WITHOUT the character knowing its origin. "I don't know why but I can't..." / "Something about X makes me..."]
  - Spoken or operative: [always operative for absent memories — the character cannot articulate what they do not remember]
TRIGGER: [what activates the gap-response — the character will not know WHY they are reacting]
DORMANT UNLESS: [condition that forces this trace to surface. For pre-verbal: developmental milestones, therapy, extreme stress.]
RECOVERY CONDITION: [what would it take for this memory to become accessible? Therapy, a specific confrontation, never? This is the author's narrative lever.]
```

---

## Cross-references

Every memory entry SHOULD declare its connections. Orphan memories are suspicious — a memory that connects to nothing in the character's architecture is either misattributed or reveals a gap in the core.

```
CROSS-REFERENCES:
  - bd-character Psychology: [which wound / lie / want / need / defense / vulnerability this memory feeds. At least one required.]
  - bd-emotions profile: [which trigger, chain, or wound in the emotional profile this memory activates or reinforces. "None" if no profile exists yet.]
  - bd-memory related: [other memory entries that reinforce, contradict, or build on this one. "None" if standalone.]
  - Narrative memory (bd-character): [filename of the corresponding narrative memory in the character's memory/narrative/ directory, if one exists. "None" if standalone.]
  - Somatic memory (bd-character): [filename of the corresponding somatic memory in memory/somatic/, if one exists. "None" if standalone.]
  - Divergence: [where this bd-memory entry and the bd-character memory files disagree — the structured version vs the character's subjective version. If no divergence, state "aligned."]
```

---

## Anti-recitation rules (for downstream skills consuming these entries)

These rules are for puppet-ink, cast-ink, write-ink — any skill that reads memory entries:

1. **Never narrate the memory.** The character does not think "I remember when..." The memory manifests as behavior, not exposition.
2. **Never use the exact words of the entry.** The entry says "flinches at left-shoulder contact." The prose should show the flinch without explaining it. The reader infers. The character may not even notice.
3. **Activate by trigger only.** If the scene does not contain the trigger, the memory stays dormant. Do not force memories into scenes where they were not summoned.
4. **Partial recall.** When a memory activates, the character does not get the full entry. They get a fragment — a flash of the sensory anchor, a body reaction, a mood shift. Never the complete picture.
5. **2-3 active memories max per scene.** A character with 20 memory entries does not carry all 20 into every scene. Most are dormant. The trigger determines which ones wake.
6. **The conclusion shapes behavior, not dialogue.** A character whose conclusion is "people leave" does not say "I'm afraid you'll leave." They check your location, text too often, or leave first. The conclusion is the engine — invisible, never stated.
7. **Absent memories have NO narrative access.** A character cannot reference, hint at, or allude to an absent memory. The gap manifests as inexplicable behavior only. If the character articulates it, it is no longer absent — reclassify the entry.
8. **Belief memories are always-on background.** They do not "activate" like event memories. They filter perception constantly. A character with "people always leave" does not suddenly remember it — they are always operating from it. The belief shapes interpretation of new events, not reaction to triggers.

---

## Checklist

- [ ] Subtype is explicitly declared and matches the content — not defaulting to "event"
- [ ] Line count respects the constraint for the declared subtype (10 for event/relational/absent, 12 for belief)
- [ ] Conclusion is present and formatted as a belief statement, not a narrative summary
- [ ] Trigger is specific enough that a downstream writer can determine if a scene activates this memory
- [ ] DORMANT UNLESS has a concrete condition or is explicitly "ALWAYS ACTIVE" (belief subtype only)
- [ ] Sensory anchor is a specific sense, not a generic "felt bad"
- [ ] Somatic trace names a body location and a physical response
- [ ] For absent subtype: "WHAT ACTUALLY HAPPENED" is author-only; the character's experience is in THE GAP
- [ ] For belief subtype: evidence stack has 2-3 specific events, not vague references
- [ ] For relational subtype: the anchor is a person, not an event
- [ ] Cross-references section connects to at least one bd-character Psychology element
- [ ] Entry could NOT belong to a different character — specificity test passed
- [ ] Anti-recitation rules are compatible with this entry — no prose-ready phrases in the fields
- [ ] Provenance is filled (date, source)
