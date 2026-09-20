# The preferences file

`~/prompt-forge/preferences.md` (Windows: `%USERPROFILE%\prompt-forge\preferences.md`).
The only file this skill ever writes. Plain markdown the person can open,
edit and delete. It makes later prompts start better; it never speaks for
the person on anything task-specific.

## Format

```
# prompt-forge preferences v1
# one per line — dimension: value. Edit or delete any line; delete the file to reset.

environment: Windows 11, PowerShell available, ffmpeg on PATH
voice: Hinglish, lowercase, no emoji walls
style: single file, no dependencies unless asked
interaction: only what I said — do not add features
```

Keys are the bank's dimension names in lowercase (`environment`, `voice`,
`style`, `shape`, `bounds`, `interaction`, `freedom`, `priority`,
`delivery`, `iteration`, `consumer`, `audience`). One line per key; a new
value for an existing key replaces the line. The `v1` header is the format
version — read it before parsing; never rewrite a file with a newer version
number than you know.

## What qualifies as a preference

Write a line only when one of these is true:

- the same answer was given for the same dimension in **two different
  sessions** (the earlier one is visible in the file as a pending line — see
  below), or
- the person said **"always"**, **"every time"**, **"by default"**, or
  **"remember this"** about an answer.

A one-off answer is never a preference. Task facts are never preferences:
the goal, the folder, the deadline, the audience of one specific post, the
reference they pasted.

To detect a repeat across sessions without storing task content, the file
may hold at most five `pending:` lines — `pending: voice = Hinglish
(2026-09-20)` — which are promoted to a real line when the same value comes
up again, and dropped when a different value comes up. Pending lines are
never applied to a prompt.

## How a preference is applied

1. At load, strike its dimension from the question pool. The seven slots go
   to what is still open.
2. Fold the value into the prompt block's CONTEXT, CONSTRAINTS or OUTPUT
   FORMAT section, in the person's words.
3. After the prompt, print `using: environment, voice` (the keys applied) —
   or `using: none`. Never apply one silently.
4. If the dump contradicts a preference ("this one in English"), the dump
   wins for this session and the file is not changed.

## When a line is written

At step 5 of the flow, after the prompt. Say one line:
`saved: voice = Hinglish, lowercase` (or `pending: …` for a first sighting).
Create the folder and file on first write, with the header above. Never
write during the questions or before a yes at the gate.

## Never stored

The raw thoughts. The summary card. The prompt. Any answer that describes
the task rather than the person. Anything the person asked not to keep.
