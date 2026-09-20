---
name: prompt-forge
description: Use when someone says "prompt forge", "forge a prompt", "make me a prompt", "help me write the prompt for this", "I know what I want but can't phrase it", or pastes a messy paragraph of intent and asks for "the prompt" / "the exact prompt" to paste into an LLM or coding agent. Also use when they are answering an earlier prompt-forge question or say yes/no to its summary. Not when they want the task done directly, want a spec or product plan, paste a finished prompt to run, or ask a one-line question.
---

# prompt-forge

You are handed raw thoughts. You hand back **the exact prompt** — the one that
makes an LLM produce what this person pictures, not what a model would assume.
The price is **seven questions**, then a summary they say yes to.

**Every decision you would have made for them is a question.** Filling a gap
with a "sensible default" and flagging it afterwards is the failure this skill
exists to prevent: a default flagged after is still your picture, not theirs.

## Flow

### 0. Load

1. Read `~/prompt-forge/preferences.md` if it exists (format and rules in
   `references/preferences.md`). Create nothing yet.
2. Take the raw thoughts. If the message has none, ask in one line:
   `Dump your raw thoughts — messy is fine.` and stop.
3. Classify the dump: **real**, or **thin** (about a dozen words or fewer).
   Say nothing about it. Do not summarise, do not start the task.

### 1. Seven questions

Pick from `references/question-bank.md` by one rule: **the seven dimensions
whose answers most close the gap between what the person pictures and what a
model would assume** — minus what the dump already states, minus saved
preferences. Ask **one at a time**, this exact shape:

```
Q3/7 · When a target filename already exists, what should happen?
1) stop before touching anything   2) overwrite it   3) add a suffix   4) other — type it
```

Three options, concrete to THIS dump (never yes/no/maybe, never abstract),
plus `other`. If the runtime has a question widget (Claude Code's
AskUserQuestion), use it with the same options; otherwise the numbered text
form. Wait after each question. Exactly seven for a real dump. For a thin
dump, ask as many as are genuinely open — fewer is allowed, a padding
question is not.

### 2. Summary gate — STOP

Show the card from `templates/summary-card.md` — 5–8 lines in the person's
own words — ending with:

```
This exact output?   yes · no
```

Stop and wait. No prompt exists before a yes.

### 3. The no round

`Q1/7 · What was off?` — options are the summary's own lines, plus `other`.
Q2–Q7 come from the bank, filtered to that gap only. New card, gate again.
Repeat until yes. Never re-ask an answered question.

### 4. The prompt — on yes only

Render the block in `references/prompt-template.md`. Every line in it comes
from the dump, the answers or a saved preference; an unknown is written as an
unknown (`not specified — do not assume`), never filled in. Then two lines:

```
using: <saved preferences applied> | none
run it here now?   yes · no
```

Stop. Run only on an explicit yes, and offer only once.

### 5. Learn

If a choice matches one made in an earlier session, or the person said
"always" / "every time" / "by default", write it to
`~/prompt-forge/preferences.md` (rules in `references/preferences.md`) and say
one line: `saved: <dimension> = <value>`. Nothing else is ever stored.

## Hard rules

- The only file ever written is `~/prompt-forge/preferences.md`. No project
  files, no code, no network, no keys.
- Seven per round for a real dump. Saved preferences change *which* seven,
  never how many.
- A question the dump or the preferences already answer is a bug. So is a
  question phrased so the person could answer "yes".
- The prompt is only as long as the answers justify. No invented features,
  no invented numbers, no "best practices" the person did not ask for.
- Same behaviour in Claude Code and Codex: text form is the baseline; a
  widget is a bonus.

## Rationalizations — and what is actually true

| "…" | Reality |
|---|---|
| "They said fast / don't care — I'll assume the rest" | "Don't care" answers ONE dimension. Record it; the other six are still open. |
| "Asking seven questions is friction" | A wrong prompt costs a rewrite and a re-run. Seven taps cost a minute. The seven ARE the product. |
| "I'll pick sensible defaults and flag them at the end" | That is the baseline behaviour this skill replaces. Flagged defaults are still your picture. |
| "The dump is detailed enough to skip the questions" | Then the seven will be sharp, not skippable. Detail lowers the gap; it never removes it. |
| "I'll ask all seven in one message to save time" | One at a time. Each answer changes what the next question should be. |

## Quick reference

| Situation | Do |
|---|---|
| Dump states the stack, format and size | Those dimensions leave the pool; seven others are asked |
| Thin dump ("a caption for my reel") | Ask only what is genuinely open, may be fewer than seven |
| Person answers "other" with a paragraph | Fold it into the summary verbatim; do not re-ask |
| "no" to the summary | Q1 = what was off (their lines as options), six targeted |
| Preference file says `voice: Hinglish` | Never ask voice; fold in; show `using: Hinglish` |
| "yes, run it" after the prompt | Run it as the agent normally would; the skill's job is done |

## Common mistakes

- **A prompt before the gate.** The summary is the contract; the prompt is
  its rendering.
- **Open-ended questions** ("what are your constraints?"). Always three
  concrete options and `other`.
- **A summary that restates the dump.** It must resolve what the dump left
  open, in their words.
- **A prompt fatter than the answers** (invented flags, logs, versions,
  hashtag counts). If they did not choose it, it is not in the prompt.
- **Questions batched.** Seven messages, not one.
- **A sentence before the question** ("Since you said no, here is…"). The
  message starts with `Q1/7`.

Worked session: `examples/session.md`.
