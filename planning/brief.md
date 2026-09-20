> ARCHIVED 2026-09-20: built and published at https://github.com/Life696969/prompt-forge — the skill folder is canonical, do not edit this copy.

# Skill brief: prompt-forge

_Forged 2026-09-20 via idea-forge. Approved by Mudit._

## What it does, in one paragraph

`prompt-forge` is a public, zero-setup Agent Skill (one `SKILL.md` folder)
for Claude Code and OpenAI Codex. The person dumps their raw thoughts about
something they want an AI to produce — code, a caption, a plan, anything.
The skill asks **exactly seven multiple-choice questions** (three concrete
options plus "type your own"), chosen for what the raw thoughts leave most
open, so the model understands the person's perspective — what they picture,
not what a model would assume. It then shows a **short summary** and asks:
"do you want this exact output?" On **yes** it hands over a structured,
copy-paste **prompt** for any coding agent or LLM. On **no** it runs another
round of seven (the first asks what was off; the other six dig into that
gap) — and the loop repeats until the summary is exactly what the person
wants. It keeps a small **preferences file** so every later prompt starts
from what it already knows about the person. It is the skill announced in
reel 87 ("na usse zyada, na usse kam"); people DM "git" for the GitHub link.

## When it triggers — and when it must NOT

- Invoke when: "prompt forge", "forge a prompt", "/prompt-forge", "make me
  a prompt", "help me write the prompt for this", "I know what I want but
  can't phrase it", or the person pastes a messy paragraph of intent and
  asks for "the prompt"/"the exact prompt".
- Do NOT invoke when: the person asks the agent to just do the task ("build
  me X", "write the caption") — do it, do not interview; when they paste a
  finished prompt and ask to run it; when they want a spec, PRD or product
  plan (that is `brainstorming` / `spec` / `idea-forge` territory); when the
  ask is a one-line factual question.

## Inputs and outputs

- Input: (a) raw thoughts — free text, any length, any language, Hinglish
  fine; (b) `~/prompt-forge/preferences.md` if it exists (stable choices:
  stack/language, tone, output formats, standing constraints); (c) answers to
  the seven questions per round; (d) yes/no at the summary gate.
- Output, each round: seven questions (asked one at a time — the menu widget
  in Claude Code, numbered options as plain text in Codex, always with an
  "other: type your own" option), then a **summary card** — 5–8 lines in the
  person's own terms (what it makes, for whom, in what shape, the
  non-negotiables, what "done" means) — and the gate "this exact output?".
- Output, on yes: **the prompt** — one markdown code block with fixed
  sections: `Goal`, `Context`, `Constraints`, `Output format`, `Done when`,
  `Examples` (omitted if none), written to be pasted into any agent or LLM;
  one line noting which saved preferences were applied ("using: TypeScript,
  terse"); one line offering "run it here now?" — executed only on an
  explicit yes; the preferences file updated if a stable preference was
  learned (see Decisions).
- Output, on no: round two — Q1 "what was off?" with choices built from the
  summary's own lines + other, then six questions targeted at that gap; a new
  summary; the gate again. No round limit.

## Hard gates

- Never writes code, files or changes to the person's project — its only
  write is `~/prompt-forge/preferences.md`. The product is the prompt.
- Never runs the prompt unless the person says yes to the one-line offer;
  the offer is made once per delivered prompt, never repeated.
- Never pads: no question that the raw thoughts or the preferences already
  answer, no generic "what's your goal?" filler. Seven is the promise for a
  real dump; a thin dump (roughly a dozen words) may get fewer — the goal is
  understanding, not the number.
- Never stores raw thoughts, summaries or prompts — only stable preferences,
  in plain editable markdown, and only when a choice repeats or the person
  says "always".
- Never asks for keys, never touches the network, no dependencies — copy the
  folder, say "prompt forge".
- Never silently applies a preference: the prompt says which ones it used.

## Overlap with existing skills — and why this one still exists

- One-click prompt improvers (Pretty Prompt, CustomGPT, PromptPerfect) —
  ~40 %: they rewrite a prompt you already wrote; prompt-forge starts from
  raw thoughts and builds the prompt through a fixed interview, inside the
  agent, with memory of your preferences.
- Generic "clarifying questions" skills — ~30 %: they unblock a task the
  agent is about to do; they produce no portable prompt and stop at "clear
  enough".
- Mudit's own `brainstorming` / `spec` (gstack) / `idea-forge` — ~35 %:
  they produce designs, specs and plans for building software; prompt-forge
  produces a copy-paste prompt for any task, is public and zero-setup, and
  has a fixed, trustable price (seven questions).

## Success looks like

- A first-time user with a two-sentence dump gets seven questions they can
  answer by tapping, under a minute, and a summary that makes them say "yes,
  that". A bad session: a question they could have skipped, a summary that
  restates the dump instead of resolving it, or a prompt that needs editing.
- Round two, when it happens, resolves the exact thing that was off; nobody
  needs a round four.
- The second session is visibly better than the first ("using: TypeScript,
  terse") without the person re-answering the known.
- Works identically in Claude Code and Codex from the same folder.

## Decisions already made

- **Name: prompt-forge** (Mudit's pick over exact-prompt / seven-questions).
  Known collision with other "PromptForge" products — accepted; the GitHub
  repo may be `prompt-forge-skill` for findability.
- **Multiple choice + "other"** — fast rounds, works on a phone, and the
  same options render as numbered text in Codex (no menu widget there).
- **The seven are chosen, not fixed** — Mudit's rule: "the questions should
  be such that the LLM understands the perspective of the user very
  clearly." So: a bank of ≥15 dimensions; pick the seven whose answers most
  close the gap between what the person pictures and what a model would
  assume. Saved preferences remove known dimensions from the pool, so the
  seven slots go to what is genuinely unknown about THIS task — the count
  stays seven ("na usse zyada, na usse kam"), memory only steers which.
- **Thin dumps flex** — Mudit: "if the dump is only 10–12 words, 7 is a
  stretch; be flexible; the main goal is to understand the user to create
  the best prompt." So fewer is allowed on a thin dump, padding never is.
- **NO round = Q1 "what was off?" + six targeted** — converges fast; the
  reel's "7 other questions" promise is kept because it is still seven.
- **Structured prompt block + one "run it here?" offer** — LLMs follow
  sectioned prompts more reliably; running is the agent's natural ability,
  offered once, never assumed.
- **Memory = preferences, not prompts** — Mudit: "no need to save the full
  prompts, but the user's preferences and stuff like that so every time the
  prompts keep getting better."
- Public distribution mirrors `next-step`: repo with `README.md`,
  `install.md`, `LICENSE`, `CHANGELOG.md`, and the `prompt-forge/` skill
  folder; DM keyword "git".
