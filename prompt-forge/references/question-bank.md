# The question bank

Eighteen dimensions. Each session asks seven of them (fewer only on a thin
dump). Nothing here is a script to read out — every question is rephrased for
the dump in front of you, with three options that are concrete to it.

## Selection rule

1. Strike every dimension the dump already states (a stated "don't care" is
   a statement — record it, strike it).
2. Strike every dimension covered by `~/prompt-forge/preferences.md`.
3. Of what is left, rank by **how far a model's default answer would be from
   what this person probably pictures**, times **how much the prompt changes
   if that answer changes**. Take the top seven.
4. Order them so each answer sharpens the next: outcome and consumer first,
   shape and bounds next, constraints and edges after, done-criteria last.

For a thin dump, stop the list where the remaining dimensions would produce
a question the person could only shrug at.

## Option craft

- Three options that are real alternatives for THIS dump, in the person's
  vocabulary, plus `other — type it`. A model's likely default should be one
  of the three, so the person can reject it consciously.
- Never yes/no. Never "it depends". Never an option that restates the
  question.
- Under fifteen words per option. If an option needs a paragraph, it is two
  questions.

## The dimensions

| # | Dimension | What it resolves | Skip when the dump… | Option pattern |
|---|---|---|---|---|
| 1 | **Outcome** | The artefact that exists at the end | names it precisely ("a PowerShell script", "one caption") | three artefact types it could be |
| 2 | **Consumer** | Who or what reads / runs the output | names the person, machine or channel | three consumers (me now · my team · an end user) |
| 3 | **Shape** | Output format and structure | gives a format or template | three structures (single block · numbered steps · file + notes) |
| 4 | **Bounds** | Length, count, scope limits | gives numbers | three sizes concrete to the artefact (one liner · 40–80 words · 3 versions) |
| 5 | **Voice / style** | Tone for text; conventions for code | states it ("Hinglish", "terse", "PEP8") | three voices with an example phrase each |
| 6 | **Given inputs** | What the LLM will be handed to work from | lists them | three input sets (nothing but this prompt · a file I paste · a link) |
| 7 | **Environment** | Platform, runtime, language, tools | states them | three realistic stacks / platforms |
| 8 | **Non-negotiables** | Must / must-not, hard constraints | lists constraints | three plausible constraints the model might otherwise ignore |
| 9 | **Edge behaviour** | What happens when the normal path fails | covers it | three failure policies (stop · skip and report · retry) |
| 10 | **Reference** | Something to match or to avoid | gives an example or a "like X" | three reference types (match this one · avoid this one · no reference) |
| 11 | **Done criteria** | How they will judge it is right | states the test | three checks concrete to the artefact |
| 12 | **Freedom** | Where the LLM may choose vs must not | says "you decide" or "exactly this" | three freedom levels (decide everything not listed · ask before choosing · only what I said) |
| 13 | **Existing state** | What already exists and must be respected | describes it | three states (nothing yet · this exists, extend it · this exists, replace it) |
| 14 | **Audience** | Who the end product is for (not who runs it) | names them | three audiences in their world |
| 15 | **Priority** | When two goals conflict, which wins | ranks them | three trade-off pairs (fast over thorough · short over complete · safe over clever) |
| 16 | **Interaction** | Should the LLM ask before acting or produce at once | says so | three modes (just produce · ask first if unsure · produce, then list assumptions) |
| 17 | **Delivery** | How the output is handed over | says so | three deliveries (one file · several files · step-by-step with pauses) |
| 18 | **Iteration** | One-shot or drafts / versions | says so | three (one final · three variants · draft then refine) |

## Phrasing examples

Dump: "a script that renames my reel clips clip1 clip2 by date and makes
1080p proxies, windows, ffmpeg installed, want it fast, don't care which
language" — struck: 1 Outcome, 7 Environment (partly), 15 Priority ("fast"),
5 Style ("don't care" — recorded). Asked, in this order:

```
Q1/7 · Where does the recording date come from?
1) the clip's own metadata (creation_time)   2) the file's modified time   3) the filename   4) other — type it

Q2/7 · What is the proxy for?
1) editing in a timeline, then relinking   2) quick previews on my phone   3) uploading somewhere   4) other — type it

Q3/7 · When a target name like clip3.mp4 already exists, what should happen?
1) stop before touching anything   2) overwrite it   3) add a suffix   4) other — type it

Q4/7 · Which folder does it work on?
1) the folder I run it in   2) a folder I pass as an argument   3) a fixed folder I set once at the top   4) other — type it

Q5/7 · Anything it must never do?
1) never touch the originals except the rename   2) never re-encode above 1080p   3) never recurse into subfolders   4) other — type it

Q6/7 · How much may the LLM decide on its own?
1) everything I did not mention   2) ask me first if unsure   3) only what I said, nothing extra   4) other — type it

Q7/7 · How will you know it is right?
1) files renamed in date order and proxies play   2) a dry-run list I approve first   3) matches one folder I already did by hand   4) other — type it
```

Dump: "caption for my reel about the 7 questions skill, hinglish, want ppl to
DM git for the link, don't make it cringe" — thin-ish but real. Struck: 1, 5,
14 (implied), 8 (partly). Asked: 4 Bounds, 18 Iteration, 10 Reference, 11
Done criteria, 2 Consumer (where it is posted / cross-posted), 3 Shape
(hook line + body + CTA?), 12 Freedom.

## The "what was off?" question

Built from the summary card, never from the bank:

```
Q1/7 · What was off?
1) <summary line 1>   2) <summary line 2>   3) <summary line 3>   4) other — type it
```

(List every card line except a `Using (saved): none` line; the numbering
runs as far as needed.) Q2–Q7 then
come from the bank, restricted to dimensions that touch the chosen line.
