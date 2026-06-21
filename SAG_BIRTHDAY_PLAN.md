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
- **Pokémon — RESOLVED (2026-06-21):** keep the **same Pokédex** (all existing species, sprites,
  cries, dex). "New Pokémon" means **re-cast which Pokémon appear situationally**:
  - different **starters**, different **legendaries** (and their encounter events),
  - re-chosen **wild encounter tables** per area,
  - **every opponent's team** rebuilt (rivals, gym leaders, E4, route trainers, bosses).
  - No species renames, no new sprites/fakemon. This keeps it light + ships on time.
  - **CASTING RULE:** the Pokémon chosen must be **on-theme with the opponent's persona AND the
    location.** Examples: baseball coach → hard-hitting Fighting/athletic mons; "Russian spy" →
    sneaky Poison/Dark; Grandma Linda → sweet-but-tough Fairy/old-school mons; frat brother →
    rowdy/"party" mons; gritty NYC streets → urban mons (Rattata, Grimer/Muk, Pidgey, Meowth);
    Yankee Stadium → flashy heavy hitters. Starters & legendaries likewise picked to fit the
    story beat where they're obtained.

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

## ★ WORLD BIBLE — "NYC / NY SUBURBS" THEME (Shane's life as a region)
The unified region = **Shane's life journey**, centered on **New York City**, radiating out to the
suburbs (NJ, Long Island) and his later life travels (Philadelphia, Atlanta, Bradenton FL).
Early game leans hard into the **NYC / NY-suburbs** vibe. Player = **Shane** (the hero).

### Locations → map roles (DRAFT — to refine into towns/routes/gyms)
**NYC core (heart of the region):**
- **West Village** — *later childhood home*; **MOM & DAD live here.** → strong "home town"
  (the New Bark / player's-house analog where the adventure begins).
- **Upper East Side** — *early-childhood memories sprinkled here*; home of **The Town School**
  (Shane's UES school). Nostalgic early-game town/district.
- **Randalls Island** — *baseball* fields (early-childhood baseball). → park/route w/ baseball NPCs.
- **Hudson Yards** — Shane's **current home** & **THE STARTING POINT**: his **1-bedroom apt on the
  28th floor (apt C)**. Same building as his **brother**. **Jared** = neighbor in **apartment 11I,
  floor 11**. → sleek modern city hub; the game opens here (New-Bark/player's-room analog).
- **Williamsburg, Brooklyn** — younger sister **Cali** (at **Brooklyn Law School**).
- **Central Synagogue (NYC)** — landmark; key building/event (bar-mitzvah-era memory?).
- **Sidley Austin law firm (NYC)** + **John Altorelli** & **"the Russian spy" he dated** —
  law-internship storyline NPCs.
- **Underage bars (NYC)** — nightlife flavor NPCs / hidden spots.
- **Riverdale Country School (NYC/Bronx)** — another school location.

**Sports venues (prime GYM / arena candidates):**
- **Yankee Stadium (Bronx)** — baseball → top gym candidate (ties Shane's HS baseball).
- **Madison Square Garden (MSG)** — arena/gym candidate.
- **Barclays Center (Brooklyn)** — arena/gym candidate.
- **IMG Academy (Bradenton, FL)** — sports academy → athletics gym candidate.

**NY suburbs / tri-state:**
- **Paramus (NJ)** — **Grandma Linda's** home; the **3 crazy uncles** (dad's brothers):
  **Matt & Jason (twins)** + **Donut (short, Napoleon complex)**.
- **Old Brookville (Long Island)** — mother's parents' home; **grandparents are deceased** →
  handle tenderly (memorial / remembered place, NOT a battle gag).

**College / later-life journey (farther region areas):**
- **University of Pennsylvania, School of Arts & Sciences (Philadelphia)** — **APES** frat; beer
  with friends.
- **Emory University Law School (Atlanta)** — drank beer with friends (girls & guys).
- **Camp Pontiac (NY)** — summer camp; nostalgic woods/lake route.

### Cast
| Person | Role in game | Placed at |
|--------|--------------|-----------|
| **Shane** | Player / hero | starts West Village |
| **Justin** | **Rival** — short, Napoleon complex | follows Shane's journey |
| **Mom & Dad** | Parents (home NPCs) | West Village |
| **Cali** (younger sister) | Family NPC (law student) | Williamsburg / Brooklyn Law |
| **Brother** (the gift-giver) | NPC — same Hudson Yards building | Hudson Yards |
| **Jared** | NPC — same building, apt **11I** (age 11?) | Hudson Yards |
| **Grandma Linda** | Family NPC | Paramus |
| **Uncle Matt** & **Uncle Jason** | Twins, "crazy uncles" | Paramus |
| **Uncle Donut** | Short, Napoleon complex (cf. Justin) | Paramus |
| Maternal grandparents | Remembered (deceased) — respectful memorial | Old Brookville |
| **John Altorelli** | Law-internship character | Sidley Austin, NYC |
| "The Russian spy" | Quirky law-internship NPC (he dated) | Sidley Austin, NYC |

### Locked decisions (2026-06-21)
- **Start point:** Hudson Yards, Shane's 1-bedroom apt, **28th floor (apt C)**. ✅
- **Tone:** **FULL ROAST** — lean into the underage bars, law-internship, Russian-spy, short-uncle
  jokes, etc. Comedic and irreverent. (Still handle deceased grandparents respectfully.) ✅
- **Jared:** neighbor in the same building, **apartment 11I, floor 11**. ✅
- **Pokémon:** same Pokédex; re-cast starters/legendaries/encounters/opponent teams. ✅

### Still open
- **16 Gym Leaders & the ladder** — UNDER DISCUSSION (see draft below). Need: who leads each gym,
  the Elite Four + Champion, and the final secret superboss (Red analog).

## ★ 16-GYM LADDER — DRAFT FOR DISCUSSION (2026-06-21)
Structure inherited from PC (so we re-skin, not re-engineer): **Gyms 1–8 → Elite Four + Champion
(mid-game) → Gyms 9–16 → secret final superboss (Red analog).** Types are PC's existing gym types
by default (changeable later); we swap in new leaders, teams, and all-new dialogue. Journey flows
**Hudson Yards → NYC/boroughs → NJ/LI suburbs → (E4/Champ) → college & later-life arc → finale.**

### Act I — NYC & suburbs (Gyms 1–8)
| # | Location | Leader (draft) | PC type slot | Roast / hook |
|---|----------|----------------|--------------|--------------|
| 1 | Hudson Yards (his building) | **Jared** (neighbor, 11I) | Flying | pushover first gym, the weird neighbor |
| 2 | The Town School (UES) | a **schoolteacher** | Bug | grade-school throwback |
| 3 | West Village | **Mom** (or Dad) | Normal | the "you'll cry" mom gym |
| 4 | Central Synagogue | a **rabbi/cantor** | Ghost | bar-mitzvah-era mysticism (respectful + funny) |
| 5 | Randalls Island | **baseball coach** | Fighting | Shane's HS baseball; "swing for the fences" |
| 6 | Williamsburg / Barclays | **Cali** (sister) | Steel | law-student sis, ice-cold prep |
| 7 | Bronx / **Yankee Stadium** | a **Yankees legend** | Ice | the big-league stadium gym |
| 8 | Paramus, NJ | **Uncle Donut** (short, Napoleon) | Dragon | tiny man, biggest ego, "prestige" 8th gym |

### Mid-game — ELITE FOUR + CHAMPION (the family)
- **E4 (draft):** Uncle **Matt** & Uncle **Jason** (twins — back-to-back mirror battle), **Grandma
  Linda** (Paramus), **Dad**. Champion = **the Brother** (the gift-giver) — "beat your big bro."
- *(All swappable — your call on who's E4 vs Champion.)*

### Act II — College & later-life arc (Gyms 9–16)
| # | Location | Leader (draft) | PC type slot | Roast / hook |
|---|----------|----------------|--------------|--------------|
| 9 | UPenn / **APES** frat (Philly) | a **frat brother** | Rock | beer, frat-house chaos |
| 10 | Emory (Atlanta) | a **college friend** | Water | grad-school benders |
| 11 | **IMG Academy** (Bradenton FL) | an **elite coach** | Electric | intense athletic boot camp |
| 12 | a college crew spot | a **college girlfriend/friend** | Grass | the chill one |
| 13 | Sidley Austin (NYC) | **"the Russian spy"** | Poison | she's literally a ninja/spy — perfect fit |
| 14 | Sidley Austin (NYC) | **John Altorelli** | Psychic | mastermind lawyer boss |
| 15 | **MSG** | a **showman/Knicks legend** | Fire | the Garden, lights, ego |
| 16 | (final gym) | **Justin** (RIVAL) | Blue/mixed | rival runs the last gym, Napoleon complex |

### Finale — secret superboss (Mt. Silver / "Red" analog)
- Candidates: the **Brother** again as the hidden ultimate ("Red"), Shane's **future self**, or tie
  it to the **courier Dragonite** event. **TBD with you.**

### Discussion points for you
- Confirm/adjust each **gym leader** above (esp. gyms 7, 9–12, 15).
- Lock the **Elite Four** (4 people) + **Champion** (1).
- Pick the **secret final boss**.
- Want gym **types re-themed** to fit people (more work), or keep PC's types under new skins (faster)?
- Camp Pontiac, Old Brookville, Riverdale, IMG, bars — which are **gyms** vs **story towns/routes**?

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
