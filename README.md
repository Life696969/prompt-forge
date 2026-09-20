# prompt-forge

**Dump your raw thoughts. It asks you exactly 7 questions. You get the exact
prompt.**

A free Agent Skill for [Claude Code](https://code.claude.com/docs/en/skills)
and [OpenAI Codex](https://agentskills.io). One folder, zero keys, zero
network, zero setup. Its only memory is one small preferences file you own.

It exists because the prompt you type in ten seconds gets you the output a
model *assumes* you want. Seven questions later, it gets you the output you
*pictured* — "na usse zyada, na usse kam".

## Install (20 seconds)

Copy the `prompt-forge/` folder into your agent's skills directory:

```bash
# Claude Code
git clone https://github.com/Life696969/prompt-forge.git
cp -r prompt-forge/prompt-forge ~/.claude/skills/prompt-forge

# Codex
cp -r prompt-forge/prompt-forge ~/.codex/skills/prompt-forge

# cross-runtime alias recognised by Codex, Copilot CLI and Gemini CLI
cp -r prompt-forge/prompt-forge ~/.agents/skills/prompt-forge
```

Windows: replace `~` with `%USERPROFILE%` (for example
`C:\Users\you\.claude\skills\prompt-forge`). Full notes in [install.md](install.md).

Then open your agent and say **"prompt forge"** followed by whatever is in
your head.

## How it works

1. **Raw thoughts in.** Messy, half-formed, any language. Hinglish is fine.
2. **Seven questions, one at a time.** Each is multiple choice — three
   concrete options plus "other". They are chosen for what your dump leaves
   open, so the model understands *your* perspective, not its own defaults.
   (A very thin dump may get fewer. Never padding.)
3. **A short summary.** "This exact output?" — yes or no.
4. **No?** Seven more: the first asks what was off, the other six dig into
   exactly that. Repeat until it is exactly what you want.
5. **Yes?** You get the prompt — a structured block you paste into any LLM
   or coding agent. It offers once to run it right there.
6. **It learns you.** Choices you repeat, or say "always" about, go into
   `~/prompt-forge/preferences.md`. Next time the seven questions skip what
   it already knows and go after what is genuinely new. Every prompt says
   which preferences it used.

## What a session looks like

```
you   › prompt forge. i want a script that renames my reel clips into
        clip1 clip2 by recording date and makes 1080p proxies, windows,
        ffmpeg installed, want it fast, dont care which language

agent › Q1/7 · Where does the recording date come from?
        1) the clip's own metadata (creation_time)   2) the file's modified time
        3) the filename   4) other — type it

you   › 1
        …six more…

agent › **What I'll write the prompt for**
        - Makes: a script that renames the clips clip1, clip2… by recording
          date and writes a 1080p proxy for each, for timeline editing
        - For: you, on Windows, ffmpeg on PATH, folder passed as an argument
        - Must: stop if a target name exists; never touch originals beyond the rename
        - Free to: pick the language · Not: add anything you did not say
        - Done when: files renamed in date order and proxies play

        This exact output?   yes · no

you   › yes

agent › GOAL … CONTEXT … CONSTRAINTS … OUTPUT FORMAT … DONE WHEN
        using: none
        run it here now?   yes · no
```

The full session, including a "no" round, is in
[`prompt-forge/examples/session.md`](prompt-forge/examples/session.md).

## What it will not do

- Do the task for you (unless you say yes to "run it here now?").
- Write anything except `~/prompt-forge/preferences.md`.
- Store your thoughts, summaries or prompts.
- Ask a question your dump already answered.
- Add "best practices" you did not choose to the prompt.

## Folder

```
prompt-forge/
  SKILL.md                      the flow, the rules
  references/question-bank.md   the 18 dimensions the seven are chosen from
  references/prompt-template.md the prompt block, with two filled examples
  references/preferences.md     the memory file: format, what qualifies
  templates/summary-card.md     the summary shape
  examples/session.md           one full session
```

MIT. Made for the people who watch [@ai_with_mudit](https://www.instagram.com/ai_with_mudit) —
DM **git** and you were sent here.
