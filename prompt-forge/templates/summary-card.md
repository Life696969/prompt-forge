# The summary card

Shown once per round, after the seventh answer (or the last one on a thin
dump). Five to eight lines, in the person's own words, then the gate. It
resolves what the dump left open — it does not repeat the dump.

```
**What I'll write the prompt for**
- Makes: <the artefact — outcome + shape>
- For: <consumer / audience>
- Must: <non-negotiables, edge behaviour>
- Free to: <what the LLM may decide> · Not: <what it may not>
- Size: <bounds, iteration, delivery>
- Done when: <their check>
- Using (saved): <preference keys> | none

This exact output?   yes · no
```

Rules:

- Drop a line whose dimension was neither answered nor saved; never write
  "n/a".
- Each line is one sentence fragment. If it wraps to three lines, it is a
  paragraph, not a card.
- Their words. "no cringe" stays "no cringe".
- The `Using (saved)` line is present whenever the preferences file was
  applied, so the person can reject a stale preference by answering "no" and
  picking that line at `What was off?`.
- The gate line is the last line. Nothing after it. Wait.
