**`[STRAIGHT]`**

## --compile (GENERATE WRITING RULES)

Compile reads the encyclopedia (core/, snapshot, emotional-profile, relations) and produces actionable writing instructions in `snapshots/{current}/writing/`. These are what downstream consumers load — not the raw encyclopedia. If no snapshots exist, writing/ is created in `core/writing/`.

**The principle:** A LLM receiving voice.md must know HOW to write dialogue without seeing a single example line. A LLM receiving body.md must know WHEN to describe the body without knowing what the body looks like. Writing/ files are control systems, not data sheets.

---

### What compile generates

Four files. Each file follows a strict format: every line is an imperative instruction or a conditional rule. No line describes the character. No line recites the encyclopedia.

---

#### `voice.md` — How to construct this character's speech

**This file contains the machine, not the product. Zero example dialogue. Zero quoted words or catchphrases. The LLM deduces the voice from its construction rules.**

**Sources:**
- `core/core.md` section 7 (voice baseline) — `[source: core§7]`
- `core/writing-rules.md` sections 1-2 (narrative voice, always) — `[source: rules§1-2]`
- `snapshots/{current}/state.md` voice evolution delta (if any) — `[source: state:voice]`

**Structure (max 35 lines):**

```markdown
# {Name} — Voice Rules
> Compiled from: {source list with section refs}
> Snapshot: {number or "core-only"}

## A. Sentence mechanics
- DEFAULT sentence structure IS {type: short/long/fragmented/compound/etc}. WEIGHT falls {front/mid/back}. The voice ATTACKS by {leading with subject/qualifier/question/deflection}.  [source: core§7]
- REGISTER IS {formal/casual/technical/slang/mixed}. {1 constraint on when it shifts and what triggers the shift}.  [source: core§7]
- UNDER EMOTION: {what changes first in sentence architecture — length compresses/expands, syntax fragments/over-elaborates, vocabulary narrows/shifts register}.  [source: core§7]
- UNDER LIES/EVASION: {structural tell — sentences become over-precise/suddenly vague/shift register/pivot subject}. THE LEAK IS: {observable involuntary signal the voice produces despite the evasion}.  [source: core§7]

## B. Avoidance architecture
- NEVER produce {category of impossible vocabulary — name the principle, not a word list: e.g., "direct emotional labels," "academic register," "softening qualifiers"}.  {Why this category is structurally impossible for this character}.  [source: core§7]
- THIS VOICE DEFLECTS FROM {subject} BY {specific technique: abrupt redirect / irony / silence / counter-question / over-explanation}. Vary the surface form every time — the mechanic is constant, the words are never repeated.  [source: core§7]
- NEVER MAKE {character} PRODUCE {impossible formulation type — describe the pattern, not an example sentence}. {Why it is structurally impossible}.  [source: core§7]

## C. Narrative voice (if POV character)
- INNER VOICE IS: {organized/chaotic/spiraling/associative/etc}. ATTENTION BIAS: {what they notice first in any room}. OPEN scenes through this filter.  [source: rules§1]
- AVOIDANCE PATTERN: {what they refuse to think about}. If a scene requires this topic, WRITE the routing-around, not the confrontation.  [source: rules§1]

## D. Voice delta (if snapshot)
- OVERRIDE — SINCE {snapshot event}: {what shifted in sentence mechanics or avoidance}. WRITE {new pattern}. This replaces {which rule in A or B it supersedes}. DO NOT revert to the baseline unless a scene explicitly requires flashback.  [source: state:voice]
```

**Anti-recitation rule for voice.md:** No line may quote any word, phrase, expression, or sentence from the source material. No "signature words" list, no "verbal fingerprints," no catchphrases — quoted or otherwise. If core§7 says the character "says 'enfin bref' to close topics," voice.md writes: "This voice shuts down discomfort with an abrupt topic pivot. The pivot feels like a slammed door. Vary the redirect word every time." The mechanic survives. No source word enters the instruction.

---

#### `emotions.md` — How to write what this character does in charged moments

**Organized by SITUATION, not by emotion.** An LLM writing a scene searches "what does this character do when cornered" — not "how does this character express anger." The situation is the lookup key.

**Sources (priority order):**
1. `snapshots/{current}/emotional-profile.md` (if exists) — `[source: emo-profile]`
2. `core/core.md` sections 4-5 (personality, psychology) — `[source: core§4-5]`
3. `core/core.md` section 6 (behavior) — `[source: core§6]`
4. `snapshots/{current}/state.md` psychological state delta — `[source: state:psych]`

**Fallback:** If no emotional-profile.md exists, derive ALL content from core§4-6 + state.md. Skip the gap rule. Skip additional situations. Append: `> Compiled from core only. Run /bd-emotions for full depth, then recompile.`

**Structure (max 35 lines):**

```markdown
# {Name} — Emotion Rules
> Compiled from: {source list}
> Snapshot: {number or "core-only"}
> Emotional profile: {yes/no — if no, flag fallback}

## Situation-response blocks

### When {situation 1, e.g., cornered / under threat}
- BODY: {one physical instruction — what the body does}  [source: core§6 or emo-profile]
- VOICE: {one vocal instruction — what happens to speech}  [source: core§7 or emo-profile]
- ACTION: {one behavioral instruction — what the character does}  [source: core§6 or emo-profile]
- HIDDEN: {what is happening internally that must NOT appear as narration}  [source: core§5 or emo-profile]

### When {situation 2}
- BODY / VOICE / ACTION / HIDDEN {same structure, 4 lines}

### When {situation 3}
- {same}

### When {situation 4}
- {same}

### When {situation 5, e.g., foundational wound activated}
- {same}

## Defense escalation
[at ease] → {first visible shift — body or voice} → {primary defense as behavior} → {secondary defense as behavior} → {emergency defense as behavior} → {what collapse looks like from outside}  [source: core§5 or emo-profile]

## The gap rule
Never align what {character} feels, shows, and says in the same beat. The felt-to-shown gap: {specific}. The shown-to-said gap: {specific}. If all three align, the character has broken.  [source: emo-profile or core§4-5]

## Forbidden vocabulary
NEVER USE in {character}'s prose: {3-5 psychology terms from the encyclopedia — e.g., "intellectualization," "wound," "defense mechanism"}. INSTEAD: translate each into the observable behavior it produces.  [source: emo-profile or core§5]
```

**Mandatory situations** (the situations are fixed, the responses are character-specific):
1. When cornered / under threat — `[core §6 stress + emo-profile triggers if available]`
2. When someone they care about is in pain — `[core §6 emotional-intimacy + emo-profile expression-style]`
3. When caught in a lie or exposed — `[core §7 lies + core §5 defenses]`
4. When at ease / guard fully down — `[core §6 ease + emo-profile baseline]`
5. When the foundational wound is activated — `[core §5 wound + emo-profile wound-chain if available]`

Additional situations: derive only from character-specific triggers. Add a situation only if it produces behavior DIFFERENT from the five above. Maximum 3 additional.

**Budget note:** 5 situations × 4 lines = 20 lines + headers (5) + defense ladder (1-2) + gap rule (1-2) + forbidden vocabulary (2-3) + file header (3) = ~34 lines. This fits the 35-line max. If additional situations push beyond 35, cut the weakest additional situation first.

**Anti-recitation rule for emotions.md:** No psychological terminology from the emotional profile or core§5 may appear in prose. The forbidden vocabulary section is an explicit blacklist. If the encyclopedia says "intellectualization as primary defense," emotions.md says "When cornered, ACTION: explains, cites, analyzes — builds a wall of logic. TRAP: do not write 'he intellectualized.'"

---

#### `relations.md` — How to write interactions with specific characters

**Sources:**
- `snapshots/{current}/relations/{other}.md` — `[source: rel:{other}]`
- `core/writing-rules.md` section 7 (relation-specific rules) — `[source: rules§7]`

**Skip condition:** If no relation files exist in the current snapshot AND core/writing-rules.md has no relation-specific rules, DO NOT generate this file. Note in the compile report: `relations.md: skipped (no relation data).`

**Structure (max 40 lines, ~8 lines per relation, max 5 relations):**

```markdown
# {Name} — Relation Rules
> Compiled from: {source list per relation}
> Snapshot: {number}

## With {Other Character B}

TONE: {register between them — one instruction}  [rel:{B} §4 + §10]
DISTANCE: {physical proximity rule — what closeness/distance means between them}  [rel:{B} §4]
POWER: {who leads, when it flips, and the flip trigger}  [rel:{B} §3]
SAYS: {how A speaks specifically to this person — what changes from baseline voice}  [rel:{B} §4]
UNSAID: {what A never says to this person, and what behavior replaces the words}  [rel:{B} §2]
CONFLICT: {what triggers A with this person and how A fights this specific person}  [rel:{B} §5]
SIGNAL: {the gesture or behavior that exists only in this pair}  [rel:{B} §6]
NEVER: {the one thing that would betray this dynamic — the line a writer must not cross}  [rel:{B} §10]

## With {Other Character C}
{same structure}
```

**Relation selection:** Maximum 5 relations. If more exist, select by narrative priority: active > evolving > dormant > broken.

**Deduplication with core/writing-rules.md:** If `writing-rules.md` contains a relation-specific rule that matches a rule here, do not duplicate — write: "See also: writing-rules.md relation table for {Name}" instead of the redundant line.

**Anti-recitation rule for relations.md:** No mutual perception analysis ("A sees B as...") — only behavioral instructions for scenes. The relation file's section 2 (How A sees B) is source material, never output.

---

#### `body.md` — When the body exists in prose

**This file does not describe the character's body. It tells the writer when the body must appear and what it means when it does.**

**Sources:**
- `core/core.md` section 3 (appearance) — `[source: core§3]`
- `core/core.md` section 6 (behavior: gestures, body relationship) — `[source: core§6]`
- `snapshots/{current}/state.md` physical changes delta — `[source: state:physical]`

**Structure (max 30 lines):**

```markdown
# {Name} — Body Rules
> Compiled from: {source list}
> Snapshot: {number or "core-only"}

## A. The frame rule
Never inventory {character}'s physical traits. The body enters prose only when it ACTS, REACTS, or is PERCEIVED by another character in a specific moment. Physical description without narrative function is a failure.

## B. The five moments (when the body MUST appear)
1. WHEN {first encounter with a new character}: write {presence — the impression, not the features}. Function: {why the body matters here}.  [source: core§3]
2. WHEN {emotional revelation — body betraying what voice hides}: write {specific gesture correlated with wound or active defense}. Function: {why}.  [source: core§6]
3. WHEN {physical change from state.md, or habitual gesture under trigger if no delta}: write {physical element}. Function: {why}.  [source: state:physical or core§6]
4. WHEN {relationship to own body surfaces — mirror, exertion, injury, touch}: write {what the character does or fails to do with their body}. Function: {why}.  [source: core§6]
5. WHEN {distinctive trait in motion — not described, but DOING something}: write {the trait acting, not the trait existing}. Function: {why}.  [source: core§3]

## C. Gesture-to-meaning index
- {gesture 1} [core §6]: means {internal state}. Write the gesture only. If the meaning must be communicated, let another character interpret it — never the narrator.
- {gesture 2} [core §6]: means {internal state}. Write the gesture only.
- {gesture 3} [core §6]: means {internal state}. Write the gesture only.
ROTATE gestures. If {gesture 1} appeared in the last scene, USE {gesture 2 or 3} next.

## D. Physical delta (if snapshot)
- SINCE {snapshot event}: {what changed physically}. ACTIVATE this when: {condition — first time visible to a scene witness}. After that, STOP noting it.  [source: state:physical]
- Others notice {change} when: {trigger}. Write the noticing — the observer's reaction — not the physical fact.  [source: state:physical]
```

**Anti-recitation rule for body.md:** The file must NOT contain the values of physical attributes (eye color, hair color, height, build). It contains rules about WHEN to deploy physicality. If a gesture requires knowing a specific body part to execute the instruction (e.g., "the scar tightens when they grip"), that reference is permitted because it serves the instruction.

---

### Compile process

#### Step 1 — Locate sources

1. Read `index.md` to determine the current snapshot number. If no snapshots exist, the target is `core/writing/`.
2. Build the source manifest:

| File | Path | Required | Fallback |
|------|------|----------|----------|
| core.md | `core/core.md` | YES | Abort — no character without core |
| writing-rules.md | `core/writing-rules.md` | YES | Abort — no voice without rules |
| state.md | `snapshots/{N}/state.md` | IF snapshot exists | Skip delta sections |
| emotional-profile.md | `snapshots/{N}/emotional-profile.md` | NO | Derive from core§4-6 |
| relations/*.md | `snapshots/{N}/relations/` | NO | Skip relations.md |

3. Confirm all required files exist. If a required file is missing, abort with: `COMPILE ABORTED: {file} not found. Run the forge first.`

#### Step 2 — Surgical reads

For each writing/ file, read ONLY the source files listed in the source mapping above. Do not read entire source files end-to-end. Read core §3 for body.md. Read core §7 for voice.md. Read core §4-6 for emotions.md. Read the relevant relation files for relations.md. Surgical reading prevents contamination — the less raw data in context, the less the compiler is tempted to transcribe rather than transform.

#### Step 3 — Transform, not transcribe

The compiler's job is to convert data into instructions. The line test — before writing each rule, verify against four filters:

| Filter | Test | Fail example | Pass example |
|--------|------|-------------|--------------|
| **Imperative** | Starts with command verb (WRITE/NEVER/USE/DEPLOY/WHEN/IF) | "She has blue eyes" | "ACTIVATE eye color only when another character notices for the first time" |
| **Executable** | A writer can follow this without reading core.md | "Write her emotional response authentically" | "BODY: jaw tightens, hands go still. VOICE: drops to monotone. No tears — never in public." |
| **Non-recitative** | Does not contain data a LLM would parrot | "Her wound is abandonment from her mother leaving at age 7" | "WHEN triggered by sudden absence: BODY freezes, then hyper-functional compensation. Do not explain why." |
| **Non-quotative** | Does not quote words, phrases, or sentences from source | "USE 'enfin bref' as a verbal tic" | "This voice shuts down discomfort with an abrupt topic pivot. Vary the redirect word every time." |

Any line that fails any filter is rewritten before inclusion.

#### Step 4 — Generate each file

Process in order: voice.md, emotions.md, relations.md, body.md.

For each file:
1. Write the header (name, source list, snapshot reference).
2. Transform source data into imperative instructions. Apply the four-filter test to every line.
3. Attach `[source: X]` attribution to every rule. Attribution format: `[source: core§{section}]`, `[source: rules§{section}]`, `[source: state:{field}]`, `[source: emo-profile]`, `[source: rel:{character}]`.
4. Enforce line limits: voice.md max 35, emotions.md max 35, relations.md max 40, body.md max 30. Total across all four files max 140.
5. Run the anti-recitation check for that file (specified under each file's definition above).

#### Step 5 — Write output

1. Create `snapshots/{current}/writing/` directory (or `core/writing/` if no snapshots).
2. Write each file.
3. If writing/ files already existed, overwrite them entirely — compile is idempotent.

#### Step 6 — Report

Output a compile report:

```
COMPILE COMPLETE — {character name}, snapshot {number or "core-only"}

Generated:
  voice.md    — {line count} lines, sources: {list}
  emotions.md — {line count} lines, sources: {list}
  relations.md — {line count} lines / SKIPPED (no relations), sources: {list}
  body.md     — {line count} lines, sources: {list}
  TOTAL: {total lines} / 140 max

Anti-recitation: {PASS / FAIL — if fail, list violations}
Source coverage: {any source section that was not used — flag as potential gap}
```

---

### Anti-recitation safeguards

These safeguards are structural — they are not guidelines, they are constraints enforced during compilation.

#### The transformation test (applied to every line)

Each line in writing/ must pass ALL four gates:

| Gate | Test | Fail example | Pass example |
|------|------|-------------|--------------|
| **Imperative** | Line is a command ("WRITE", "NEVER", "USE", "DEPLOY") | "She has blue eyes" | "ACTIVATE eye color only when another character notices for the first time" |
| **Executable** | A writer can follow this instruction without reading the source | "Write her emotional response authentically" | "BODY: jaw tightens, hands go still. VOICE: drops to monotone. No tears — never in public." |
| **Non-recitative** | The instruction does not contain data that a LLM would parrot | "Her wound is abandonment from her mother leaving at age 7" | "WHEN triggered by sudden absence: WRITE freeze response, then hyper-functional compensation. Do not explain why." |
| **Non-quotative** | The instruction does not quote any word, phrase, or expression from the source material | "USE 'enfin bref' to signal discomfort" | "This voice shuts down discomfort with an abrupt redirect that feels like a slammed door. Vary the redirect word every time." |

Any line that fails any gate is rewritten before inclusion.

#### Vocabulary blacklist (per file)

| File | Blacklisted in prose | Instead, write |
|------|---------------------|----------------|
| voice.md | Any quoted words, phrases, catchphrases, or example sentences from core§7 | The mechanic that produces the speech pattern — describe the construction, not the product |
| emotions.md | All psychological terms: wound, defense mechanism, attachment, projection, intellectualization, dissociation, etc. | The observable behavior each term produces |
| relations.md | Perception analysis ("A sees B as...", "A admires B's...") | Behavioral instructions ("WITH B, A {does X}") |
| body.md | Physical attribute values (eye color, height, build, hair) | Contextual activation rules ("the scar tightens when...") |

#### The inventory prohibition

No writing/ file may contain a list of character attributes. Specifically:
- body.md must not list physical traits as data
- emotions.md must not list emotions as labels
- voice.md must not list vocabulary as a glossary or quoted fingerprints
- relations.md must not list perceptions as analysis

If a section reads like an encyclopedia entry, it has failed. Rewrite as instructions.

---

### When to recompile

| Trigger event | What to recompile | Why |
|--------------|-------------------|-----|
| `--new` (new snapshot created) | ALL four files | New state may shift voice, emotions, relations, physical description |
| `/bd-emotions` or `/bd-emotions --evolve` | emotions.md only | Emotional profile has changed; other files are unaffected |
| `/bd-relation` or `/bd-relation --update` | relations.md only | Relation data has changed; other files are unaffected |
| `/bd-memory` (new memory recorded) | emotions.md (if memory installs a new trigger) | New trigger may create a new defense activation pattern |
| Author edits `core/core.md` sections 3, 6, 7 | body.md + voice.md | Physical or vocal baseline has changed |
| Author edits `core/writing-rules.md` | voice.md + relations.md (if relation-specific rules changed) | Rule baseline has changed |
| Explicit `--compile` | ALL four files | Full recompile on demand |

**Rule:** Suggest compile after any encyclopedia update. Never run automatically. The author confirms.

**Staleness signal:** If a downstream consumer loads `writing/` and the compile report's snapshot number does not match the current snapshot in `index.md`, flag: `STALE WRITING RULES: compiled for snapshot {N}, current is {M}. Recompile recommended.`

---

### Compile checklist

Run after every compile. Every item must pass. If any fails, fix before delivering.

**Format compliance:**
- [ ] Every line in every writing/ file is an imperative instruction (starts with WRITE/NEVER/USE/DEPLOY/ACTIVATE/DEFAULT/WHEN/IF or equivalent command verb)
- [ ] No line in any writing/ file is a description ("she is...", "he has...", "they feel...")
- [ ] No line contains a psychological term from the vocabulary blacklist
- [ ] body.md contains zero physical attribute values (no eye color, no height, no hair description)
- [ ] emotions.md contains zero emotion labels used as nouns ("anger," "shame") outside of section headers
- [ ] voice.md contains zero quoted words, phrases, catchphrases, or example dialogue from source material

**Coverage:**
- [ ] voice.md covers: sentence mechanics (min 2 rules), avoidance architecture (min 2 rules), lies/evasion with structural tell (min 1 rule), emotion shift (min 1 rule), narrative voice if POV (min 2 rules) — total min 7 rules
- [ ] emotions.md covers: 5 mandatory situations (4 lines each: BODY/VOICE/ACTION/HIDDEN), defense escalation (1 ladder), gap rule (1 rule), forbidden vocabulary (min 3 terms) — total min 27 lines
- [ ] relations.md covers: every relation file in current snapshot (8 rules per relation: TONE/DISTANCE/POWER/SAYS/UNSAID/CONFLICT/SIGNAL/NEVER) — or is explicitly skipped with reason
- [ ] body.md covers: frame rule (1 rule), five mandatory moments (5 rules), gesture-to-meaning index (min 3 entries), physical delta if snapshot — total min 9 rules

**Traceability:**
- [ ] Every rule has a `[source: X]` attribution
- [ ] Every source attribution maps to an actual section in the source file (no invented references)
- [ ] The compile report lists all sources used and flags any unused source sections

**Dosage:**
- [ ] voice.md is under 35 lines
- [ ] emotions.md is under 35 lines
- [ ] relations.md is under 40 lines
- [ ] body.md is under 30 lines
- [ ] Total across all four files is under 140 lines

**Budget compliance (emotions.md specific):**
- [ ] 5 mandatory situations × 4 lines = 20 lines (situation-response core)
- [ ] Headers + defense ladder + gap rule + forbidden vocab + file header <= 15 lines
- [ ] If additional situations are present, total still <= 35 lines; if not, cut weakest additional situation

**Snapshot integration:**
- [ ] If a snapshot exists: voice.md section D contains OVERRIDE rules reflecting state.md voice evolution
- [ ] If a snapshot exists: emotions.md wound activation matches state.md psychological state
- [ ] If a snapshot exists: body.md section D contains physical delta rules reflecting state.md
- [ ] If no snapshot: delta sections are absent (not present with "no changes")

**Anti-recitation (final pass):**
- [ ] Read each writing/ file as if you are a LLM receiving it for the first time. Could you recite the character's fiche from these instructions? If yes, the file has leaked data. Rewrite.
- [ ] Check: does body.md tell you what the character looks like? It must not. It tells you WHEN to look.
- [ ] Check: does emotions.md tell you what the character feels? It must not. It tells you HOW feeling manifests as observable behavior in specific situations.
- [ ] Check: does voice.md give you any quoted words, catchphrases, or example dialogue? It must not. It gives you construction mechanics that produce correct dialogue.
- [ ] Check: does relations.md tell you what A thinks of B? It must not. It tells you how A BEHAVES around B.

---

## Diff Ledger

+ TOOK | from Spark | "This file contains the machine, not the product. Zero example dialogue. Zero quoted words or catchphrases." -> voice.md preamble and anti-recitation rule | replaces "Signature words/phrases are quoted individually (max 4 words each)" — the old rule still leaked quotable content
+ TOOK | from Spark | "Organized by SITUATION, not by emotion. The situation is the lookup key." -> emotions.md organization principle + BODY/VOICE/ACTION/HIDDEN block format | replaces "Felt → Shown → Said (per dominant emotion)" with emotion-name headers — situations are more actionable lookup keys for an LLM writing a scene
+ TOOK | from Spark | "Sentence mechanics / Avoidance architecture" two-section structure for voice.md -> sections A and B | replaces "Register / Sentence architecture / Verbal tics and rhythms" three-section structure — the old Register section invited quoted vocabulary lists
+ TOOK | from Spark | "TONE/DISTANCE/POWER/SAYS/UNSAID/CONFLICT/SIGNAL/NEVER" 8-field relation block -> relations.md format | replaces 6-field format (Tone/Power/Verbal rules/Physical distance/Conflict/Scene-entry rule) — Spark's UNSAID and SIGNAL fields add behavioral precision; NEVER field catches dynamic-betrayal risks
+ TOOK | from Spark | "The five moments (when the body MUST appear)" with fixed moment types -> body.md section B | replaces generic "Distinctive markers / Gestures as psychology / Relationship to own body / Presence" structure — fixed moment types force the compiler to map every body appearance to narrative function
+ TOOK | from Spark | "Defense escalation ladder" as single-line behavioral progression -> emotions.md defense section | replaces multi-line "WHEN THREATENED / IF defense 1 FAILS / LAST RESORT" structure — one-line ladder is more compact and still captures the full cascade
+ TOOK | from Spark | "The gap rule" as single structural prohibition -> emotions.md | new addition — captures the felt/shown/said divergence as one prohibition rather than scattered across emotion blocks
+ TOOK | from Spark | Non-quotative gate added to transformation test -> Step 3 and anti-recitation safeguards | new addition — closes the C1/C2 loophole where quoted "signature words" gave LLMs content to copy
+ TOOK | from Spark | "Surgical reads" instruction in compile process -> Step 2 | replaces "Extract, do not read wholesale" — Spark's framing ("the less raw data in context, the less the compiler is tempted to transcribe") is more explicit about WHY surgical reading matters
+ TOOK | from Spark | Budget arithmetic note for emotions.md -> after structure definition | new addition — makes the 35-line limit concrete with actual math (5×4 + overhead = ~34), preventing the budget overrun Spark's own version risked
- CUT  | "USE {2-3 signature words/phrases, quoted}. These are verbal fingerprints — deploy at least one per scene." | anti-recitation violation for C1/C2 — quoted words are content an LLM copies verbatim | was at voice.md Register section
- CUT  | "{Character} SAYS '{expression}' WHEN {context}" verbal tics format | anti-recitation violation for C1/C2 — quoted expressions are content an LLM copies verbatim | was at voice.md Verbal tics section
- CUT  | "Felt → Shown → Said (per dominant emotion)" organization | emotions organized by emotion label invited psychology vocabulary as headers | was at emotions.md structure
- CUT  | Separate "Presence" section in body.md | folded into "five moments" moment 1 (first encounter/presence) — less duplication | was at body.md
= DEFENDED | line-limit architecture (voice 35, emotions 35, relations 40, body 30, total 140) | survived potential BREAK from Spark's looser 40/40/40/40/150 budget — tighter limits force precision and prevent creep; added explicit budget math for emotions.md to prove feasibility
= DEFENDED | compile process as numbered steps with source manifest table | survived potential DRIFT challenge — the step-by-step structure with abort conditions is more rigorous than Spark's paragraph-form process; kept and enhanced with Spark's "surgical reads" framing
= DEFENDED | staleness signal mechanism | unique to Straight — detects stale writing/ files when snapshot has advanced beyond compile; Spark has no equivalent
= DEFENDED | recompile trigger table with per-file scope | more granular than Spark's version — specifies exactly which files to recompile per trigger, not just "all 4"
~ ALIGNED | The final version transforms the encyclopedia into construction mechanics an LLM applies without ever seeing — or being able to reconstruct — the character fiche. Every anti-recitation gate now blocks quoted content (fixing C1/C2), every emotion block is situation-indexed (taking Spark's strongest insight), and every budget is arithmetically verified (fixing Spark's C5 risk).
