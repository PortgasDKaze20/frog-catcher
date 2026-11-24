# Frog Catcher: project audit (before v2)

Audited version: `backup/v1` branch (commit f89eac5), the build live at portgasdkaze20.github.io/frog-catcher before this upgrade.

## Structure and technology

- One file, `index.html` (about 1,300 lines): HTML for the HUD and menus, CSS, and one inline script.
- No engine or libraries. It draws everything itself on an HTML5 2D canvas, so there are no image files. The only outside request is the Google Fonts stylesheet for Baloo 2.
- Rendering: three cached off-screen canvases (sky gradient, scrolling starfield, painted land), with all creatures and effects drawn fresh each frame. The swamp darkness is drawn on a one-third-resolution off-screen canvas.
- Audio: everything is generated with the Web Audio API (music, crickets, frogs, owl, wind, sound effects), with separate music, night-sound and effects buses. A silent looping `<audio>` element unlocks sound on iPhones in silent mode.
- Saving: one `localStorage` key, `frogCatcher.save.v1`, holding JSON.

## How the systems worked

| System | Behaviour found |
|---|---|
| Camera | Fixed 2D side view of the whole pond, scaled to the screen. No scrolling. The layout adapts to portrait and landscape. |
| Farmer | Stays in one place on the grass (your earlier request). Tap or click anywhere and a telescopic pole shoots the net to that point, catches whatever is under it, then pulls back. |
| Frogs | Seven species, each moving between "spots": lily pads, bank points and bush points. States: sit, jump, swim and hidden. Behaviour was hard-coded per type with `if` checks. |
| Catching | Anything inside the net's circle when it lands is caught. Golden and Moon frogs used a flat random chance. No timing or skill element. |
| Economy | Coins are added instantly on each catch. The basket has limited space and the cart sells it for a 20% bonus. Four upgrades: net, pole, lantern and basket. |
| Journal | A grid of 13 species showing caught count and reward, with silhouettes for undiscovered ones. No descriptions or rarity. |
| Progression | Five fixed nights, then endless ones. Star rating was based only on how fast you finished. |
| Settings | Three volume sliders, a graphics quality switch, fullscreen, and reset progress. |

## Bugs found

1. **The Main menu button crashed the game.** `goMenu()` still referred to the removed joystick element (`touchUI`), so Pause → Main menu, Results → Main menu and Reset progress all threw an error and left the game stuck. (Fixed in v2.)
2. Star rating only measured speed. With a stationary farmer, that mostly reflected luck with spawns, not skill. (Replaced by goal-based stars.)
3. Leftover code from the walking version (`walkTop`, the dash and water-wading variables, about 25 lines of joystick CSS) was still being loaded. (Removed.)
4. The menu scene set the farmer to an old walking position, which layout then overwrote. Harmless but confusing. (Removed.)
5. Rare-frog catches were pure luck, so a perfect throw could still fail. (Now timing quality decides.)

## Missing functionality (against the v2 brief)

- No skill-based catching, no Perfect/Good/Miss results, no accessibility option.
- No adaptive difficulty, no player statistics, no accuracy tracking.
- No weather or night conditions apart from the fixed swamp darkness.
- No objectives beyond "catch N creatures", and no milestones or achievements.
- No journal details (rarity, behaviour, favourite conditions), discovery moment or collection rewards.
- No detection tool, no decorations or customisation.
- Farmer animation was limited to breathing, swing and a small celebration.

## Performance notes

- Particles were stored in an array that was rebuilt with `filter()` every frame, which creates garbage on phones. (v2 recycles particles from a pool and updates them in place.)
- The clouds created 24 radial gradients every frame. (v2 draws cached sprites instead.)
- The darkness overlay already ran at one-third resolution. That was kept.
- Measured in headless Chrome with software rendering (no graphics card), heaviest scene: v1 46 fps on desktop. v2's heaviest scene (rain, darkness, every decoration, max lantern) runs at 38 fps in the same test, and 42 fps without rain. Phones and laptops with a real graphics chip run much faster. Battery saver mode lowers resolution and the rain count.

## Recommendations taken in v2

Keep the single-file, no-dependency approach and the stationary farmer. Keep the existing camera, since it shows the whole pond at once, which suits tap-to-throw. Add a data-driven species table, a timing-ring catching system, a rolling-window adaptive director, weather states, objectives, a richer journal, a detection tool and optional decorations, all on top of the existing systems. Migrate the save in place with a backup copy.
