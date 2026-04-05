# Bible Compilation Instructions

This note defines how HBOx should store and use source-lore material that is broader than any single prompt file.

The goal is:

- keep lore, world rules, origin myths, and recurring callback material out of ad hoc prompt rewrites
- make new bible material reusable across scene seed, behavior, continuity, sequel, and opener prompts
- give Codex a repeatable process for compiling raw lore into prompt-ready context

## Folder Rule

Bible material should live at:

`Vault/<Show>/Bibles/`

Not inside:

- `Prompts/`
- `Inputs/`
- `Outputs/`

Reason:

- `Prompts/` is for runtime prompt contracts
- `Inputs/` and `Outputs/` are traces
- `Bibles/` is source material

## What Belongs In `Bibles`

`Bibles` is for persistent material that may need to feed multiple prompts.

Examples:

- show premise
- world history
- institution rules
- origin myths
- timeline notes
- character clusters
- set bibles
- recurring company legends
- callback material
- contested lore
- event reinterpretations

## What Does Not Belong In `Bibles`

- parser instructions
- line-format requirements
- one-off scene requests
- generated inputs or outputs
- prompt text whose job is purely runtime formatting

## Suggested Bible File Types

Not every show needs every file, but these are the useful categories.

| File | Purpose |
| --- | --- |
| `Show Bible.md` | Core premise, tone, engine, status-quo rules |
| `World Bible.md` | Institutions, metaphysics, social rules, historical frame |
| `Story Engine.md` | How episodes regenerate pressure |
| `Roster Bible.md` | Character layers, clusters, recurring dynamics |
| `Set Bible.md` | What locations are for, not just what they are called |
| `Lore.md` | Myths, origin stories, jokes, fake callbacks, recurring bits |
| `Timeline.md` | Major events and show-specific chronology |
| `Historical Reinterpretations.md` | Alternate-history or show-specific event versions |
| `Compilation Notes.md` | Show-specific instructions for how to use these files in prompts |

## Core Compilation Principle

Do not dump a whole bible into every prompt.

Compile only what a prompt stage actually needs.

The compilation flow should be:

1. read source bible material
2. classify each note by function
3. extract only the relevant slices for the target prompt stage
4. compress the result into prompt-ready context
5. preserve runtime prompt clarity

## Bible Function Labels

When adding new material, classify it into one or more of these:

| Label | Meaning |
| --- | --- |
| `World` | Persistent setting truths |
| `Institution` | Rules of companies, empires, ships, states, buildings |
| `Character` | Stable wants, fears, methods, myths, bits |
| `Plot State` | What is currently true in the serial present |
| `Set` | Social function of locations |
| `Lore` | Stories people retell, myths, fake callbacks, origin myths |
| `Tone` | House style, joke boundaries, mouth-feel |
| `Event` | Historical or world events that shape current assumptions |

## Stage-to-Bible Map

This is the default compilation target for existing HBOx prompt stages.

| Prompt stage | Pull from bible |
| --- | --- |
| `Defaults.md` scene seed | `Show`, `World`, `Tone`, light `Plot State`, light `Set` |
| `Behavior Generation` | `Character`, `Institution`, current `Plot State`, light `Lore` |
| `Editor Process` | `World`, `Institution`, `Set`, current `Plot State`, compiled character stances |
| `Dialogue Generation` | compiled scene spine, `Tone`, light `Lore` |
| `Memory Generation` | current `Plot State`, relevant `Character` priors |
| `Episode To Episode Continuity` | `Institution`, `Plot State`, `Event` |
| `Sequel Generation` | `Story Engine`, `Plot State`, light `Lore` |
| `Openers` | `Tone`, `Lore`, `Character`, `Event`, `Story Engine` |

## Codex Compilation Process

When new bible material is added, Codex should follow this process:

1. Read the new bible note.
2. Decide which function labels it belongs to.
3. Decide which prompt stages should inherit it.
4. Summarize the note into small prompt-ready claims, not full prose dumps.
5. Update the minimum number of prompt files necessary.
6. If the note is broad and persistent, prefer updating show-level prompts or adding a dedicated compiled note instead of copying the same paragraph everywhere.

## Compression Rule

Bible prose is source material.
Prompt prose is compiled material.

That means:

- source lore can be rich, funny, and expansive
- compiled prompt context should be short, sharp, and functional

Example:

Source lore:

- Germany threw a rave in France's basement
- everyone joined it
- Soviet Union came back from Central Asia and discovered all his girls had gone to Germany's rave

Compiled prompt use:

- Germany treats conquest like a decadent house party everyone was too tempted to leave
- Soviet Union carries humiliation from returning late to an already-stolen war
- Britain and America remember the alliance less as virtue than as a temporary anti-rave coalition

## Show-Specific Use

### `polbots`

`Bibles` is especially useful for:

- alternate-history event summaries
- geopolitical mythology
- recurring bloc logic
- how historical figures and state-characters reinterpret major wars

### `AppyDays`

`Bibles` is especially useful for:

- company origin myths
- naming stories
- fake callback material
- coworking-space lore
- what the company says it is versus what it actually is

### `RomeBots`

`Bibles` is especially useful for:

- dynastic timeline notes
- status rules
- marriage/death/succession pressures
- reusable Roman social assumptions

### `SpaceDrivel`

`Bibles` is especially useful for:

- ship mythology
- anomaly interpretations
- command structure
- unresolved prior incidents

## Compilation Notes File

Each show can optionally include:

`Vault/<Show>/Bibles/Compilation Notes.md`

Use this for show-specific instructions like:

- what lore is allowed to stay contradictory
- what counts as canon
- what gets treated as rumor
- what kind of callback material is encouraged
- what should never dominate prompt space

## Practical Rule For Lore

If a piece of lore would help in more than one runtime prompt, it belongs in `Bibles`.

If it only matters to one output format, it probably belongs in `Prompts`.

## Bottom Line

`Bibles` should become the source layer.
`Prompts` should become the compiled runtime layer.

Codex should not treat those as the same thing.
