# Flowline

A pipe-turning puzzle game for the browser. Spin pipes in place until the line is joined up, then open the valve and see if the water makes it. Later sheets add a second liquid, bridges, and colour mixing.

The whole game is one `index.html`. No build step, no dependencies, no server, no account, no tracking.

## Play

Open `index.html` in any modern browser. It works from a local file.

To host it on GitHub Pages:

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. The game appears at `https://<your-username>.github.io/<repo-name>/` after a minute or so.

## How to play

- **Tap a pipe** to turn it a quarter clockwise. **Right-click** turns it back. On a keyboard use the arrow keys to move, **Space** to turn (Shift+Space turns back) and **F** to open the valve.
- Press **Open valve** to test your line. Water runs from each `IN` tank and stops where the line breaks.
- A sheet is complete only when **every drain receives the right liquid and no pipe end is left open**. Reaching the drain with a leak somewhere still fails, and the leaks are marked with red rings.
- **Reset** puts the sheet back to its starting layout. Turns are counted against a par.

### The liquids

| Sheets | What is new |
|---|---|
| 1–8 | One liquid. Get the water to the drain. |
| 9–16 | Two liquids and two drains. Each drain needs its own colour. Keep them apart. |
| 17–24 | Mixing. Two sources merge at a junction and the drain needs the mixed colour. |
| 25–32 | A mix and a pure colour on the same board. |
| 33–40 | Two separate mixes. |

Mixing follows paint rules on three primaries: red + yellow = orange, yellow + blue = green, red + blue = purple.

A pipe with four arms is a **bridge**, not a junction. One liquid passes through left to right, another passes over it top to bottom, and they never mix. Bridges first appear on sheet 12.

### Progress and the shop

- The **level tree** has 40 main sheets and 18 bonus sheets (the diamonds). A sheet unlocks when its parent is cleared. Bonus sheets are easier and pay double coins.
- Stars: 3 for par or better, 2 for up to 1.4× par, 1 otherwise. Coins per star grow with the tier. Replays only pay for extra stars.
- The **shop** sells six pipe finishes and six water colours. Water colour applies to single-liquid sheets. Mixing sheets keep their own red, yellow and blue so the puzzle stays readable.

Progress, coins and purchases are saved in your browser's `localStorage` under the key `flowline.save3`. Nothing leaves your machine. Clearing site data resets the game.

## Project layout

```
index.html                   the whole game: markup, styles and script
tests/generation.test.js     headless check of the level generator
package.json                 only provides `npm test`
```

## Tests

```
npm test
```

(or `node tests/generation.test.js`). It needs only Node. It builds all 58 sheets plus 400 random samples and checks that each one generates, starts unsolved with a par of at least 3, and has a hidden solution that really wins under the rules above.

## How it works

- **Levels are deterministic.** Each sheet seeds its own random generator from its id, so sheet 17 is the same board for everyone every time.
- **Solution first, scramble second.** The generator carves the routes (source to drain, or source to junction to drain) across the grid, derives the pipe pieces from the routes, fills the rest with decoys, then randomly rotates the route pieces. A solved board always exists by construction.
- **Bridges** are planted where a later route crosses a straight stretch of an earlier one at a right angle. In the simulation a four-arm piece is two separate nodes (up-down and left-right).
- **Mixing** is a bitwise OR of source colours (red 1, yellow 2, blue 4). A drain is satisfied when the combined colour of its connected network equals the colour it asks for.
- **Rendering** is a single canvas. Water is drawn per node, so a mix visibly spreads through the network as the other liquid arrives.

## Customising

Everything is plain constants near the top of the script in `index.html`:

- `TIERS`, `SIZES` and `specFor()` set the tier boundaries, grid sizes and when bridges appear.
- `TRUNK` and the branch loop set the length and shape of the level tree.
- `PIPES` and `WATERS` are the shop catalogue (name, price, colours).
- `LIQ` holds the liquid names and colours.
- Theme colours are CSS custom properties at the top of the stylesheet, with light and dark sets.

After changing the generator, run `npm test`.

## Notes

- The page requests two fonts (Chakra Petch and IBM Plex Mono) from Google Fonts. That is the only network request. If it is blocked or you are offline, the game falls back to system fonts and plays the same. To remove the request entirely, delete the three `<link>` lines in the head.
- It follows your system light or dark setting.
- The motion respects the reduced-motion setting.

## Licence

No licence has been chosen yet. Add a `LICENSE` file before sharing the repo publicly.
