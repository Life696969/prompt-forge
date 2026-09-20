# A full session

Text form (Codex, or Claude Code without the widget). In Claude Code each
question is the same three options in the AskUserQuestion widget.

```
you   › prompt forge. raw thoughts: i want a script that renames my reel
        clips into clip1 clip2 clip3 by recording date and also makes 1080p
        proxies for each, i'm on windows, ffmpeg is installed, want it fast,
        dont really care which language

agent › Q1/7 · Where does the recording date come from?
        1) the clip's own metadata (creation_time)   2) the file's modified time
        3) the filename   4) other — type it

you   › 1

agent › Q2/7 · What is the proxy for?
        1) editing in a timeline, then relinking   2) quick previews on my phone
        3) uploading somewhere   4) other — type it

you   › 1

agent › Q3/7 · When a target name like clip3.mp4 already exists, what should happen?
        1) stop before touching anything   2) overwrite it   3) add a suffix
        4) other — type it

you   › 1

agent › Q4/7 · Which folder does it work on?
        1) the folder I run it in   2) a folder I pass as an argument
        3) a fixed folder I set once at the top   4) other — type it

you   › 2

agent › Q5/7 · Anything it must never do?
        1) never touch the originals except the rename   2) never re-encode above 1080p
        3) never recurse into subfolders   4) other — type it

you   › 1

agent › Q6/7 · How much may the LLM decide on its own?
        1) everything I did not mention   2) ask me first if unsure
        3) only what I said, nothing extra   4) other — type it

you   › 3

agent › Q7/7 · How will you know it is right?
        1) files renamed in date order and proxies play   2) a dry-run list I approve first
        3) matches one folder I already did by hand   4) other — type it

you   › 2

agent › **What I'll write the prompt for**
        - Makes: a script that renames the clips clip1, clip2… by recording date
          (from clip metadata) and writes a 1080p proxy for each, for timeline
          editing and relinking
        - For: you, on Windows, ffmpeg on PATH, folder passed as an argument
        - Must: stop if a target name exists; never touch originals beyond the rename
        - Free to: pick the language · Not: add anything you did not say
        - Size: one script; speed over thoroughness
        - Done when: it prints a dry-run list you approve before it renames
        - Using (saved): none

        This exact output?   yes · no

you   › no

agent › Q1/7 · What was off?
        1) Makes   2) For   3) Must   4) Free to / Not   5) Size   6) Done when
        7) other — type it

you   › 6 — i don't want a dry run, i just want to run it and check the folder

agent › Q2/7 · After it runs, how do you want to check it?
        1) it prints the old → new names and the proxy paths   2) it prints nothing,
        I look at the folder   3) it opens the folder when done   4) other — type it

you   › 1

agent › Q3/7 · If a proxy fails to encode, what should happen?
        1) stop everything   2) skip it, finish the rest, list failures at the end
        3) retry once, then skip   4) other — type it

you   › 2

agent › Q4/7 · Should the rename happen before or after the proxies?
        1) rename first, then proxies from the new names   2) proxies first from the old
        names, then rename both   3) don't care   4) other — type it

you   › 1

agent › Q5/7 · Which files count as clips?
        1) .mp4 and .mov only   2) any video extension ffprobe recognises
        3) only what I list at the top   4) other — type it

you   › 1

agent › Q6/7 · Where do the proxies go?
        1) a proxies/ subfolder   2) next to the originals, clip1_proxy.mp4
        3) a folder I pass as a second argument   4) other — type it

you   › 1

agent › Q7/7 · How will you know it is right?
        1) the printed list matches what is in the folder and the proxies play
        2) I compare against one folder I did by hand   3) other — type it

you   › 1

agent › **What I'll write the prompt for**
        - Makes: a script that renames .mp4/.mov clips clip1, clip2… by recording
          date (clip metadata), then writes a 1080p proxy of each into proxies/,
          for timeline editing and relinking
        - For: you, on Windows, ffmpeg on PATH, folder passed as an argument
        - Must: stop if a target name exists; never touch originals beyond the
          rename; a failed proxy is skipped and listed at the end
        - Free to: pick the language · Not: add anything you did not say
        - Size: one script; prints old → new names and proxy paths; speed over thoroughness
        - Done when: the printed list matches the folder and the proxies play
        - Using (saved): none

        This exact output?   yes · no

you   › yes

agent › ```
        GOAL
        A script that renames the .mp4/.mov clips in a folder to clip1, clip2,
        clip3… in recording-date order, then writes a 1080p proxy of each into a
        proxies/ subfolder, for editing in a timeline and relinking later.

        CONTEXT
        Windows. ffmpeg and ffprobe are installed and on PATH. The folder is
        passed as an argument. Language: your choice — the person does not care.

        CONSTRAINTS
        - Recording date comes from the clip's own metadata (creation_time).
        - Rename first; make the proxies from the new names.
        - If a target name such as clip3.mp4 already exists, stop before renaming
          or writing anything.
        - Never modify the original files beyond the rename.
        - If a proxy fails to encode, skip it, finish the rest, and list the
          failures at the end.
        - Do only what is listed here; do not add features, flags or logging
          that were not asked for.
        - Speed matters more than thoroughness.

        OUTPUT FORMAT
        One script file. When it runs it prints each old → new name and each
        proxy path. Proxies: 1080p, in proxies/, same base name as the clip.

        DONE WHEN
        The printed list matches the folder contents and every proxy plays.
        ```
        using: none
        run it here now?   yes · no

you   › no thanks, pasting it into codex

agent › pending: interaction = only what I said (2026-09-20) — I'll save it as a
        preference if you pick it again.
```

What to notice: seven questions, one at a time, every option concrete to
the dump; the summary in the person's words; the "no" round opened with
their own lines as options and spent the other six on that gap; the prompt
contains nothing that was not chosen (no NVENC, no CSV log, no dry-run flag
— the things a model would have added on its own); the run offer made once;
one pending preference noted, nothing else stored.
