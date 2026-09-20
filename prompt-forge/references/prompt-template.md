# The prompt block

One markdown code block, six sections in this order. It is written as
instructions to whatever LLM or agent will receive it, in plain second person.
It is pasted, not read aloud — no preamble before it, nothing after it except
the `using:` line and the run offer.

```
GOAL
<one or two sentences: the artefact, for whom, what it is for>

CONTEXT
<what exists, what the LLM is given, the environment — only what was said>

CONSTRAINTS
- <must / must-not, one per line, from the answers>
- <priority when goals conflict, if answered>
- <freedom: what the LLM may decide, what it may not>

OUTPUT FORMAT
<shape, bounds, delivery, voice — concrete>

DONE WHEN
<the person's own check, from the done-criteria answer>

EXAMPLES
<the reference to match or avoid, quoted — omit this section if there is none>
```

## Rules

- **Only from the session.** Every line traces to the dump, an answer, or a
  saved preference. If you cannot point to the source of a line, delete it.
- **Unknowns are written as unknowns.** `Date source: not specified — do not
  assume; ask if it matters.` is correct. Inventing `creation_time` is not.
- **Length follows the answers.** Seven answers make a prompt of roughly
  10–25 lines. Forty lines means you added things.
- **Their words.** Keep the person's terms ("proxies", "cringe", "git")
  rather than translating them into yours.
- **No role-play opener.** No "You are a world-class…". The GOAL line does
  the work.
- **CONSTRAINTS holds the answers to Non-negotiables, Edge behaviour,
  Priority and Freedom.** One line each; skip a line whose dimension was not
  asked.

## Filled example — code

From the rename/proxies session in `examples/session.md` (answers: date from
clip metadata; proxies for editing then relinking; stop if a target exists;
folder passed as an argument; never touch originals except the rename; only
what I said; done = renamed in date order and proxies play):

```
GOAL
A script that renames the video clips in a folder to clip1, clip2, clip3… in
recording-date order and writes a 1080p proxy for each, for editing in a
timeline and relinking later.

CONTEXT
Windows. ffmpeg and ffprobe are installed and on PATH. The folder is passed
as an argument. Language: your choice — the person does not care.

CONSTRAINTS
- Recording date comes from the clip's own metadata (creation_time).
- If a target name such as clip3.mp4 already exists, stop before renaming
  or writing anything.
- Never modify the original files beyond the rename.
- Do only what is listed here; do not add features, flags or logging that
  were not asked for.
- Speed matters more than thoroughness.

OUTPUT FORMAT
One script file. Proxies go next to the originals, same base name, 1080p.

DONE WHEN
The files are renamed in date order and every proxy plays.
```

## Filled example — text

From a caption session (answers: 40–80 words; three variants; avoid this one
[a pasted caption]; done = I would post it as-is; Instagram only; hook line +
two lines + CTA; decide wording, not the CTA):

```
GOAL
An Instagram caption for a reel about a skill that asks seven questions and
then gives you the exact prompt. Viewers should DM the word "git" to get the
link.

CONTEXT
Posted on Instagram only. The reel already explains how the skill works; the
caption does not need to.

CONSTRAINTS
- Hinglish, not cringe. Avoid anything like this: "<pasted caption>".
- The CTA is exactly: DM "git". Do not change the word or add a second CTA.
- You may choose the wording; do not change the structure below.

OUTPUT FORMAT
Three variants. Each: one hook line, two short lines, one CTA line. 40–80
words each. No hashtags.

DONE WHEN
One of the three can be posted without editing.

EXAMPLES
Avoid: "<pasted caption>"
```
