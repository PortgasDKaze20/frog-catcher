# Changelog

## v2.0: Cozy adaptive night adventure

Modified files: `index.html` (game), `README.md`, plus new `AUDIT.md` and `CHANGELOG.md`.
Backup of the previous version: branch `backup/v1`.

### Catching
- Tap a creature to lock on and throw. Hold to show a timing ring, and let go when the white ring meets the gold ring:
  **Perfect** (+50% coins, special sound and burst), **Good** (normal reward), **Miss** (nothing, and the frog may escape).
- A quick tap still works for normal frogs. Rare frogs need good timing (a quick tap gives a reduced chance).
- **Simple tap** mode in Settings for accessibility: no timing needed.
- The net homes in on the creature you aimed at, so the result depends on your timing, not on hitting a moving target.

### Adaptive difficulty
- Settings: Relaxed, Adaptive (recommended, default) or Challenging.
- Adaptive watches your last 20 throws at creatures and adjusts in small steps, only between throws and every 8 seconds:
  frog speed and alertness, timing window size, how many tricky frogs spawn, rare-creature chances, and bonus goals.
- Settings shows how the game currently feels (Relaxed, Balanced or Challenging) and your stats: accuracy, Perfect catches, average catch time, misses and time played.

### Frogs and creatures
- Every species now has configurable speed, jump frequency, detection distance, escape style, rarity, catching difficulty, reward and spawn conditions (the `SPEC` table).
- New: **Rain Frog** (only while it rains, dives away) and **Night Frog** (full moon and firefly nights, fades between pads with a bell call).
- Shy Bush Peepers now move between hiding places and duck away if you aim at them too long.
- Bats fly on wandering paths at different speeds, sometimes loop, and appear on two depth layers. Far bats cross the moon as silhouettes.
- Moths flutter around the lights, and crickets hop and chirp in the grass. They are for atmosphere only and never block a throw.
- Frogs sometimes croak in chorus after a shooting star or when rain starts.

### Nights and weather
- Five chapters: Peaceful Pond, Firefly Forest, The Bat Moon, Midnight Rain, The Golden Moon. Endless nights follow.
- Conditions: Clear, Foggy, Rainy, Full Moon and Firefly night. Each changes visuals, sound, frog behaviour and which creatures appear. Changes fade in and out gradually (for example, Midnight Rain starts foggy and the rain arrives later).

### Goals and progression
- Each night has a main goal plus two optional goals (for example, catch 2 Rain Frogs, 3 Perfect catches, catch 6 species, find a rare creature). Sometimes there's a bonus goal too.
- Stars are 1 for the main goal plus 1 for each optional goal. After the main goal you get 40 seconds to finish the others, or you can end the night.
- The results screen shows stars, coins, creatures caught, accuracy, Perfect catches, new discoveries, goals and time.
- Milestones give coin rewards for discoveries, Perfect catches, 3-star nights and more.

### Journal
- Illustrations, rarity, number caught, description, behaviour, favourite conditions, where the creature appears, and your success rate.
- Undiscovered creatures appear as silhouettes with a hint. A **New discovery** card pops up the first time you catch something.

### Shop
- Gear: Net (bigger, with a wider Perfect window), Telescopic Pole (faster, more responsive), Basket (bigger, and from Lv 3 it sells itself when full), Lantern (light), and new **Frog Radar** (marks rare creatures, outlines hidden frogs, more rare spawns, and shows how long a rare creature will stay).
- Decorations (optional, can be shown or hidden): string lights, flower beds, lotus blossoms, stone lantern, bench, fence, scarecrow, arched bridge, farmhouse.

### Farmer animation
- Smooth turning, breathing, blinking, looking toward where you aim, an occasional yawn and stretch, a lean back while you hold, a lean in on the throw, a fist pump on success, and a slump, head shake and sweat drop on a miss.

### UI
- Warm wooden frames around moonlit panels, tabs in the shop and journal, goals in the HUD (tap the panel to collapse it), and a weather label.

### Fixes and performance
- Fixed the Main menu, Results menu and Reset progress crash.
- Particles are recycled from a pool, and the clouds use cached sprites.
- Save format v2 with automatic migration from v1. The old save is kept as `frogCatcher.save.v1.v1backup`. Coins, upgrades, nights, journal and settings carry over.
