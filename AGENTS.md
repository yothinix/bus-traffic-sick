# Depot Dash

Single-file browser game: everything lives in `index.html` (CSS, markup, one inline script). No build, no dependencies, no test runner. Player-facing rules are in `README.md`.

## Publishing

- The live copy is the claude.ai artifact `https://claude.ai/artifact/Ndf2hDZuLhcLHXFWWn8GSG`. Republish to that URL so the player's link and saved progress carry over.
- The file has no `<!doctype>`, `<html>`, `<head>` or `<body>` tags on purpose: the artifact publisher wraps it in its own skeleton. Start the file with `<title>` and `<style>`.
- The artifact declares the `db` and `user` capabilities for progress sync. Keep them on republish.

## Level generator invariant

`gen(level)` builds levels in reverse: each new bus must have a clear road past every bus already placed, so removing buses last-placed-first always works. The rider queue follows that removal order, shuffled within pairs of buses so two bays suffice. `verify()` replays that intended solution with no power-ups, and a `console.assert` runs it over levels 1–60 on load. Any change to bus shapes, capacities, bays or queue building must keep `verify()` passing.

Levels are seeded from the level number, so changing the generator changes every level, including the one the player is on.

## State model

- Riders and buses match on a key, `color*2 + vip`, so VIP behaves as its own color.
- `S.bays` holds the regular bays followed by the Express lane as its last slot (`lane()`); only Tow fills the lane.
- Progress (`level`, `coins`) is saved to localStorage and, when available, to the db doc `data/users/<user id>/progress`. On load the higher level wins.
- Boarding runs one rider per `step()` tick. A run continues while a bus is still pulling into a bay, and its coin bonus is paid in `endCombo()`.

## Checking a change

Extract the script and syntax-check it, then run the generator check in Node:

```sh
awk '/<script>/{f=1;next}/<\/script>/{f=0}f' index.html > /tmp/page.js && node --check /tmp/page.js
```

To run `verify()` outside the browser, copy the script from `const COLORS` through the `console.assert` loop into a file and run it with Node.

## Conventions

Code is dense, one-statement-per-idea style with short names, matching the existing script.
