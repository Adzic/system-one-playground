# Calibration Duel — you vs the engine

A Jev-inspired game at **https://coacerva.com**. 10 statements, true or false. Your probabilities against a small AI's — scored on **calibration** (Brier) and **points**. Runs 100% in the browser (Transformers.js + `Xenova/nli-deberta-v3-xsmall`), no server, no sign-up.

## The game
1. 10 random true/false statements.
2. You lock in your P(true).
3. The engine reveals its P(true) — guessed from language patterns, not looked up.
4. You choose: **AUTO-ACT** (+100/−200), **ESCALATE** (+20/−10), **SKIP** (0).
5. Truth revealed. Both you and the engine get Brier scores. The 33%/70% thresholds fall out of the payoff math.

## Notes
- Demo-grade: raw NLI scores, uncalibrated. The duel *measures* calibration live instead of asserting it.
- Evolved from the earlier System One / decision-engine playground; the playground tab was removed to keep it simple — just the game.
