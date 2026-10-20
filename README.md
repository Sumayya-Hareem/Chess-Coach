# Chess Coach

Play a chess bot and get plain-language feedback on every move you make. Installable, works offline.

## What it does

- Three opponents: Beginner, Club player, Tough.
- After each of your moves the coach labels it (best, good, inaccuracy, mistake, blunder) and explains why in words: hung pieces, missed captures, missed or allowed checkmates, development and castling.
- "Take back & retry" or "Take back & show better move" so you learn from the slip right away.
- Two-stage hint (which piece, then where), evaluation bar, move list with coloured quality dots, end-of-game review, all-time stats.
- Autosaves the game, so closing the app does not lose it.

## Deploy on GitHub Pages

1. Put the files from this zip (index.html, app.js, style.css, sw.js, manifest.webmanifest, icons/) in a repo, in the root or in a folder.
2. Settings > Pages > deploy from the branch.
3. Open the Pages URL on your phone and use "Install app" (or the browser's Add to Home Screen).

If you change the code later, bump `VERSION` in `sw.js` so installed copies refresh straight away.

## Develop

```
npm install
npm run build   # bundles src/ into public/app.js and writes chess-coach-standalone.html
npm test        # engine/coach tests + a simulated-browser UI test
```

`chess-coach-standalone.html` is a single file you can open directly (no hosting, no offline install).

## How the coach works

An alpha-beta search (material plus piece-square tables, capture search, check extension) over chess.js. The coach searches your position 3 moves deep, compares your move with the best one, and turns the gap into a label and an explanation. It is a solid guide for learning, not a grandmaster.
