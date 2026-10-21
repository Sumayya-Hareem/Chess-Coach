# Chess Coach

Play a chess bot and get plain-language feedback on every move you make. Installable, works offline.

## What it does

- Three opponents: Beginner (1 move deep, makes mistakes on purpose), Intermediate (3 moves deep, a little randomness, sometimes plays opening theory) and Advanced (searches up to 6 moves deep in about 1.4 seconds, plays a built-in opening book, converts won endgames).
- Table talk: the bot comments on every move, yours and its own. Its mood follows the game: smug when you slip, impressed when you play well, relaxed on quiet moves, nervous when it is losing. The teasing is always about the move, never about you.
- Pop-ups on great moves (best move), mistakes and blunders, with a one-line reason. Tap one to dismiss it. Plain "good" moves only get a chat line; to get a pop-up on those too, add 'good' to `TOAST_LABELS` in `src/banter.js`.
- After each of your moves the coach labels it (best, good, inaccuracy, mistake, blunder) and explains why in words: hung pieces, missed captures, missed or allowed checkmates, development and castling.
- "Take back & retry" or "Take back & show better move" so you learn from the slip right away.
- Two-stage hint (which piece, then where), evaluation bar, move list with coloured quality dots, end-of-game review, all-time stats.
- Autosaves the game, so closing the app does not lose it.

## Deploy on GitHub Pages

1. Put the files from this zip (index.html, app.js, style.css, sw.js, manifest.webmanifest, icons/) in a repo, in the root or in a folder.
2. Settings > Pages > deploy from the branch.
3. Open the Pages URL on your phone and use "Install app" (or the browser's Add to Home Screen).

After updating the files, reload the page twice so the old cached copy clears. If you change the code later, bump `VERSION` in `sw.js` so installed copies refresh straight away.

## Develop

```
npm install
npm run build   # bundles src/ into public/app.js and writes chess-coach-standalone.html
npm test        # engine/coach tests, comment-system tests, and a simulated-browser UI test
```

`chess-coach-standalone.html` is a single file you can open directly (no hosting, no offline install).

## How the coach works

An alpha-beta search (material plus piece-square tables, capture search, check extension) over chess.js. The coach searches your position 3 moves deep, compares your move with the best one, and turns the gap into a label and an explanation. It is a solid guide for learning, not a grandmaster.

## Comments and pop-ups

`src/banter.js` turns the move that was just played (capture, check, castle, promotion, retreat, development, centre pawn...), the coach's verdict on your move and the evaluation into a short line. Lines are chosen from pools of variants and never repeat back to back. There is no AI call: it runs fully offline and instantly, and the facts it reacts to (captures, checks, move quality) come from the engine rather than from a language model that could invent them. The wording is playful and loose, so treat it as banter, not analysis; the coach panel is the serious explanation.
