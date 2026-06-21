# SAG Version — Birthday Gift Build Plan

> A personalized fork of **Pokémon Polished Crystal**, built as a birthday present for
> **Shane Austin Gaer (SAG)**.
> This document is the living source of truth. As details come in, they get logged here,
> then implemented and checked off.

- **Recipient:** Shane Austin Gaer ("SAG")
- **From:** _(to be filled in)_
- **Base:** Polished Crystal v3.2.3 (pokecrystal disassembly)
- **Working branch:** `claude/polished-crystal-fork-s4rysf`
- **Started:** 2026-06-21

---

## Status Legend
- [ ] Not started
- [~] In progress
- [x] Done & verified

---

## Phase 0 — Project setup & tracking
- [x] Create this tracking document
- [ ] Decide final ROM name / branding strings (Makefile `NAME`, `VERSION`, `AUTHOR`)

## Phase 1 — Build toolchain (so we can produce a playable ROM)
- [ ] Install build deps (make, gcc, bison, libpng, pkg-config)
- [ ] Install **RGBDS v1.0.1** (required; `.rgbds-version` = 1.0.1, source enforces v1.0.0+)
- [ ] Verify a clean **baseline** build produces `polishedcrystal-3.2.3.gbc`
- [ ] Confirm the ROM runs (sanity: file size / header correct)

## Phase 2 — Personalization (the gift) — DETAILS BELOW
Implemented from the "Personalization Details" section as Shane provides them.
- [ ] Branding / title
- [ ] Intro speech
- [ ] Default names
- [ ] In-game personal messages / NPCs
- [ ] Credits dedication
- [ ] Any custom characters / events / Pokémon / teams

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

### Inside jokes / references / personal touches
_(awaiting details)_

### Credits / dedication message
_(awaiting details)_

### Regions — add Hoenn & Sinnoh (on top of Kanto + Johto)  ⚠️ MAJOR SCOPE
- Want: full **Hoenn** and **Sinnoh** regions added as an expansion on top of the existing
  Kanto + Johto world.
- **Reality check:** this is by far the biggest item — each region = dozens of maps, new
  tilesets/graphics, wild encounter tables, NPC/event scripts, warps, town map data, story
  hooks, music, etc. A full faithful Hoenn+Sinnoh is hundreds of hours and would dwarf the rest
  of the gift. Worth scoping deliberately so the birthday build actually ships.
- **Options to choose from (pick scope):**
  1. **Teaser/MVP:** add 1–2 iconic locations per region (e.g., a Hoenn route + town, a Sinnoh
     route + town) reachable via a new portal/ferry — proves the expansion, ships on time.
  2. **Partial region:** one full region's early-game arc (e.g., Hoenn start area) now, expand later.
  3. **Full both regions:** treat as a long-term ongoing project beyond the birthday deadline.
- Pragmatic approach regardless: add a connection point (ferry/portal) from the existing world,
  then build region maps incrementally. New maps need: `maps/*.asm` + map header registration,
  `data/maps/`, tileset/blockset gfx, encounter data, town map updates.
- **DECISION NEEDED from you:** which scope above (1/2/3)? (Defaulting to teaser/MVP unless told.)

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
