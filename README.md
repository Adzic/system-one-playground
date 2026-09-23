# System One Playground

A Jev-*inspired* decision playground that runs entirely in your browser. No API key, no sign-in, no backend, no payment.

Describe a situation, then ask three kinds of questions:

- **Choice** — a distribution over predefined options ("Where should we eat?")
- **Score** — a distribution over ordered labels plus an expected value ("How urgent is this ticket?")
- **Noul** — an estimated probability that a statement is true ("This customer will churn")

An autonomy-threshold slider marks each decision `AUTO-ACT` or `ESCALATE`.

**Make it a game:** on any Choice question, set *🎯 your call* before hitting DECIDE — the engine tells you whether it agrees or overrules you. Copy the result into the group chat and argue about it. That's the whole point: the probabilities are the conversation starter.

Presets: 🌭 hot dog (the default — settle the sandwich debate), 🎧 support triage, 🎬 movie night, 🍕 pizza wars, ✈️ weekend trip.

## 🎮 Calibration Duel (the game)

The default tab. Ten statements, true or false. Each round:

1. You lock in **your** P(true).
2. The engine reveals **its** P(true) — same tiny NLI model, running live.
3. You choose **AUTO-ACT** (+100/−200), **ESCALATE** (+20/−10), or **SKIP** (0/0).

Two leaderboards: **points** (decision quality under uncertainty) and **Brier score** (calibration — mean((p − truth)²), lower wins; it's the scoring rule RLCD trains on). With these stakes the optimal policy is SKIP below 33%, ESCALATE 33–70%, AUTO-ACT above 70% — the thresholds fall out of the payoffs, not vibes.

Closer to real Jev than the playground: entropy-based `confidence` on Choice (mirrors Jev's response contract), tiered action thresholds (the act / ask-human / do-nothing pattern), and calibration measured with a proper scoring rule instead of asserted.

## How it works

The page loads a small open-weights NLI model (`Xenova/nli-deberta-v3-xsmall`) via Transformers.js and runs inference locally in your browser using ONNX Runtime Web. First load downloads the model once and caches it; afterwards it works offline.

- **Noul** = NLI entailment probability of the statement given the situation.
- **Choice** = each option scored as a hypothesis against the situation, normalized to a distribution.
- **Score** = ordered anchors scored the same way, then an expected value over the label order.

## Honesty notes

- This is **inspired by** Jev's described behavior, not a reproduction of it. Jev is closed-weight and API-only; there is no public RLCD paper or open implementation to be faithful to.
- The NLI probabilities are **raw and demo-grade** — uncalibrated, from a small model, on zero-shot prompts. Do not use them for real decisions.
- Threshold verdicts (`AUTO-ACT` / `ESCALATE`) are a UI toy, not a safety mechanism.

## Run it

It's a single static file. Open `index.html` directly, or serve the folder with any static host (Netlify, GitHub Pages, Vercel, `python3 -m http.server`).

Live demo: `https://coacerva.com`
