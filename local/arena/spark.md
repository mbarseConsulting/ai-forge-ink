## --compile (GENERATE WRITING RULES)

Compile reads the encyclopedia and produces actionable writing instructions in `snapshots/{current}/writing/`. These files are what downstream consumers load -- not the raw encyclopedia, not the psychology, not the data. writing/ contains ONLY rules an LLM applies while writing prose.

**The cardinal rule:** Every line in writing/ is an instruction or a prohibition. Zero description. Zero psychology vocabulary. Zero physical inventory. If a line could appear in a character sheet, it does not belong in writing/.

---

### What compile reads

| Source file | Provides | Used by |
|-------------|----------|---------|
| `core/core.md` sections 3, 6 | Physical baseline, gesture triggers, body-to-psychology links | body.md |
| `core/core.md` section 7 | Vocabulary, structure, tics, never-says, lies/evasions | voice.md |
| `core/core.md` sections 4-5 | Wound/lie/defense structures, behavioral manifestations | emotions.md |
| `core/core.md` section 6 | Stress/ease/conflict/intimacy patterns | emotions.md |
| `core/writing-rules.md` | Always/never, deformation table, narrative voice, relation-specific rules | voice.md, relations.md |
| `snapshots/{current}/state.md` | Physical deltas, voice evolution, behavior shifts, psychological state | all four files |
| `snapshots/{current}/emotional-profile.md` | Wounds, triggers, chains, felt/shown/said, defense repertoire, expression style | emotions.md |
| `snapshots/{current}/relations/*.md` | Per-relation dynamics, communication, conflict, signals, writing rules | relations.md |

**If a source file does not exist, the compiler works without it.** Missing emotional-profile: derive from core psychology. Missing relations: skip relations.md entirely. Missing state.md (no snapshots): compile from core/ only, write to `core/writing/`.

### Source manifest (compile step 1)

| File | Path | Required | Fallback |
|------|------|----------|----------|
| core.md | `core/core.md` | YES | Abort: `COMPILE ABORTED: core.md not found.` |
| writing-rules.md | `core/writing-rules.md` | YES | Abort: `COMPILE ABORTED: writing-rules.md not found.` |
| state.md | `snapshots/{N}/state.md` | IF snapshot exists | Skip delta/override sections |
| emotional-profile.md | `snapshots/{N}/emotional-profile.md` | NO | Derive from core SS4-6. Flag in header. |
| relations/*.md | `snapshots/{N}/relations/` | NO | Skip relations.md |

---

### Output format contract

Every writing/ file follows this format:

```markdown
# {file title}

> Source: {list of source files read}
> Compiled: {date} | From: {snapshot number or "core"}

---

{Rules organized by numbered sections. Each rule is one line.}
{Format per rule: imperative verb + specific instruction.}
{Source attribution inline: [core SS N] or [state] or [ep] or [rel:Name]}
```

**Format constraints:**
- Each rule starts with an imperative verb: "Write...", "Never...", "When X, do Y...", "If X, avoid..."
- No rule exceeds 2 lines. If it takes more, split it.
- Source attribution uses brackets at end of rule: `[core SS N]`, `[wr]`, `[state]`, `[ep]`, `[rel:Name]`
- Each file: minimum 5 rules, maximum line budget per file (see below).
- **Budget: voice.md 35 lines, emotions.md 35 lines, relations.md 40 lines, body.md 30 lines. Total max 140 lines.**

---

### File 1: voice.md -- How to construct this character's speech

**This file contains the machine, not the product. Zero example dialogue. Zero quoted tics. The LLM deduces the voice from its construction rules.**

Max 35 lines.

#### A. Sentence mechanics

Rules about HOW this character's sentences are built -- rhythm, weight, attack point. Not what they say but the architecture of how they say it.

Derive from `core SS7 sentence-structure + vocabulary + oral-vs-written` and `wr narrative-voice`:

- Sentence length under neutral conditions and what makes it change
- Where the weight falls in this character's sentences (front-loaded, back-loaded, buried)
- What this character attacks first: the subject, a qualifier, a question, a deflection
- Register (formal/casual/technical/slang) and the specific conditions that shift it
- What happens to syntax under emotional pressure: compress, fragment, over-elaborate, go silent, accelerate

**Rule:** No quoted words or phrases from the source. If core SS7 says the character "says 'anyway' to change topics" -- voice.md writes: "This voice closes uncomfortable topics with an abrupt redirect that feels like a door slamming. Vary the redirect word every time." The mechanic survives. The specific word does not enter the instruction.

#### B. Avoidance architecture

Rules about what this voice structurally cannot produce -- the words, subjects, and formulations that are impossible for this character and why.

Derive from `core SS7 never-says + lies/evasions` and `wr never-list`:

- Categories of impossible vocabulary (not a word list -- the principle behind the avoidance: "Never use emotional vocabulary directly -- this character names sensations, not feelings")
- Subjects this voice deflects from, and the specific deflection technique per subject
- How lies sound: the structural tell (over-precision, sudden vagueness, register shift, subject pivot)
- What leaks when the character is evading -- the involuntary signal the voice produces

#### C. Snapshot overrides (only if state.md contains voice-evolution)

Rules about what has CHANGED in this voice. Written as explicit overrides of section A or B.

Derive from `state voice-evolution`:

- Format: "OVERRIDE -- Since {event}: {new rule} replaces {previous pattern from A or B}"
- New verbal habits acquired since the snapshot event
- Lost expressions -- what the voice no longer produces and why

**Anti-pattern -- voice.md rejects:**
- Quoted dialogue or catchphrases (the LLM copies them verbatim instead of generating)
- Lists of "characteristic words" (becomes a vocabulary checklist the LLM recites)
- Personality description dressed as voice description ("she speaks warmly" is description, not construction)
- Tone adjectives without mechanics ("sardonic" means nothing -- "short sentences that end by undermining their own opening" is a mechanic)

---

### File 2: emotions.md -- How to write what this character does in charged moments

**Organized by SITUATION, not by emotion.** An LLM writing a scene never searches "how does this character express anger" -- it searches "what does this character do when cornered." The situation is the lookup key.

Max 35 lines.

#### A. Situation-response blocks

Compile 4-6 blocks. Each block is one situation the character is likely to face, with a compressed behavioral instruction set.

**Block format (strict -- 3 lines per block + header):**

```
### When {specific situation}
- SHOW: {what an observer sees -- one body instruction + one voice instruction} [source]
- DO: {what the character does + what is happening internally that must NOT surface as narration} [source]
- NEVER: {the cliche or trap an LLM would default to here, and what to write instead} [source]
```

**Mandatory situations** (derive content from sources -- the situations are fixed, the responses are character-specific):
1. When cornered / under threat -- `[core SS6 stress + ep triggers]`
2. When caught in a lie or exposed -- `[core SS7 lies + core SS5 defenses]`
3. When at ease / guard fully down -- `[core SS6 ease + ep baseline]`
4. When the foundational wound is activated -- `[core SS5 wound + ep wound-chain]`

Additional situations (max 2): derive only from character-specific triggers. Add a situation only if it produces behavior DIFFERENT from the four above.

#### B. Defense escalation ladder

One compact line showing the behavioral progression from comfort to collapse. No psychology terms -- observable behavior only.

```
[at ease] > {first visible shift} > {primary defense as behavior} > {secondary defense} > {emergency defense} > {collapse from outside}
```

Derive from `core SS5 defenses (behavioral manifestations)` + `ep defense-repertoire` if available.

#### C. The gap rule

One prohibition capturing the structural divergence between felt, shown, and said.

Format: "Never align what {character} feels, shows, and says in the same beat. Felt-to-shown gap: {specific}. Shown-to-said gap: {specific}. If all three align, the character has broken."

Derive from `ep felt/shown/said` if available. If not, derive from `core SS4 facade-vs-core` + `core SS5 defenses`.

**Anti-pattern -- emotions.md rejects:**
- Psychology vocabulary as headers or content (wound, defense mechanism, attachment, trauma response, intellectualization)
- Emotion-name headers ("Anger", "Sadness", "Joy") -- situations are headers, not emotions
- Internal monologue scripts -- the DO line names the internal state, it does not script thoughts
- Universal human reactions ("pupils dilate", "heart races") -- only what is specific to THIS character

**Fallback (no emotional-profile exists):** Compile the 4 mandatory situations from core SS5 + core SS6. Skip gap rule. Skip additional situations. Append: "compiled from core only -- run /bd-emotions for full depth, then recompile."

---

### File 3: relations.md -- How to write interactions with specific characters

**One block per relation file in `snapshots/{current}/relations/`.** If no relation files exist, do not generate this file.

Max 40 lines.

**Block format (strict -- 8 lines maximum per relation):**

```
### With {character name}

TONE: {register between them -- one instruction} [rel:Name SS4 + SS10]
DISTANCE: {physical proximity rule -- what closeness/distance means between them} [rel:Name SS4]
POWER: {who leads, when it flips, and the flip trigger} [rel:Name SS3]
SAYS: {how A speaks specifically to this person -- what changes from baseline voice} [rel:Name SS4]
UNSAID: {what A never says to this person, and what behavior replaces the words} [rel:Name SS2]
CONFLICT: {what triggers A with this person and how A fights this specific person} [rel:Name SS5]
SIGNAL: {the gesture or behavior that exists only in this pair} [rel:Name SS6]
NEVER: {the one thing that would betray this dynamic -- the line a writer must not cross} [rel:Name SS10]
```

**Relation selection:** Maximum 5 relations. If more exist, select by narrative priority: active > evolving > dormant > broken. Within equal status, select by proximity to current story arc.

**Deduplication with core/writing-rules.md:** If `writing-rules.md` contains a relation-specific rule that matches a rule here, do not duplicate -- write: "See also: writing-rules.md relation table for {Name}" instead of the redundant line.

**Anti-pattern -- relations.md rejects:**
- Backstory of the relationship (how they met, what happened) -- data, not instruction
- Psychological analysis of the dynamic ("codependent", "anxious attachment") -- write the behavior to produce
- Symmetrical statements ("they both care about each other") -- writing/ is from THIS character's perspective. Asymmetry is structural.

---

### File 4: body.md -- When the body exists in prose

**This file does not describe the character's body. It tells the writer when the body must appear and what it means when it does.**

Max 30 lines.

#### A. The frame rule

One overarching prohibition -- the first line of the file:

> "Never inventory {character}'s physical traits. The body enters prose only when it ACTS, REACTS, or is PERCEIVED by another character in a specific moment. Physical description without narrative function is a failure."

This rule is non-negotiable and derives from the anti-recitation rules.

#### B. The five moments (when the body MUST appear)

Exactly 5 situations where physical description is mandatory because the body carries narrative meaning. Each moment names: the situation, which physical element to activate, and why it matters.

**Format:**

```
1. WHEN {situation}: write {physical element}. Function: {why the body matters here}. [source]
2. WHEN {situation}: write {physical element}. Function: {why}. [source]
3. WHEN {situation}: write {physical element}. Function: {why}. [source]
4. WHEN {situation}: write {physical element}. Function: {why}. [source]
5. WHEN {situation}: write {physical element}. Function: {why}. [source]
```

**Mandatory moment types** (the types are fixed -- the content is character-specific):
1. First encounter with a new character -- activate presence (core SS3 presence), not inventory. Write the impression, not the features.
2. Emotional revelation -- the body betraying what the voice hides. Derive from core SS6 habitual-gestures + the specific gesture that correlates with the wound or active defense.
3. Physical change from state.md -- if state contains any physical delta, this is a moment. If no delta exists, replace with: a specific habitual gesture under its trigger condition.
4. Relationship to own body surfacing -- from core SS6 body-relationship. The moment the character's relationship with their own physicality becomes visible (mirror, exertion, injury, touch).
5. The distinctive trait in motion -- not the trait described, but the trait DOING something. Derive from core SS3 distinctive-traits. "The scar catches light" not "he has a scar."

#### C. Gesture-to-meaning index

3-5 rules linking specific gestures to their underlying state. The instruction: write the gesture, NEVER write the meaning.

**Format:**

```
- {gesture} [core SS6]: means {internal state}. Write the gesture only. If the meaning must be communicated, let another character interpret it -- never the narrator.
```

Derive from `core SS6 habitual-gestures` + `core SS5 psychology`.

#### D. Physical delta instructions (only if state.md contains physical changes)

Rules about how to handle what changed physically since core.

- "Since {event}, {character} {change}. Activate this when: {condition}. Write it as: {instruction}."
- "Others notice {change} when: {specific trigger}. Write the noticing -- the observer's reaction -- not the physical fact."

Derive from `state physical-changes`.

**Anti-pattern -- body.md rejects:**
- Physical description data (eye color, height, build, hair color, weight) -- that lives in core SS3 and never enters writing/
- Exhaustive gesture catalogs -- only 3-5 gestures with clear psychological triggers make the cut
- Beauty or attractiveness statements -- how someone looks is not an instruction
- "Show don't tell" as a rule -- too vague. The five moments and gesture index replace this cliche with precision.

---

### Compile process

1. **Identify the target.** Read `index.md` to find the current snapshot number. If no index.md, compile from core/ only, output to `core/writing/`. Verify required files exist per source manifest (see above). Abort if core.md or writing-rules.md is missing.

2. **Surgical reads.** For each writing/ file, read ONLY the source files listed in the source table. Do not read the entire encyclopedia. Surgical reading prevents contamination -- the less raw data in context, the less the compiler is tempted to transcribe rather than transform.

3. **Transform, not transcribe.** The compiler's job is to convert data into instructions. Three test derivations to illustrate the transformation:

   - Source: `core SS3 -- "blue eyes, piercing gaze"` -> body.md: "Mention eyes only when another character is held by the gaze. Write the sensation of being looked at, not the color."
   - Source: `core SS5 -- "intellectualization as primary defense"` -> emotions.md: "When cornered, SHOW: stillness, sentences lengthen and register rises. DO: explains and analyzes; terror underneath -- never surface it. NEVER: do not write 'he intellectualized' -- write the lecture."
   - Source: `core SS7 -- "says 'enfin bref' to close topics"` -> voice.md: "This voice shuts down discomfort with an abrupt topic pivot. The pivot feels like a slammed door. Never write the same redirect word twice -- vary it each time."

4. **The line test.** Before writing each rule, verify against four filters:
   - **Instruction test:** Does it start with an imperative verb? If no -> rewrite or discard.
   - **Description test:** Does it contain "is", "has", "feels" as main verb? If yes -> rewrite as instruction.
   - **Autonomy test:** Can an LLM follow this without reading core.md? If no -> add missing context to the rule.
   - **Recitation test:** Could an LLM paste this line into prose verbatim? If yes -> the rule is too specific. Abstract to the mechanic.

5. **Write files.** Create `snapshots/{current}/writing/` (or `core/writing/`). Write each file that has sufficient source material (minimum 5 rules). If a file would have fewer than 5 rules, skip it and report why.

6. **Budget audit.** After writing all files, count lines:
   - voice.md: max 35 lines
   - emotions.md: max 35 lines
   - relations.md: max 40 lines
   - body.md: max 30 lines
   - Total: max 140 lines
   - If over budget: cut the weakest rules (those with the least specific instructions or the most overlap with other files)

7. **Report.** Display after compilation:

```
COMPILE REPORT -- {character name} -- snapshot {number}
Files generated: {list with line counts}
Files skipped: {list with reason}
Total: {N}/140 lines
Sources read: {file list per output file}
```

**Staleness signal:** If a downstream consumer loads `writing/` and the compile report's snapshot number does not match the current snapshot in `index.md`, flag: `STALE WRITING RULES: compiled for snapshot {N}, current is {M}. Recompile recommended.`

---

### When to recompile

| Trigger | Scope | Reason |
|---------|-------|--------|
| `--new` (new snapshot) | All 4 files | New state deltas may affect voice, emotions, body, relations |
| `/bd-emotions` or `--evolve` | emotions.md | Emotional profile changed -- situation-response blocks may differ |
| `/bd-relation` or `--update` | relations.md | Relation data changed -- interaction rules need refresh |
| `/bd-memory` (new memory with trigger link) | emotions.md | New memory may reinforce or alter a trigger-response chain |
| Core retcon (core.md edited) | All 4 files | Foundation changed -- everything downstream is suspect |
| Explicit `--compile` | All 4 files | Full recompile on demand |

**Suggest compile after any encyclopedia update.** Never run automatically -- the author decides.

---

### Compile checklist

- [ ] **Instruction purity:** Every line in every writing/ file starts with an imperative verb or "When/If" conditional. Zero lines with "is/has/feels" as main verb.
- [ ] **Anti-recitation -- body.md:** Contains zero physical measurements, zero color descriptions, zero beauty assessments. Only activation rules.
- [ ] **Anti-recitation -- emotions.md:** Contains zero psychology vocabulary (wound, defense, attachment, trauma, mechanism). Only behavioral descriptions. Zero emotion-name headers.
- [ ] **Anti-recitation -- voice.md:** Contains zero quoted dialogue, zero listed catchphrases, zero personality adjectives. Only construction mechanics.
- [ ] **Coverage:** Each generated file contains minimum 5 actionable rules.
- [ ] **Source attribution:** Every rule ends with a bracketed source.
- [ ] **Budget -- voice.md:** max 35 lines.
- [ ] **Budget -- emotions.md:** max 35 lines.
- [ ] **Budget -- relations.md:** max 40 lines.
- [ ] **Budget -- body.md:** max 30 lines.
- [ ] **Budget -- total:** All files combined max 140 lines.
- [ ] **voice.md:** Covers sentence mechanics (A), avoidance architecture (B), snapshot overrides if applicable (C). No quoted words or phrases from source -- mechanics only.
- [ ] **emotions.md:** Organized by situation (4-6 blocks, 3 lines each). Defense ladder present (1 line). Gap rule present (or flagged as core-only). No emotion-name headers.
- [ ] **relations.md:** One block per active relation, max 8 rules per block, max 5 relations. No backstory, no psychology labels. Deduplication with writing-rules.md verified.
- [ ] **body.md:** Frame rule present. Exactly 5 mandatory moments. Gesture-to-meaning index (3-5 entries). Physical delta instructions if state.md has changes.
- [ ] **Snapshot integration:** voice.md section C and body.md section D reflect state.md deltas. Written as OVERRIDE, not replacement.
- [ ] **No invention:** Every rule traces to an existing source file and section. The compiler derives -- it never adds traits, behaviors, or details absent from the encyclopedia.
- [ ] **Autonomy:** A downstream consumer loading only writing/ (without core.md) can follow every rule. No rule requires external context to be actionable.

---

## Challenge from Agent B

DRIFT (intent deviation):
- Straight voice.md `## Verbal tics and rhythms` section instructs: `{Character} SAYS "{expression}" WHEN {context}` -- this quotes signature words/phrases directly into the writing rules. The Intent Anchor demands "des regles que le LLM applique sans reciter la fiche." Quoting tics IS reciting the fiche. The LLM will parrot these exact words instead of generating from mechanics.

TAKE (from Straight):
- Source manifest table (Step 1 in Straight's compile process): explicit Required/Fallback columns with abort conditions for missing core files. Better engineering than my inline fallback mentions -- formalizes the dependency chain. Taking and integrating into source section.
- Per-file line budgets (35/35/40/30 = 140 total): tighter than my original 40/file x 150 total. The differentiated budgets reflect real content density -- relations.md needs the most space, body.md the least. Taking as the budget contract.
- Staleness signal: Straight's concept of flagging when writing/ snapshot number diverges from index.md current. Clean operational safeguard absent from my version. Taking into compile report section.

GIVE (strongest differentiators Straight should consider):
- Situation-based organization for emotions.md: "When cornered" is a scene lookup key. "Anger" is a psychology lookup key. An LLM writing a scene knows the situation, not the emotion label. Straight's `## Felt > Shown > Said (per dominant emotion)` with headers like `### Anger` uses emotion-name headers -- the exact anti-pattern the spec forbids.
- No-quoted-words rule in voice.md: "No quoted words or phrases from the source" is the structural enforcement that prevents tic recitation. Straight's explicit `USE {2-3 signature words/phrases, quoted}` and `{Character} SAYS "{expression}"` instructions invite verbatim copying.
- The HIDDEN/internal-state line in situation blocks: naming what must NOT appear in narration is a stronger anti-recitation guard than Straight's `THE GAP` inline in each emotion block.

BREAK (what will fail against criteria):
- Straight's voice.md breaks C1 (anti-recitation, instruction purity) and C2 (anti-recitation enforcement): `USE {2-3 signature words/phrases, quoted}. These are verbal fingerprints` is a quoted-word list. `{Character} SAYS "{expression}" WHEN {context}` is a catchphrase catalog. The anti-recitation checklist explicitly says "voice.md: Contains zero quoted dialogue, zero listed catchphrases." Straight's own checklist contradicts its own voice.md template. Scoring impact: 0.5 on both C1 and C2.
- Straight's emotions.md breaks the Intent Anchor's situation-vs-emotion architecture: headers like `### {Emotion 1, e.g., Anger}` are emotion-name headers. The anti-pattern section of the spec explicitly rejects "Emotion-name headers ('Anger', 'Sadness', 'Joy') -- situations are headers, not emotions." Straight organizes by what the character feels, not by what scene context triggers the behavior. An LLM in a scene does not think "now I need to write anger" -- it thinks "now the character is cornered."

## Rebuttal from Agent B (pre-emptive, against likely A challenges)

**Likely BREAK from A: "Spark's emotions.md busts the 40-line budget with 5 situations x 5 lines."**
CONCEDE. Fixed. Reduced mandatory situations from 5 to 4 (merged "someone they care about is in pain" into wound-activation or additional-situation territory since it overlaps). Compressed block format from 5 lines to 3 (SHOW merges body+voice, DO merges action+hidden, NEVER captures the trap). Defense ladder stays as 1 line. Gap rule stays as 1 line. Budget math: 4 blocks x 4 lines (header + 3) = 16, plus ladder (2 with header), gap rule (2 with header), section headers and anti-patterns (8), file header (4) = ~32 lines. Under 35.

**Likely DRIFT from A: "Spark's compile section is too long / too prescriptive for a skill file."**
DEFEND. The Intent Anchor says "des instructions d'ecriture actionnables -- pas de la description, pas de la psychologie brute, mais des regles que le LLM applique sans reciter la fiche." The compile section IS the transformation engine that enforces this. Every line of specification exists to prevent a specific failure mode (recitation, description-as-instruction, psychology vocabulary leaking). Cut the specification and the compiler loses its constraints -- which means the anti-recitation principle has no teeth.

**Likely TAKE demand from A: "Spark should adopt Straight's explicit 'Forbidden vocabulary' section in emotions.md."**
REJECT. A dedicated forbidden-vocabulary section in the output file is a vocabulary checklist -- which Spark's anti-pattern rules already reject for voice.md. The prohibition belongs in the compile checklist (which enforces it during generation) and in the anti-pattern block (which defines it). Putting a blacklist in the output file tempts the LLM to treat it as a reference card rather than an internalized constraint.

---

## Diff Ledger

+ TOOK | from Straight | Source manifest table with Required/Fallback/Abort columns | -> "Source manifest (compile step 1)" section | new addition
+ TOOK | from Straight | Per-file budgets 35/35/40/30 = 140 total | -> format constraints + all per-file headers + budget audit step + checklist | replaces "maximum 40 lines per file, 150 total"
+ TOOK | from Straight | Staleness signal concept | -> added after compile report in process section | new addition
- CUT  | "When someone they care about is in pain" as mandatory situation 2 | overlap with wound-activation; recoverable as additional situation | was at emotions.md mandatory situations
- CUT  | BODY + VOICE as separate lines in situation block | budget pressure for C5 | was at emotions.md block format -- merged into SHOW
- CUT  | ACTION + HIDDEN as separate lines in situation block | budget pressure for C5 | was at emotions.md block format -- merged into DO
- CUT  | TRAP as separate line in situation block | budget pressure for C5 | was at emotions.md block format -- compressed into NEVER
= DEFENDED | Situation-based organization for emotions.md | survived likely DRIFT/BREAK from Straight: emotion-name headers violate anti-recitation | stays because the Intent Anchor demands scene-actionable rules, not psychology-indexed rules
= DEFENDED | No-quoted-words rule in voice.md | survived BREAK from Straight: "USE {signature words, quoted}" violates anti-recitation checklist | stays because the compile checklist item "zero listed catchphrases" requires it
= DEFENDED | Compile section length and prescriptiveness | survived likely DRIFT flag | aligned per Intent Anchor: the transformation engine IS the anti-recitation enforcement
~ ALIGNED | The final version serves the Intent Anchor by compiling encyclopedia data into situation-indexed, mechanics-only writing rules that fit a 140-line budget -- no quoted tics, no emotion labels, no physical inventory, no psychology vocabulary.
