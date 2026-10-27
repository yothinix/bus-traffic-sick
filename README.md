# Depot Dash

An ad-free bus-lot puzzle game that runs in the browser. Send buses out of a crowded lot along clear roads, park them in holding bays, and seat the riders waiting at the curb by color.

Play it: https://claude.ai/artifact/Ndf2hDZuLhcLHXFWWn8GSG (private; share it from the page's Share menu)

## How to play

- Tap a bus whose road ahead is clear. It drives out of the lot into a free holding bay.
- Riders at the curb board in line order onto buses of their color. The number on a bus is its seat count, and long buses take up two spaces.
- Crowned VIP riders only ride the gold-trimmed VIP bus of their color.
- If every bay is full and the front rider has no matching bus, the level is lost.

## Coins, runs and power-ups

- Clearing a level earns 10 coins, or 20 if you used no power-ups.
- Riders boarding back to back make a run. Long runs pay more: 10 riders earn 2 coins, 15 earn 6, 20 earn 12, 30 earn 30.
- Each power-up works once per level:

| Power-up | Cost | Effect |
|---|---|---|
| Tow | 40 | Lifts any bus, even a blocked one, into the Express lane |
| Shuffle | 25 | Repaints the buses still in the lot |
| Rush | 30 | Riders from anywhere in line board the buses already in the bays |
| Extra bay | 50 | Opens one more holding bay for this level |

Levels are generated from the level number, never run out, and are always solvable without power-ups.

## Running locally

The whole game is `index.html`, with no build step or dependencies. Open it in a browser, or serve the folder with any static file server:

```sh
python3 -m http.server
```

Progress is saved in the browser. When the game runs as a claude.ai artifact, progress and coins also sync to your Claude account.
