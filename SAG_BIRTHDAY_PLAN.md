# SAG Version — Birthday Gift Build Plan

> A personalized fork of **Pokémon Polished Crystal**, built as a birthday present for
> **Shane Austin Gaer (SAG)**.
> This document is the living source of truth. As details come in, they get logged here,
> then implemented and checked off.

- **Recipient:** Shane Austin Gaer ("SAG")
- **From:** _(to be filled in)_
- **Base:** Polished Crystal v3.2.3 (pokecrystal disassembly) — kept for its QOL & modern features
- **Working branch:** `claude/polished-crystal-fork-s4rysf`
- **Started:** 2026-06-21

### Base decision (2026-06-21)
Shane has already played Polished Crystal and loves the Gen 1/2 era. Considered switching to a
fresh base (vanilla `pret/pokecrystal`, Gen 1 `pokered`/`pokeyellow`, the 1997 `pokegold-spaceworld`
demo, or the open-source **Crystal Legacy** at `github.com/cRz-Shadows/Pokemon_Crystal_Legacy`).
**Decision: stay on Polished Crystal** — keep its quality-of-life and modern features as the
engine/foundation, and **build a fresh, personalized story & content layer "from the ground up"
on top of it.** The personalization is what makes it Shane's, not the base.

> Approach note: "from the ground up" content means we mostly **repurpose/replace** existing PC
> story, characters, and events with Shane-themed versions (which frees ROM space as we go),
> rather than only piling new data onto an already-98.8%-full ROM.

---

## Status Legend
- [ ] Not started
- [~] In progress
- [x] Done & verified

---

## Phase 0 — Project setup & tracking
- [x] Create this tracking document
- [ ] Decide final ROM name / branding strings (Makefile `NAME`, `VERSION`, `AUTHOR`)

## Phase 1 — Build toolchain (so we can produce a playable ROM)  ✅ DONE
- [x] Install build deps (make, gcc, bison, libpng, pkg-config)
- [x] Install **RGBDS v1.0.1** (built from source; `rgbasm v1.0.1`)
- [x] Verify a clean **baseline** build produces `polishedcrystal-3.2.3.gbc` (2 MB, exit 0)
- [x] Header/size sanity OK (md5 `4e53ffed7ab34d599276e68f7e4497ed`)

> ⚠️ **SPACE CONSTRAINT:** baseline ROM is **98.8% full** (only ~25 KB / 2 MB free).
> Adding large new content (many trainers, lots of dialogue, new maps) will require freeing
> space or it won't fit. Favor *edits/replacements* over *additions*; keep new text tight.

## Project scope (2026-06-21) — TOTAL STORY CONVERSION
Keep Polished Crystal's **engine, QOL, and modern features**. Rebuild the **entire content layer
from the ground up**, personalized for Shane:
- **Whole story rewritten** — new narrative, dialogue, characters, events, themes.
- **Game flow redone** — progression/order, key story beats, gym/badge or equivalent structure,
  pacing, where you go and why.
- **All trainers redone** — every trainer party (Gym Leaders, Elite Four, rivals, route trainers,
  bosses) re-tuned/re-themed; rosters, levels, items, AI as needed.
- Personal touches woven throughout (rival = Justin, courier Dragonite, champion cameos, baseball
  references, dedication, etc. — see details below).

> This is a big, ongoing build. We do it **incrementally and track every piece in this doc**, so
> the gift can ship in coherent milestones (intro + early game first, then outward).
> **Still needed from Shane's family (you):** the high-level STORY concept/premise and the new
> game flow (region order, who the key characters are, the central goal). Firehose welcome.

## ★ MASTER DIRECTIVE (2026-06-21): make it feel COMPLETELY NEW
Change **every piece of dialogue, every character, and every Pokémon** so nothing reads as stock
Polished Crystal. This is the largest possible content scope — effectively a full reskin + rewrite
on top of PC's engine. It's very doable but it's a marathon, so we work systematically and bank it
in milestones.

### Scale (so we plan realistically)
- **Dialogue:** thousands of text strings across `data/text/*.asm` + every `maps/*.asm` script.
- **Characters:** all NPCs/trainers — names, personalities, sprites where it matters.
- **Pokémon:** 391 species in PC. "Changed" can mean very different efforts — DECISION NEEDED:
  - **(A) Rename + re-flavor:** new species names + new Pokédex entries, keep existing sprites.
    Lightest; ships fastest; still feels new in dialogue/dex. *(Recommended starting point.)*
  - **(B) Rename + re-type/re-stat:** also change types/stats/movesets (data-heavy, no new art).
  - **(C) Full "fakemon":** new names AND new sprites/cries for all — massive art pipeline,
    needs sourced/created assets; realistically a long-term stretch goal, not the birthday build.

### Method (how we churn through it without drowning)
1. **Define the "bible" first:** the new world's theme, the renamed Pokémon list, and the cast of
   characters. Everything else references this for consistency. (Lives in this doc.)
2. **Work region-by-region, file-by-file:** rewrite text + scripts in batches, committing often.
3. **Trainers re-themed as we pass through each area** (ties into dialogue).
4. **Track coverage** with a checklist of text files / maps so we know what's done vs remaining.
5. Rebuild frequently to catch breakage early (text macros, character limits, name lengths).

### Coverage tracker (filled in as we go)
- [ ] World/theme "bible" written
- [ ] Pokémon rename list (species → new names)  — scope = (A/B/C) TBD
- [ ] Character/cast list
- [ ] Intro & New Bark / starting town
- [ ] (further areas added as we reach them)

## Phase 2 — Content rebuild (the gift) — DETAILS BELOW
Implemented from the "Personalization Details" section as details come in.
- [ ] Story rewrite (narrative, key dialogue, events)
- [ ] Game flow / progression redesign
- [ ] All trainers re-themed & re-tuned
- [ ] Branding / title
- [ ] Intro speech
- [ ] Default names (rival = Justin)
- [ ] In-game personal messages / NPCs
- [ ] Credits dedication
- [ ] Custom characters / events / Pokémon (courier Dragonite, champion cameos)

## Phase 3 — Build, verify & deliver
- [ ] Rebuild the personalized ROM cleanly (no errors)
- [ ] Commit & push all changes to the working branch
- [ ] Deliver the playable ROM file

---

## Personalization Details (Shane's firehose — captured here)

> Everything Shane wants in the game gets logged under the right heading.
> Nothing is implemented until it's written down here first.

### Branding / Title screen
_(awaiting details)_

### Player / Rival / character names

**Rival → "Justin"**
- Default rival name = **Justin** (instead of "Silver").
- **Very short** → swap his overworld sprite (and ideally battle sprite) to a shorter/smaller
  character model. Implementation: point the rival to an existing short sprite (e.g. a youngster/
  kid-sized overworld sprite) rather than drawing new art, unless custom art is wanted.
- **Napoleonic complex** → rewrite his battle/encounter dialogue so he's arrogant, hot-tempered,
  and overcompensating — constantly asserting dominance, touchy about his height, big talk.
- Files: name default in `engine/events/specials.asm`; rival overworld/battle sprite assignment
  (TBD — locate rival sprite constant + gfx); rival dialogue across his battle scripts.

### Intro / new-game speech
_(awaiting details)_

### In-game messages, NPCs, signs, easter eggs
_(awaiting details)_

### Custom Pokémon / movesets / teams

**Shane's favorite: DRAGONITE — the "courier Dragonite" from Pokémon: The First Movie**
- The Dragonite that delivers Mewtwo's invitation letter at the start of the first movie.
- Goal: make **this specific Dragonite obtainable as a one-off (single, unique) encounter.**
- Implementation ideas (TBD):
  - A static/scripted one-time encounter (like the legendary/roaming static battles), not a
    wild-grass repeatable spawn — so it's a "deliver-the-letter" themed event.
  - Themed presentation: it arrives carrying a letter (tie the encounter script to a mail/letter
    item or a short cutscene), then can be caught/given.
  - Possibly give it a fitting moveset/level and maybe a held Mail item as a nod to the movie.
  - Location: TBD (somewhere meaningful / discoverable).
- Files (to locate during impl): static encounter / special wild battle scripts, a map script for
  the event, Dragonite species data, mail/item data if we include the letter.

### Guest characters from other regions (Champions / Gym Leaders)
- Include cross-region notables as encounterable NPCs/trainers, e.g.:
  - **Cynthia** (Sinnoh Champion)
  - **Wallace** (Hoenn Champion / Sootopolis leader)
  - **Steven Stone** (Hoenn Champion)
  - **etc.** — more to be named (Lance & Red already exist in base game).
- Implementation: add them as battleable trainers / cameo NPCs. Each needs a trainer-class +
  party definition, overworld sprite, and placement/dialogue script. Naturally pairs with the
  Hoenn/Sinnoh expansion (they can headline those regions), but cameos can also be dropped into
  the existing world as special post-game battles.
- Files (to locate): trainer party data (`data/trainers/`), trainer class constants, overworld
  sprites, and map event scripts for placement.

### Inside jokes / references / personal touches

**Shane = high school baseball player**
- Weave baseball references in: e.g., player's bedroom could have a baseball/bat decoration or a
  trophy with custom flavor text; an NPC could reference his playing days; a sign or the TV could
  mention a game. Trainer flavor / dialogue can use baseball metaphors ("swing for the fences!").
- Possible nods: a "home run" themed moment, baseball cap on the player sprite (stretch — sprite
  edit), or a held item / gift item framed as a "lucky bat/ball."

### Credits / dedication message
_(awaiting details)_

### World structure — ONE big unified region, 16 Gym Leaders (2026-06-21)
- **Want:** axe the separate Johto/Kanto identity and present **one big continuous region** with a
  single **16-gym** progression.
- **Why it fits:** Polished Crystal already has **16 badges** (8 Johto + 8 Kanto) and the engine
  supports that whole progression — so we reuse the 16-gym backbone and re-theme it as one region.
- **Keep the FULL area:** retain the entire landmass of both Johto **and** Kanto (all existing
  maps/routes/towns stay) — we want that big explorable world. We're not shrinking it, just
  unifying it. ~2 regions' worth of area = one large region.
- **Pragmatic build (feasible for the gift):** keep the existing map *geometry/connections* but
  **re-skin and re-narrate** them into one cohesive new region — new region name, new town/route
  names, unified town map narrative, one continuous journey across all 16 gyms, no "fly to Kanto"
  region break in the story. Re-theme the 16 Gym Leaders into our new cast.
- **Heavy/stretch version:** draw brand-new map layouts + custom tilesets from scratch (huge art
  task). Default to re-skin-and-reflow unless we decide to invest in new geometry.
- Cross-region champions (Cynthia/Wallace/Steven, etc.) → fold into the new cast as Gym Leaders,
  Elite Four, or special battles within the one region.

### Hoenn & Sinnoh new regions ❌ DESCOPED — superseded by the single unified region above.

---

## Known customization hook locations (researched)
For reference when implementing — exact spots in the codebase:

| What | File | Notes |
|------|------|-------|
| ROM name / version / author | `Makefile` (lines 1–15) | `NAME`, `VERSION`, `AUTHOR`; `COPYRIGHT` string also shows in-game credits |
| Title screen text/graphics | `engine/movie/title.asm`, `gfx/title/` | "POLISHED CRYSTAL" tilemap @ ~line 64; logo/version/crystal art are LZ-compressed 2bpp |
| Default player names | `data/player/default_names.asm` | Chris/Kris/Crys/Krys by gender |
| Default rival name | `engine/events/specials.asm` | "Silver" |
| Intro speech (Prof. Elm) | `data/text/common.asm` | `_ElmText1`–`_ElmText7` (~lines 3160–3240) |
| Starting bedroom (interactables) | `maps/PlayersHouse2F.asm` | PC, Radio, Journal, Poster — good for a custom note |
| Mom's house (1F) | `maps/PlayersHouse1F.asm` | Mom dialogue, TV, fridge, etc. |
| Credits sequence | `data/credits_script.asm`, `engine/movie/credits.asm` | natural spot for a dedication |

---

## Build notes / log
- Environment: Linux, has make/gcc/git/python3. RGBDS **not** preinstalled — must build v1.0.1 from source.
- _(build results logged here as we go)_
