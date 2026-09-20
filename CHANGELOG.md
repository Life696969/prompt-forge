# Changelog

## 1.0.0 — 2026-09-20

First public release.

- Raw thoughts in, the exact prompt out.
- Exactly seven multiple-choice questions per round (three options + other),
  chosen from an 18-dimension bank for what the dump leaves open; fewer only
  on a very thin dump, never padding.
- Summary gate: "this exact output?" — no prompt before a yes.
- The no round: Q1 "what was off?" built from the summary's own lines, six
  targeted questions, repeat until yes.
- A six-section prompt block (Goal · Context · Constraints · Output format ·
  Done when · Examples); unknowns written as unknowns, nothing invented.
- One offer to run the prompt in place.
- Memory of stable preferences only, in `~/prompt-forge/preferences.md`
  (repeat or "always"); never thoughts, summaries or prompts.
- Text form works in any runtime; the question widget is used where available.
- One worked example session.
