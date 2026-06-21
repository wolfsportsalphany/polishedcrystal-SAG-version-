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
  - **Shane's starting trio: Eevee + Level 1 Gastly + Level 1 Mankey** (all favorites). Gastly &
    Mankey owned at start; **Eevee gifted by Jared on floor 11** (the only obtainable Eevee).
  - different **legendaries** (and their encounter events),
  - re-chosen **wild encounter tables** per area,
  - **every opponent's team** rebuilt (rivals, gym leaders, E4, route trainers, bosses).
  - No species renames, no new sprites/fakemon. This keeps it light + ships on time.
  - **CASTING RULE:** the Pokémon chosen must be **on-theme with the opponent's persona AND the
    location.** Examples: baseball coach → hard-hitting Fighting/athletic mons; "Russian spy" →
    sneaky Poison/Dark; Grandma Linda → sweet-but-tough Fairy/old-school mons; frat brother →
    rowdy/"party" mons; gritty NYC streets → urban mons (Rattata, Grimer/Muk, Pidgey, Meowth);
    Yankee Stadium → flashy heavy hitters. Starters & legendaries likewise picked to fit the
    story beat where they're obtained.
  - **SHANE'S FAVORITE LINES — feature prominently:**
    - **Primeape line (Mankey → Primeape)** — give it a starring role: available/obtainable early
      and meaningfully (great fit for the baseball/Fighting/NYC-tough-guy vibe), showcased on key
      ally/opponent teams. A signature 'mon for Shane.
    - **Dragonite line (Dratini → Dragonair → Dragonite)** — already special via the **courier
      Dragonite** one-off event; lean into the line as a prestige/aspirational Pokémon.
    - **Haunter — SPECIFICALLY Haunter, not Gengar.** Shane loves Haunter itself; feature Haunter
      prominently (ace/ally/opponent), but **stop at Haunter** — don't push the Gengar evolution
      (Haunter is the star, the "perfect form" here).
  - **LEGENDARIES — use them AGAINST the player, don't hand them out:**
    - Shane doesn't love legendaries, so **the player generally can't obtain them** — instead the
      **second-half GYM LEADERS (gyms 9–16) and the ELITE FOUR field legendaries in their parties**
      as serious threats. Legendaries become intimidating opponent power, not collectibles.
    - **MEWTWO (+ Mew) are the deliberate exceptions** — catchable only via the Mewtwo Island arc
      (his favorite, earned through the *First Movie* climax). Concentrate player-obtainable
      legendary content into that one arc; keep others as enemies-only.
    - **★ ARMORED MEWTWO STORYLINE** — a central plot arc themed on *Pokémon: The First Movie*
      (Armored Mewtwo). Ties directly to the **courier Dragonite** event (the Dragonite that
      delivers Mewtwo's invitation letter) → one cohesive first-movie storyline: a mysterious
      letter/invite → tracking the experiments → confronting **Armored Mewtwo**.
    - *Art note:* the armor is a **custom sprite** (one-off). Doable as a single special asset;
      if art slips, fall back to standard Mewtwo sprite. (We otherwise avoid new sprites.)
    - **★ TWO-PHASE BOSS MECHANIC:**
      1. **Phase 1 — Trainer battle vs Armored Mewtwo:** fought as a *trainer*-controlled boss
         (so it can't be caught yet; armor = unbeatable-feeling, tuned tough).
         - **★ MIRROR TEAM:** Mewtwo's party is a **clone of the PLAYER's current team, each member
           +5 levels.** (On-theme: Mewtwo is a clone — it copies you.) *Impl: custom code that
           reads `wPartyMon` species/moves at battle start and builds the enemy party as copies at
           +5 levels — not a static party. Non-trivial engine work; flag for build phase.*
      2. **On defeat → cutscene:** the **armor breaks/shatters.**
      3. **Phase 2 — Wild Mewtwo battle:** immediately transition into a **wild** encounter with
         the now-unarmored Mewtwo → **the player can capture it.**
      - *Impl:* scripted trainer battle that, on victory, triggers a cutscene then starts a wild
        battle (engine supports scripted/forced wild encounters). Set Mewtwo's wild level/catch
        rate so it's a real (but fair) capture moment — the payoff of the whole arc.

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
| **Justin** | **Rival** — short, Napoleon complex; **owns a Pilates studio** he insists beats being a lawyer; first battle blocks the Sidley Austin entrance | follows Shane's journey |
| **Merrick** | **Justin's brother** — genuinely nice; warm foil to Justin's ego | helpful NPC; encourages Shane, maybe gives items/tips |
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
- **Gyms** = a lighter, SEPARATE layer (see below) — not built from the family. Leaders/types TBD.
- **Secret final boss** (Red analog) — TBD.

## ★ OPENING SEQUENCE — LOCKED & READY TO BUILD (2026-06-21)
The concrete first slice of the game (Act I start):

1. **Apt 28C, Hudson Yards** — Shane wakes up in his 1-bedroom apartment on the **28th floor**.
   Tutorial/room beat, then head out to the elevator.
2. **Elevator → 11th floor** — Shane takes the elevator **down to the 11th floor to visit his
   brother**. (Brother lives on floor 11; **Jared** is the neighbor in **apt 11I**.)
3. **CHANGED (2026-06-21): Shane starts with a full PARTY** (no single-Eevee gift). The party is
   pre-set at new-game start (see "Starting party" below). The **11th-floor visit becomes a
   send-off**: the **brother** sees Shane off (gives gear — Pokédex / Town Map / running shoes /
   key item), and **Jared** still gets a comedic bit.
   - **STARTING PARTY (confirmed 2026-06-21): Eevee + Level 1 Gastly + Level 1 Mankey.** All three
     of his favorites (Eevee + Haunter & Primeape lines). Gastly & Mankey are **Lv1**; Eevee level
     TBD (default low, e.g. Lv5 as a "found" mon — confirm if you want a specific level).
   - **Eevee delivery (keeps the jokes):** Shane already has Gastly + Mankey; **Jared hands over
     the Eevee on floor 11.** This preserves the **only obtainable Eevee**, Justin's **Eevee-mirror
     battle**, and the **"Jared said it's rare / that's why he wasn't invited to the wedding"** gags.
4. **Downstairs = Hudson Yards (explorable hub)** — the lobby/street level is the explorable
   **Hudson Yards** area. **Doormen NPCs: Robert, Eric, Jose, and Jonathon.** (Give each a distinct
   funny personality.)
5. **Route = TIMES SQUARE** — the "route" from Hudson Yards to the first gym is **Times Square** —
   **make it FUNNY**: costumed characters (knockoff Elmo/Spider-Man), the Naked Cowboy, aggressive
   flyer-handers, tourists blocking the path, ticket scalpers as "trainers," etc.
6. **FIRST RIVAL BATTLE — Justin** — right **before Shane first enters Sidley Austin**, **Justin
   runs up and blocks the entrance** and challenges him to a battle. In his intro he brags that
   he **owns a Pilates studio**, which (in his mind) is **way better than being a lawyer** — peak
   Napoleon-complex energy. (This is Shane's first encounter with the rival.)
   - **Justin's starter = an Eevee too**, and he sneers that **Jared was wrong — "it's actually
     not that rare."** (Rival-mirror battle: Eevee vs Eevee. Justin's Eevee is NPC-owned, so it
     doesn't break "Shane's is the only *obtainable* Eevee.")
   - Justin also snipes that **that kind of stupidity is exactly why Jared didn't get invited to
     his wedding.** (More rival roast fuel.)
7. **FIRST GYM = Sidley Austin law firm (Midtown)** — a **MULTI-STORY gym** (navigate floors of the
   office building, like an elevator/floor-puzzle gym). Set in Shane's corporate law firm.
   Leader likely **John Altorelli**; ties into the law-internship / "Russian spy" subplot.
   Full roast — billable hours, associates/paralegals as grunt trainers, conference-room battles.

> **Pokémon note:** **Eevee** = the opening gift / signature companion (only one in the game).
> Other "starters/legendaries" re-cast per the casting rule. NOTE: this moves **Sidley Austin from
> the late-game law tower to GYM #1** — gym layout/order is being driven by the real-life flow now.

## ★ DESIGN PRIORITY (2026-06-21): build the WORLD from Shane's life
**Use the biographical info to build the TOWNS, MAPS, and STORIES — not as a gym-leader roster.**
The real places become the region's towns/areas; the real people become the **resident NPCs and
storylines** living in them; real events (baseball, frat, law internship, the Russian spy, the
crazy uncles) become **quests/story beats**. Gyms sit on top as a separate, lighter progression.

### Region towns & story beats (the heart of the build)
Re-skin PC's existing maps into these NYC/NY-themed towns; each carries its real-life vibe,
resident NPCs, and a personal story beat. (Order = rough travel flow from the start.)

| Town / area (re-skin of PC map) | Real-life vibe | Resident NPCs | Personal story beat (full roast) |
|---|---|---|---|
| **Hudson Yards** (START) | glass high-rises, adult life | **Brother** (floor 11), **Jared** (apt 11I); doormen **Robert, Eric, Jose, Jonathon** | wake in apt 28C → elevator to fl 11 → Jared gifts **Eevee** → explore Hudson Yards lobby/street |
| **Times Square** (Route 1) | tourist-trap chaos | costumed characters, Naked Cowboy, scalpers | the funny "route" from Hudson Yards to the office — see Opening seq. |
| **West Village** | brownstone childhood home | **Mom & Dad** | the family home; parents send you off / give gear |
| **Upper East Side** | posh; **The Town School** | childhood friends, teachers | grade-school throwback; earliest memories |
| **Randalls Island** | real explorable ballfields/park island | baseball teammates/coach | Shane's HS baseball; a "big game" event; fishing off the water |
| **Central Park** | big iconic green expanse | joggers, dog-walkers, chess hustlers | major hub park — wild encounters, trainers, hidden items |
| **Riverside Park** (West Side Hwy) | LONG, NARROW greenway | runners, bikers | a super-long **4-tiles-wide** scenic green path/route hugging the river |
| **Central Synagogue** | landmark | rabbi/cantor | bar-mitzvah-era memory (respectful + funny) |
| **Williamsburg, Bklyn** | hipster law-student life | **Cali** (sister, Brooklyn Law) | visit lil sis; she ribs Shane |
| **Bronx** | stadium district | Yankees fans | **Yankee Stadium** landmark/event |
| **Paramus, NJ** | mall suburbia | **Grandma Linda**, uncles **Matt & Jason** (twins), **Donut** (short) | the "crazy uncles" chaos; Grandma feeds you; mall jokes |
| **Old Brookville, LI** | quiet, leafy | (memorial) | mother's late parents' home — tender remembered place |
| **Sidley Austin (Midtown)** — **GYM #1** | corporate law tower / his office | **John Altorelli** (likely GYM 1 leader), **"the Russian spy"** | first gym battle at the firm; law-internship espionage subplot (full roast) |
| **NYC nightlife** | dive bars | bartenders/buddies | underage-drinking hidden spots / sidequest |
| **UPenn (Philly)** | campus + **APES** frat | frat brothers | beer-soaked frat chaos |
| **Emory (Atlanta)** | grad-school campus | college friends (girls & guys) | benders & buddies |
| **IMG Academy (FL)** | elite sports academy | coaches/athletes | athletic boot-camp arc |
| **Camp Pontiac (NY)** | summer camp, lake/woods | camp friends | nostalgic wilderness route |

> Landmarks like **MSG** and **Barclays** = set-piece event venues (concerts/games, special battles)
> rather than full towns. **Riverdale Country School** = secondary school cameo.

### Recurring citywide establishments (re-skinned, LOCATION-DEPENDENT)
- **PokéMart → real chains, varying by location:** **CVS, Rite-Aid, Duane Reade, Walmart, Target,
  bodegas**, etc. Pick whatever fits each neighborhood (get creative — a posh UES pharmacy vs a
  gritty corner bodega vs a suburban Target/Walmart). Same Mart function, many storefronts.
- **Pokémon Center → real heal spots, varying by location too:** e.g., **CityMD / urgent care,
  hospitals (NYU Langone, Mount Sinai), a spa, a vet clinic** — location-appropriate. Same "heal
  your team" function, different skins per area.
- **Joe's Pizza** — recurring **chain in every neighborhood**, but **NOT** the Pokémon Center.
  It's a flavor/social food spot (counter NPC, maybe sells a cheap healing "slice" item or buffs).
  Consistent Joe's storefront everywhere ties the city together.
- **Bars** — citywide nightlife spots (the underage-drinking roast included). Social hubs, quirky
  NPCs, maybe drinking-themed items/sidequests. Full roast.
- **Dispensaries (weed)** — NYC-style dispensaries as recurring establishments. Comedic NPCs/items,
  full roast. (Keep it jokey/over-the-top, in the spirit of the gift.)

### Gyms — secondary layer (lighter, TBD)
- Keep PC's 16-gym backbone, but gyms are **their own thing**, distributed across the towns above.
- Open: are gym leaders **generic themed trainers**, or a few hand-picked characters? Keep PC gym
  **types** (faster) vs re-theme. We'll lock this *after* the world/story takes shape.
- **Justin (rival)** still recurs throughout as Shane's foil regardless of gym design.

## ★ GAME PROGRESSION / STRUCTURE (locked 2026-06-21)
1. **Gyms 1–8** — NYC & suburbs arc (start: Hudson Yards → Gym 1 Sidley Austin → …).
2. **After 8th badge → MEWTWO ISLAND arc** — courier **Dragonite** arrives with Mewtwo's
   invitation (battle + catch it), then the *First Movie* climax on Mewtwo Island. **This replaces
   the usual mid-game Elite Four.** Catch Mewtwo; Mew becomes catchable after.
3. **Gyms 9–16** — college & later-life arc (Philly/Atlanta/IMG/etc.).
4. **After 16th badge → ELITE FOUR** — the true endgame Elite Four (+ Champion / secret final boss,
   cast TBD).

## ★ ENDGAME ARC — MEWTWO ISLAND (*First Movie* climax; replaces mid-game E4)
New location: **Mewtwo Island** ("New Island"), unlocked after the **8th badge** via the courier
Dragonite's invitation. The arc **closely mirrors the plot & beats of *Pokémon: The First Movie***
— invitation by Dragonite → chosen trainers summoned → stormy boat/crossing → island mansion →
Mewtwo's reveal & monologue → clone reveal → trainer battles → the Armored Mewtwo confrontation →
Mew's appearance → resolution. Hit the iconic story beats (re-flavored for our world/roster).

**Flow:**
1. Beat **Gym 8** → **courier Dragonite** flies in with the invitation → **battle & catch the
   Dragonite** (the one-off) → accept invite → travel to the island (stormy crossing, movie-style).
2. **On the island:** invited-trainer arrivals, Mewtwo's mansion/lab, clone-machine intrigue —
   re-create the movie's set pieces and tone.
3. **Battle gauntlet — the player fights them ALL:**
   - **Team Rocket** (the experiment's backers — grunts + a boss; Jessie/James/Meowth flavor).
   - **Ash**, **Misty**, and **Brock** (anime cameos as trainers, themed teams).
   - **Justin** — the **rival also got an invite** and is one of the chosen trainers on the island
     (mirrors the movie's invited trainers). Battle him here too, in full Napoleon-complex form.
4. **★ Armored Mewtwo (two-phase boss):**
   - Phase 1: trainer battle vs **Armored Mewtwo** with the **mirror team** (clone of player's
     party, +5 levels). Phase 2: armor shatters → **wild Mewtwo** → **catchable.**
5. **Mew appears** and becomes **catchable after** the Mewtwo battle (movie's other legendary).
6. Return to the mainland to continue toward **Gyms 9–16**.

> Opponents to script here: Team Rocket (grunts + boss), Ash, Misty, Brock. Teams themed to each
> (Ash = mixed ace incl. Pikachu; Misty = Water; Brock = Rock/Ground), tuned to post-8-badge level.

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
- **TRIGGER (locked):** after the player **defeats the 8th gym**, the **courier Dragonite arrives
  with Mewtwo's invitation.** The Dragonite is then **battleable AND catchable** right there — the
  one-off Dragonite. Accepting the invite launches the **Mewtwo Island** endgame arc.
- **Ties into the ★ Armored Mewtwo storyline** (see Featured Pokémon) — the letter it delivers is
  Mewtwo's invitation; the two events form one cohesive *First Movie* arc.
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
