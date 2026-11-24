# Frog Catcher: A Magical Night Adventure

A cozy night-time frog catching game that runs in any modern browser on phones, tablets and computers.
Everything (art, animation, music and night sounds) is generated in code, so the whole game is **one file: `index.html`**.

Play: https://portgasdkaze20.github.io/frog-catcher/

## How to play

The farmer stands on the grass by the pond and you never walk.

| | Phone and tablet | Computer |
|---|---|---|
| Throw the net | Tap a creature (or anywhere) | Click |
| Perfect catch | Hold on a creature, let go when the white ring meets the gold ring | Hold the mouse button or Space |
| Sell your basket | Tap the cart | Click the cart |
| Goals panel | Tap it to collapse or expand | Click |
| Menus | Top-right buttons | B shop, J journal, Esc pause, F fullscreen |

- **Perfect** catches give +50% coins. Rare frogs need good timing. Prefer no timing? Choose **Simple tap** in Settings.
- **Difficulty**: Relaxed, Adaptive (recommended) or Challenging. Adaptive quietly adjusts to how you're doing over your last 20 throws.
- Each night has a main goal and optional goals, and stars come from completing them.
- The weather changes: clear, foggy, rainy, full moon and firefly nights, each with different creatures.
- Collect all 15 species in the Night Journal, earn milestones, upgrade your gear, and decorate your pond.

Progress saves automatically in your browser. Each player and each device has its own save.

## Run locally

Double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deploy

GitHub Pages serves this repo from the `main` branch root (Settings → Pages). Push to `main` and the site updates in a minute or two.

## Project notes

- `AUDIT.md` covers the review of v1: features, bugs, gaps and performance.
- `CHANGELOG.md` lists everything added in v2.
- Branch `backup/v1` holds the original version.
- Code map inside `index.html`:
  - `SPEC`: per-species settings (speed, jump, detect, escape, rarity, diff, reward, spawn).
  - `LEVELS`: nights, weather and goals.
  - `UPG` and `DECOR`: the shop.
  - `dfx()` / `adaptTick()`: adaptive difficulty.
  - `pressStart`, `pressEnd`, `throwNet`, `resolveCatch`: catching.
  - `updateWeather`: night conditions.
  - `render()`: drawing.
  - `Audio`: synthesized sound.
