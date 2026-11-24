# Live events: the 12-month calendar

Ashen Vigil runs a new themed event roughly every month, plus a rotating weekend twist every Friday to Sunday. Everything below is built into the game and repeats every year on the same dates (players' local time). Between themed events, **Feathers of the Fallen** runs in two-week seasons so there is always something to earn.

Each event has its own currency, earned the same way: **+3 per horde broken, +2 per boss, +6 for a stage clear, +2 per dungeon run, +4 per Trial of Bells win** (hard mode +50%). Every event shares the same milestone ladder so players learn it once, with a different headline prize:

| Points | Reward |
|---|---|
| 10 | 300 gold |
| 25 | 10 sigils |
| 45 | Iron reliquary |
| 70 | Familiar egg (tier 3 odds) |
| 100 | 25 sigils |
| 140 | **Headline prize** (see calendar) |
| 200 | Ember reliquary + 20 sigils |

## The calendar

| Dates | Event | Currency | Gameplay twist | Headline prize | Why it's there |
|---|---|---|---|---|---|
| 1–14 Jan | **Ashen New Year** | Dawn Embers | +25% gold | Raven Wings | New-year installs; easy, generous start |
| 15 Jan – 6 Feb | Feathers of the Fallen | Feathers | — | Wings ladder (Bat, Raven, Abyssal) | Filler season |
| 7–20 Feb | **Crimson Hearts** | Crimson Hearts | Blood moon: twice the elites, +10% gold | Familiar egg (tier 6 odds) | Valentine's; harder, richer runs |
| 7–20 Mar | Feathers of the Fallen (spring) | Feathers | — | Abyssal Wings | Classic season |
| 4–17 Apr | **Egg Hunt of the Deep** | Eggs | Eggs drop from slain foes | Familiar egg (tier 8 odds) | Easter; drives the familiar collection |
| 2–15 May | **Trial of Champions** | Laurels | Hard mode earns double | Ember reliquary | Rewards skilled and spending players |
| 6–19 Jun | **Midsummer Pyre** | Cinders | Vigil flame lasts twice as long, fire +25% | Raven Wings | Summer holidays; relaxed, powerful runs |
| 4–17 Jul | **The Abyssal Rift** | Void Shards | Hordes 50% bigger, +20% embers | Familiar egg (tier 7 odds) | Chaos event for big-screen clips |
| 1–14 Aug | **Guild Crusade** | Banners | Guild members earn +50% gold and banners | Ember reliquary | Pushes players into guilds (retention) |
| 5–18 Sep | **Harvest of Souls** | Souls | +50% embers (XP) | Abyssal Wings | Back-to-school catch-up for lapsed players |
| 17–31 Oct | **Hallowed Night** | Candy Skulls | An extra horde every run, +20% gold, candy skulls drop | Abyssal Wings | Halloween: the year's biggest event |
| 21 Nov – 2 Dec | **Ember Festival** | Festival Embers | Double gold | Ember reliquary | Black Friday; pair with store sales |
| 12 Dec – 1 Jan | **Winter's Vigil** | Snowflames | A free daily gift, vigil flame lasts longer | Raven Wings | Holidays; daily gift builds the login habit |

## Limited-edition event cosmetics

Seven events have their own wings and/or familiar. Each set has two versions:

| Version | How to get it | Roughly |
|---|---|---|
| **Epic** | Event ladder at 160 points (familiar at 400 when the event has both) | A committed player over the two weeks |
| **Legendary** | **Mythic milestone at 800 points**, or the paid **event bundle** (`av_event_bundle`, only on sale during the event) | 30+ full clears in two weeks, or money |

| Event | Wings | Familiar |
|---|---|---|
| Ashen New Year | Wings of the First Dawn | — |
| Crimson Hearts | Crimson Heartwings | Heartling |
| Egg Hunt of the Deep | — | Ember Hatchling |
| Midsummer Pyre | Midsummer Phoenix Wings | — |
| The Abyssal Rift | Voidrend Wings | Voidling |
| Hallowed Night | Hallowed Bat Wings | Pumpkin Wisp |
| Winter's Vigil | Frostvigil Wings | Snow Owl |

Event cosmetics can't be merged, so the only legendary wings in the game come from the shop, the event bundle or the Mythic milestone. Legendary familiars outside events only hatch at the highest Ember Hatchery tiers (about 2% at tier 10).

## Weekend twists (every Friday to Sunday, rotating)

1. **Double Gold Weekend:** all gold in runs doubled.
2. **Horde Frenzy Weekend:** 40% more foes, 30% more embers.
3. **Blood Moon Weekend:** twice the elites, +20% gold.
4. **Dungeon Weekend:** one extra free entry to every dungeon each day.

Weekend twists stack with the monthly event, so a Hallowed Night weekend can also be a Double Gold weekend.

## Always running

- **Weekly world boss** per realm (resets Monday).
- **Daily dungeons** and the **daily login chest**.
- **Seasonal realm openings**: a new realm opens every 21 days or 3,000 players, giving new players a fresh leaderboard to climb.

## Running events without an app update

Events can be changed live from the Firebase console:

1. Firestore → **Start collection** `config` → document ID `events`.
2. Add a field `events` (type **array**). Each entry is a **map** with:
   - `id` (string, unique, e.g. `hallowed`), `name`, `start` (`"MM-DD"`), `days` (number)
   - `glow` (`"R,G,B"`), `cur` (currency name), `icon` and `art` (asset names, e.g. `env_bones`, `boss_mother`), `blurb`
   - `mods` (map, any of: `gold`, `xp`, `elite`, `spawn`, `horde`, `flame`, `fire`, `hardEarn`, `guildGold`, `extraHorde`, `dungeon`)
   - `prize` (map: `wings` 0–2, or `egg` 1–10, or `claims` like `{ ember: 1 }`)
   - optional `drop` `{ chance, pts }` and `daily` `{ gold, pts }`
3. When that document exists, it **replaces** the built-in calendar on players' next launch. Delete it to go back to the built-in one.

## Ideas for year two

- **Event bundles** in the shop: a themed sigil pack with an event-only cosmetic, on sale only during the event.
- **Limited event stages:** a themed arena (pumpkin patch, frozen cathedral) with its own boss.
- **Anniversary week** on the launch date: every weekend twist active at once.
