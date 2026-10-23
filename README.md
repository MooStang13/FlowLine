# Flowline

A pipe-turning puzzle game for the browser. Spin pipes in place until the line is joined up, then open the valve and see if the water makes it. Later sheets add a second liquid, bridges, and colour mixing.

The whole game is one `index.html`. No build step, no dependencies, no server, no account, no tracking.

## Play

Open `index.html` in any modern browser. It works from a local file.

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

Enjoy 
