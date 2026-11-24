# Frog Catcher — A Magical Night Adventure

A cozy 2D night-time catching game that runs in any modern browser (desktop and mobile, portrait and landscape).
Everything (art, animation, music and night sounds) is generated in code, so the whole game is **one file: `index.html`**.

## Play locally

The quickest way: double-click `index.html` to open it in Chrome, Safari, Edge or Firefox.

To test on your phone over Wi-Fi, run a tiny local server from the folder:

```bash
cd frog-catcher
python3 -m http.server 8000
# or: npx serve .
```

Then open `http://localhost:8000` on your computer, or `http://<your-computer-IP>:8000` on a phone on the same Wi-Fi network.

## Deploy to a website

It is a static site, so any static host works. Upload `index.html`:

- **Netlify Drop**: drag the `frog-catcher` folder onto https://app.netlify.com/drop
- **GitHub Pages**: push the folder to a repo, then Settings → Pages → deploy from the `main` branch root
- **Vercel**: `npx vercel` inside the folder
- **itch.io**: zip the folder, create a new HTML project, upload the zip and tick "This file will be played in the browser"

## Controls

The farmer stands still on the grass. You never walk.

| | Desktop | Mobile |
|---|---|---|
| Shoot the net | Click anywhere | Tap anywhere |
| Sell your basket | Click the cart | Tap the cart |
| Lantern light (from Lantern Lv 1) | Follows the mouse | Glows where you last tapped |
| Shop / Inventory / Pause | B / I / Esc | Top-right buttons |

## How it plays

- Catch frogs, fireflies and the glowing items bats drop. Coins are added the moment you catch something.
- Your **basket** has limited space. When it's full, tap the **cart** next to the farmer to sell it for a 20% bonus.
- Fill the progress bar to finish the night and earn a completion reward. Nights 1–5 add new creatures and new challenges, then the Endless Nights keep going and get a little faster each time.
- Upgrades: **Net** (range, swing speed, luck with rare frogs, a magic glow), **Telescopic Pole** (the net flies out faster and reloads sooner, which matters for frogs that run away), **Lantern** (draws fireflies to you, lights the swamp, brings out rare insects), **Basket** (holds more).

| Night | New things |
|---|---|
| 1 Peaceful Pond | Common frogs, fireflies, bats carrying Moonberries |
| 2 Firefly Garden | Hopper frogs, Blinker fireflies (catch them only while they glow) |
| 3 Midnight Forest | Bush Peepers hiding in the bushes, Azure fireflies, more bats, Star Shards |
| 4 Moonlight Swamp | Darkness and mist, Swamp Shades (only visible in your lantern light), Dart frogs that flee from a slow net |
| 5 Magical Night | Golden frogs (100), Moon frogs (250, they teleport), Star fireflies, aurora |

Progress saves automatically in the browser (localStorage), so it's still there after a refresh. Settings → Reset progress clears it.

## Code map (inside `index.html`)

- `SPEC`, `LEVELS`, `THEMES`, `UPG`: creature rewards, level setup, colour themes and upgrade prices. Change these to rebalance the game.
- `layout()` / `buildBG()`: responsive scene layout and the painted background (redrawn when the screen size changes).
- `updateFrog`, `updateFly`, `updateBat`, `updateItem`: creature behaviours.
- `shoot`, `updateFarmer`, `resolveCatch`, `collect`, `award`, `deliver`: the telescopic net and the economy.
- `moonUpdate` / `drawMoon`: the moon crossing the sky with its halo, rays and drifting clouds; the starfield scrolls slowly in `render()`.
- `drawFarmer`, `drawFrog`, `drawBat`, `render()`: all drawing on the 2D canvas.
- `Audio`: Web Audio synth for the music, crickets, katydids, frogs, owl, wind and sound effects. Volumes are in Settings.
