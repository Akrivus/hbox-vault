# AppyDays Prompt Change Map

This note compares the current `AppyDays` prompts to the revised show bible in [AppyDays Show Bible](C:/Users/akriv/OneDrive/Desktop/HBOx/Vault/AppyDays%20Show%20Bible.md).

The short version:

- the current prompts are good at startup-pressure one-shots
- they are weaker at founder structure, coworking ecology, and ongoing serial status changes
- the existing actor prompts are usable, but some roles need reframing

## What Already Works

These parts already fit the new model reasonably well:

| Prompt | Keep | Why |
| --- | --- | --- |
| `Vault/AppyDays/Prompts/Defaults/Behavior Generation.md` | mostly keep | It already asks for repeatable workplace tactics instead of one-off jokes. |
| `Vault/AppyDays/Prompts/Defaults/Editor Process.md` | keep structure, revise content | It already builds a scene spine rather than jumping straight to dialogue. |
| `Vault/AppyDays/Prompts/Defaults/Dialogue Generation.md` | mostly keep | It already has the right mouth-feel: panic hidden in professional language. |
| `Vault/AppyDays/Prompts/Defaults/Episode To Episode Continuity.md` | keep stage, revise focus | The stage is correct even if the current continuity model is still a bit generic. |
| actor prompt format | keep | The format is already good for pressure-profile characters. |

## Main Problems In The Current Prompt Stack

| Area | Current issue | Why it matters |
| --- | --- | --- |
| `Defaults.md` | Startup tone is present, but the company itself is still abstract | The show needs a more specific social machine: tiny founder-led company inside a coworking space |
| founder logic | Current cast language does not clearly establish Clive + Noah as the core founder pair | The show engine depends on that pairing |
| company size | The current prompts imply a larger generic office ensemble | The revised show wants fewer than ten real insiders |
| coworking ecology | The current prompts do not strongly foreground the larger shared-space world | This is a major source of pressure and exposure |
| role boundaries | Gideon currently reads like CEO, Janine like HR Director | The revised show wants Gideon as investor pressure and Janine as space-management authority |
| serialization | Current prompts can sustain scenes, but not yet a clear episode engine where the company survives by mutating its obligations | That is the show's new core loop |
| location logic | Prompts ask for a real office location but do not yet encode what each location is good for | Set selection is still too arbitrary |

## Prompt-By-Prompt Changes

## 1. `Vault/AppyDays/Prompts/Defaults.md`

### Current job

Scene seed generator for startup chaos.

### Needed changes

- define AppyDays as a tiny app company in a larger coworking environment
- emphasize the founder/company split:
  Clive pressures, Noah systems, everyone else gets trapped in the gap
- replace vague scale ambiguity with concrete mismatch:
  too small for this, not thinking big enough, please let us work
- bias scene seeds toward incoming organizational pressure rather than generic meltdown
- encourage selection of outsiders when appropriate:
  investor, client, candidate, building management, neighboring tenant

### Add pressure sources such as

- investor drop-in
- client demand
- candidate interview
- coworking conflict
- impossible promise coming due
- product or infra failure

## 2. `Vault/AppyDays/Prompts/Actors/*.md`

### Keep

The pressure-profile format.

### Revise

- `Clive.md`
  shift from finance-only framing to business founder who turns fantasy into cost and systems demand
- `Noah.md`
  strengthen founder/operator identity; make him less purely "technical truth guy" and more "hunch-driven product builder who still collides with reality"
- `Sal.md`
  keep strong; maybe sharpen his status as best engineer and material reality check
- `Felicity.md`
  keep role, but let her dynamic with Noah be present as origin texture, not romance bait
- `Ivy.md`
  shift from QA-only if needed toward junior dev / recently hired intern who is structurally in Noah's orbit
- `Gideon.md`
  recast from CEO to investor / narrative escalator
- `Janine.md`
  recast from HR Director to coworking or building operations authority
- optional prune or demote some roster members into external orbit if the company should stay small

## 3. `Vault/AppyDays/Prompts/Defaults/Behavior Generation.md`

### Keep

- repeatable workplace animal framing
- tactic over biography
- office language disguising damage

### Add

- whether this character is acting as founder, builder, coordinator, investor, outsider, or witness in this scene
- what small-company pressure they feel right now
- what private dependency or role ambiguity they are defending
- how the coworking/public nature of the scene changes their tactic

This prompt should stop thinking of everyone as equal coworkers and start thinking in layers:

- company insiders
- company orbit
- building orbit

## 4. `Vault/AppyDays/Prompts/Defaults/Editor Process.md`

### Keep

- scene-spine structure
- surface problem vs hidden problem framing
- power move / misread / shift logic

### Change

Make the scene engine explicitly track:

- what the company thinks it is doing
- what it actually has the capacity to do
- who is trying to narrate scale
- who is trying to force operational reality
- how the room's privacy is compromised by the coworking environment

This prompt should become less "generic startup chaos" and more "small company pretending to be institution."

## 5. `Vault/AppyDays/Prompts/Defaults/Dialogue Generation.md`

### Keep

Most of it.

### Tighten toward

- founder/builder asymmetry
- dependency and rank
- people speaking as if they represent a larger company than they do
- office language used as access control, not just panic cover
- scenes that end with a commitment, ownership shift, or dependency exposed

This prompt is already close.

## 6. `Vault/AppyDays/Prompts/Defaults/Episode To Episode Continuity.md`

### Current state

Generic serial office continuity.

### Change

Track items like:

- promises made to investors or clients
- who now owes whom
- role changes nobody announced
- which lies are still active
- what the larger coworking space now knows
- which outsider now has leverage over the company

Continuity should care less about generalized office gossip and more about obligation, exposure, and headcount-scale fragility.

## 7. `Vault/AppyDays/Prompts/Openers/*.md`

### Current state

Usable thematic one-shot starters.

### Change

Future openers should target recurring AppyDays entry patterns:

- investor energy
- candidate exposure
- client overreach
- space-management conflict
- founder disagreement
- fake after-hours casualness becoming a real work crisis

## Set Prompting Changes

Locations should stop being treated as interchangeable office boxes.

Each core set should have a dramatic job.

| Target set | Best for |
| --- | --- |
| Suite A | founder strategy, spin, bad commitments, closed-door status fights |
| Suite B | technical reality, shipping pressure, implementation conflict |
| Common Area | overheard conversations, fake casualness, coworking exposure |
| Hallway | interception, damage control, accidental witnesses |
| Reception | access, embarrassment, scheduling, building authority |

Prompt implication:

Location selection should be based on conflict type, not just capacity.

## Suggested Order Of Prompt Work

1. Rewrite `Defaults.md`
2. Recast key actor prompts:
   `Clive`, `Noah`, `Sal`, `Felicity`, `Ivy`, `Gideon`, `Janine`
3. Update `Editor Process.md`
4. Update `Episode To Episode Continuity.md`
5. Revisit `Openers/`
6. Only then decide whether new act or sequel scaffolding is needed

## Immediate Safe Changes

These can be done without touching runtime code:

- tighten the world bible in `Defaults.md`
- redefine founder and investor roles in actor prompts
- make Janine a building authority
- shift continuity toward obligation and exposure
- reduce prompts' assumption that everyone is an internal employee

## Changes That Can Wait

- adding act-specific sequel prompts for AppyDays
- codex expansion for founder/investor/building relationships
- location taxonomy files if you decide to formalize set bibles later

## Bottom Line

The current `AppyDays` prompts are not broken.

They are just still aimed at:

- startup one-shots
- generalized office dysfunction
- ensemble chaos

The revised show bible wants:

- a very small founder-led company
- a strong coworking ecology
- recurring pressure from outsiders and promises
- scenes about scale mismatch, dependency, and premature organizational identity

That is mostly a prompt rewrite problem, not a runtime problem.
