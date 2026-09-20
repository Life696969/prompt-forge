# Skill plan: prompt-forge

_Forged 2026-09-20 via idea-forge._

## Never lose sight of this

- **Seven is the price, understanding is the product.** Exactly seven
  questions per round for a real dump; each one must move the model closer
  to what the person pictures. A question the dump or the preferences already
  answer is a bug. A thin dump may get fewer; padding is never allowed.
- **Raw thoughts in, a pasteable prompt out.** The skill never does the
  task, never writes into the project, never runs anything without a yes.
- **The loop converges.** Round two starts with "what was off?" and spends
  the other six on that gap only. A session that needs a fourth round is a
  question-quality failure, not a user failure.
- **Memory only steers, never speaks for the person.** Preferences remove
  known dimensions from the pool and are applied visibly ("using: …").
  Nothing else is stored.
- **Zero setup, both runtimes.** One folder, no keys, no network; the same
  SKILL.md works in Claude Code (AskUserQuestion) and Codex (numbered text).

## File layout

```
Personal insta/Public skills/prompt-forge/      — the public repo
  README.md            — pitch, 20-second install, a sample session
  install.md           — Claude Code / Codex / Windows paths, uninstall
  LICENSE              — MIT (as next-step)
  CHANGELOG.md
  planning/            — this brief + plan (archived once built)
  prompt-forge/        — THE SKILL (copied to ~/.claude/skills/prompt-forge)
    SKILL.md           — frontmatter + the flow, hard gates, output rules
    references/question-bank.md   — the ≥15 dimensions, each with: what it
                         resolves, when it is already answered (skip rule),
                         three option patterns + "other", example phrasing
    references/prompt-template.md — the six-section prompt block, with rules
                         per section and two filled examples (code / non-code)
    references/preferences.md     — the memory file's format, what qualifies
                         as a preference (repeat or "always"), how to apply
                         and announce it, how to edit or reset
    templates/summary-card.md     — the 5–8 line summary shape + the gate line
    examples/session.md           — one full session: dump → 7 → no → 7 → yes
                         → prompt → "run it?" → preferences updated
```

## Flow / phases

### Phase 0 — Load and read
Read `~/prompt-forge/preferences.md` if it exists (create nothing yet). Read
the dump. Classify it: **real** (enough to pick seven meaningful questions)
or **thin** (~a dozen words or less). Do not answer, do not start the task.

### Phase 1 — The seven
Pick questions from the bank by the rule: the seven dimensions whose answers
most close the gap between what the person pictures and what a model would
assume — minus what the dump states, minus saved preferences. Ask **one at a
time**: Claude Code → AskUserQuestion with three options + the built-in
"Other"; Codex → the same three as a numbered list plus "4) other — type it".
Options are concrete and specific to this dump, never abstract. Count is
shown ("3/7"). Thin dump: ask as many as are genuinely needed (fewer than
seven allowed), never invent a question to reach seven.

### Phase 2 — Summary gate  **STOP**
Show the summary card (5–8 lines in the person's terms) and ask: **"this
exact output?"** — yes / no. Wait. No prompt is produced before a yes.

### Phase 3 — The NO round
Q1: "what was off?" — options built from the summary's own lines + other.
Q2–Q7: targeted at that gap only (from the bank, filtered to the gap). New
summary, gate again (Phase 2). Repeat until yes. No cap, but the plan
expects round three to be rare.

### Phase 4 — The prompt
Render the six-section block from `prompt-template.md`, entirely from the
answers (no invented detail; unknowns are stated as unknowns inside the
prompt). Print: the block; one line "using: <preferences applied>" (or
"using: none"); one line "run it here now?" **STOP** — run only on yes.

### Phase 5 — Learn (silent, bounded)
If a choice this session matches a choice recorded earlier, or the person
said "always/every time", write it to `~/prompt-forge/preferences.md` (create
the file on first write) and say one line about what was saved. Never store
the dump, the summary or the prompt.

## Frontmatter description (draft)

Turn raw thoughts into the exact prompt for any coding agent or LLM. Use when
the person says "prompt forge", "forge a prompt", "make me a prompt", "help me
write the prompt for this", "I know what I want but can't phrase it", or
pastes a messy paragraph of intent and asks for the prompt. Asks exactly
seven multiple-choice questions (fewer only for a very thin dump), shows a
short summary, asks "this exact output?", loops with seven more until yes,
then hands over a structured copy-paste prompt and offers once to run it.
Remembers stable preferences in ~/prompt-forge/preferences.md. Do not use
when the person wants the task done directly, wants a spec or plan, or asks a
one-line question.

## Open questions for the build

- **Bank size and phrasing** — the ≥15 dimensions and their option patterns
  are the real design work; draft them against three test dumps (a code
  task, a caption, a plan) and check no question is skippable.
- **Thin-dump threshold** — "about a dozen words" is Mudit's rule of thumb;
  the build picks the exact heuristic (word count vs. number of open
  dimensions) and states it in SKILL.md.
- **Preference format** — flat `key: value` lines vs. grouped sections;
  decide for editability by hand.
- **Repo name** — `prompt-forge` vs `prompt-forge-skill` (collision).
- **Reel tie-in** — README should quote the reel's promise ("7 questions —
  na usse zyada, na usse kam") and link the profile; confirm handle text.

## Growth foundation

- **Now:** v1 above — one folder, seven questions, the gate, the loop, the
  six-section prompt, a preferences file. Boundaries: no code, no network,
  one written file.
- **Next (assumed from the reel and Mudit's answers, not promised):** more
  bank dimensions as real dumps expose gaps; a "reuse a past prompt" mode;
  team/shared preferences; a widget form for more runtimes.
- **Foundation now:** the bank is a table of dimensions with skip rules —
  a dimension is added by adding a row, the flow does not change; the prompt
  block has fixed section names, so downstream tools can parse it; the
  preferences file carries a `v1` header, so a later format can migrate
  instead of overwriting; question rendering is one shape with a widget
  fallback, so a new runtime is one paragraph.
- **Deferred:** a prompt library (Mudit chose preferences only); adaptive
  question counts (breaks the promise); reading past dumps (privacy).
  Justified only by repeated user requests after release.
- **Preservation:** any change keeps the seven, the gate, the six sections
  and the `v1` file readable; a v2 preferences file must read v1 lines.
- **Evidence:** adding dimension 19 ("Language of the output") is a table
  row plus its skip rule — no other file changes.
