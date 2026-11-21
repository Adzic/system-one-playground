# Coacerva — a small gym for data science thinking

*Coacerva* is Latin for a **heap**: problems piled up until the pile teaches you something.

The home page (`index.html`) is a problem gym. Each problem is a real one — the kind that shows up in data science interviews and then, worse, in production — and each runs the same four beats, in order:

1. **Commit** — you answer first (multiple choice or a number). Nothing else on the page unlocks until you do. No reading the solution and nodding.
2. **See it** — a live simulation or interactive demo, computed in your browser, shows what actually happens.
3. **The mechanism** — the short worked explanation, with the math where the math is the point.
4. **At work** — where the same trap bites in a real data science job.

Progress (committed answers, completed problems) is stored in `localStorage` under `coacerva_progress`, on the visitor's device only. No backend, no sign-in, no tracking.

## The problems

| # | Problem | File | The trap |
|---|---------|------|----------|
| 1 | Duplicate the Data | `problems/duplicate.html` | Duplicate every row of an OLS dataset: β̂ and R² do not move, the standard error shrinks by about √2, and the t statistic inflates — fake sample size manufacturing significance. |
| 2 | The Even Dice Trap | `problems/dice.html` | Roll until the first 6, given every roll was even: the expected number of rolls is 3/2, not the tempting 3. Conditioning reweights histories; it does not rebuild the die. |
| 3 | The Noise Harvest | `problems/noise.html` | n = 10,000, p = 200, true R² ≈ 0.01: the loudest noise feature (correlation ≈ 0.03) dwarfs a typical true effect (≈ 0.007), so a default GBDT's split search harvests noise while ridge degrades gracefully. |
| 4 | Ridge, Seen Sideways | `problems/ridge.html` | Through the SVD, ridge is a smooth spectral filter, d²/(d²+λ) per principal direction; PCR is the same filter with a step instead of a ramp. Both rank directions by variance in X, never by relevance to y. |

## 🎮 Calibration Duel (the original game)

The game that used to be the home page now lives at **`duel.html`**, unchanged apart from a link back home. Ten statements, true or false. Each round:

1. You lock in **your** P(true).
2. The engine reveals **its** P(true) — a small NLI model (`Xenova/nli-deberta-v3-xsmall`) running live in your browser via Transformers.js.
3. You choose **AUTO-ACT** (+100/−200), **ESCALATE** (+20/−10), or **SKIP** (0/0).

Two scores: **points** (decision quality under uncertainty) and **Brier score** (calibration — mean((p − truth)²), lower wins; a proper scoring rule, so your best move is to report what you actually believe). With these stakes the optimal policy is SKIP below 33%, ESCALATE 33–70%, AUTO-ACT above 70% — the thresholds fall out of the payoffs, not vibes.

First load downloads the model once and caches it; afterwards the Duel works offline. The gym pages need no download at all.

## Run it

Everything is static. Open `index.html` directly, or serve the folder with any static host (Netlify, GitHub Pages, Vercel, `python3 -m http.server`). Vanilla HTML/CSS/JS only — no build step, no libraries, charts hand-drawn with SVG and canvas.

Live demo: `https://coacerva.com`
