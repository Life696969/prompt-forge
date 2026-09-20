# Installing prompt-forge

The skill is the `prompt-forge/` folder in this repo (the one with `SKILL.md`
inside). Copy it into the skills directory of the agent you use. Nothing to
build, no dependencies, no keys.

## Claude Code

```bash
mkdir -p ~/.claude/skills
cp -r prompt-forge ~/.claude/skills/prompt-forge
```

Windows (PowerShell):

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse prompt-forge "$env:USERPROFILE\.claude\skills\prompt-forge"
```

Project-only install: put it in `<repo>/.claude/skills/prompt-forge` instead.

## Codex

```bash
mkdir -p ~/.codex/skills
cp -r prompt-forge ~/.codex/skills/prompt-forge
```

Codex, Copilot CLI and Gemini CLI also read `~/.agents/skills/`, so one copy
there serves all three.

## Check it works

Open the agent and say `prompt forge` followed by a few lines of what you
want. The first reply is `Q1/7 · …` with three options and `other`. No file is
created until the first preference is learned.

## The memory file

`~/prompt-forge/preferences.md` (Windows: `%USERPROFILE%\prompt-forge\preferences.md`)
is created the first time the skill learns a stable preference of yours. Open
it, edit any line, delete any line, or delete the file to start over. It never
contains your thoughts, summaries or prompts.

## Uninstall

Delete the copied folder. Delete `~/prompt-forge/` too if you want a clean
slate.
