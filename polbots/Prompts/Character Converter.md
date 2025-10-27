You are rewriting a verbose description of a _polbots_ character (which could be a **nation, NGO, rebel group, corporation, or cultural bloc**) into a **concise, behavior-driven card** that LLMs can use to generate dialogue and character beats.  

The new card must be:

- **performative, not narrative** (written in imperative voice);
- **Obsidian-compatible** (tags and wiki-links);
- **≤ 220 words**, clear, and modular.

**Entity:** `{0}` 
**Pronouns:** `{2}`
**Old Card (.md):**

```
{1}
```

---

## Output Format (emit exactly this structure)

### {0} ({2})

**Tags:** #type/{infer type, state, NGO, corp, bloc, breakaway} #region/{infer primary region} #ideology/{infer or none} #role/{empire, former colony, client state, non-aligned, union, energy hub, island, landlocked, private} #tone/{dry, grandiose, snarky, earnest ironic, etc} #humor/{gallows, deadpan, absurd, self-deprecating, nationalist irony} #tempo/{rapid, measured, clipped} #trait/{1-2 key traits}  
**Relations:** [[insert ally name]], [[insert rival name]], [[insert partner name]], [[insert mentor name]], [[insert client name]], [[insert ancestor name]]

#### Core Persona

> Act as a {one-sentence archetype in imperative voice}. Prioritize {2-3 instincts or values}.

#### Voice & Demeanor

- **Tone:** {phrase}
- **Rhythm:** {fast/slow/clipped}
- **Register:** {formal/casual/mixed}.
- **Speech markers:** {3-4 concrete tells: jargon, dialect, idioms, code-switching}.
- **Conflict response:** {choose: deflect, escalate, reframe, placate, guilt-trip}.
- **Interest/hobbies**: {1-3 items and activities unique to local culture}.

#### Drives & Instincts (3-5)

- Protects...
- Proves...
- Distrusts...
- Seeks...
- Avoids...

#### Relational Behavior (4-6)

- **With [[insert ally name]]:** {banter or leverage cue}.
- **With [[insert rival name]]:** {pressure or taunt cue}.
- **With [[insert partner name]]:** {cooperative but self-interested cue}.
- **With [[insert mentor name]]:** {admiring-but-resentful dynamic}.
- **With [[insert client name]]:** {condescending or protective dynamic}.
- **With [[insert ancestor name]]:** {ancestral gag or callback}.

#### Running Gags (2-4)

- {short gag ≤ 8 words}
- {short gag ≤ 8 words}
- {optional}

#### Example Beat (≤ 3 lines)

> {0}: “{in-voice line}”  
> insert counterpart name: “{pushback line}”  
> {0}: “{button/turn line}”

### TL;DR

Act as **{0}**, a **{concise archetype}**.  
Speak {tone/rhythm}.  
Default tactics: {two verbs}.  
Core tensions: {two themes}.  

---

## Rules

**Compression & Focus**

- Entire card ≤ 220 words.
- No lore or timelines. History = _instincts_.
- Use **imperatives**, not adjectives.

**Tags & Links (Obsidian-compatible)**

- Tags: `#namespace/value` (no spaces). Aim for 6-9.
- Relations use wiki-links `[[Name]]`.
- Keep 3-8 high-signal relations ordered by importance.

**Behavioral Specificity**

- “Speech markers” = real linguistic quirks.
- “Relational Behavior” = one-line if-rules (style + tactic).
- “Running Gags” = repeatable comedic hooks.

**Safety & Tone**

- Satire ≠ slander. Punch up.
- If sensitive material appears, distill it to motives, not trauma.

**Inference**

- Use provided pronouns `{2}`; if unclear, default they/them.
- Infer region, ideology, and type reasonably; never output “unknown”.

**Output Hygiene**

- Output **only** the markdown card, nothing else.
- Preserve heading levels and punctuation exactly.

---

### Validation Checklist

-  ≤ 220 words
-  6-9 tags using `#namespace/value`
-  3-8 wiki-linked relations
-  3-5 drives + 4-6 relations + 2-4 gags
-  Example beat ≤ 3 lines
-  No redundancy across sections