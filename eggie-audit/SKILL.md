---
name: eggie-audit
description: Use when the owner asks whether a project is any good, safe, ready to go online or worth rebuilding, asks for an audit or review of a whole project, or wants to look deeper after an earlier audit — and when eggie-setup offers a check of an imported project. Use it for a judgement of the project as a whole, taken in steps the owner approves one at a time; a review of one change or a hunt for one bug does not need it.
---

# Auditing a project

An owner who cannot read code cannot tell careful work from code that barely holds together:
both show the same page at the same URL. An audit is the judgement a senior engineer gives a
manager — what shape this is in, what will hurt, what it means for you — and it is true when
the news is bad and true when it is good. Judge the code as you find it, whoever wrote it,
including an earlier session of yours.

It is taken in steps and the owner decides after each one. A real audit of a large project
never reads every file, and never goes silent for an hour before saying anything.

## Before you look

- `docs/brief.md` and `docs/stack.md` say what the project is for, and every finding is judged
  against that. Missing → **use `eggie-rules`** first.
- `docs/audit.md` exists → read it and continue from its *Coverage* table; start over only
  when the owner asks for a fresh audit. First make it true again: where `git log` shows
  changes since *Last updated*, re-check the open findings in the parts that changed and
  correct the verdict.
- Ask the owner, once in every session and before any verdict: **"Is anyone besides you
  using this yet?"** Write the answer into the report. A brief that says "customers"
  describes a plan, and an answer from last month describes last month.
- The audit watches and reads; it never disturbs. Do not stop, restart or rebuild the
  project, and send it no request that changes anything: a restart is exactly what wipes an
  app that keeps its data in memory. The evidence for a hole is the code, never a try.
- It writes one file, `docs/audit.md`, fixes nothing and leaves nothing else behind in the
  project: no caches, no scratch files, no installed tools. Tests and checks run on a copy
  of the project outside its folder, with their own empty data — never through the
  project's own services, which hold the owner's data.

## The quick look

A survey with a fixed budget that does not grow with the project.

1. **Map.** Counting and searching the whole tree is free: files and size per folder,
   `git log` for age, last change and which files change most. Name the parts a developer
   would name. Mark code someone else maintains — a platform the project is built on,
   libraries copied into the tree, generated files. That code is out of scope, with two
   questions kept: has it been edited in place, and how far behind its current release is it.
2. **Read at most 12 files of the project's own code in full**: the entry points, then the
   largest and the most-changed. The brief, the stack record and the few files that say how
   the project is built and run do not count. A project smaller than that is read whole.
3. **Seven checks**, each answered from evidence:

   | Check | Look at |
   |---|---|
   | Data | where what the app must remember is kept, and what a restart does to it |
   | Settings and secrets | credentials written into the code or committed; switches meant for building |
   | Access | which pages and actions answer without signing in; accounts with a default password |
   | Dependencies | declared and pinned; how old; known holes, when the ecosystem has a check for them (run on a copy outside the project) |
   | Safety net | whether tests exist, run and pass (on a copy outside the project), and whether they test logic that matters |
   | Running behaviour | this project's containers in `docker stats --no-stream` at rest; errors and the time it took to start, as `eggie logs` shows them |
   | Structure | what the files you read show: one giant file, logic copied around, one decision spread through many places |

   Not running → the running check is recorded as not looked at. Never estimate memory or
   speed from reading code.
4. **Write the report, then tell the owner** — within about ten minutes of starting, whatever
   the project's size.

## Deep looks

| Area | The owner's question | Guidance |
|---|---|---|
| security | can a stranger read, change or break something | `references/security.md` |
| data and reliability | can what it remembers be lost or damaged | `references/data-and-reliability.md` |
| speed and resource use | will it stay fast and fit its memory | `references/speed-and-resources.md` |
| code health | can it be changed without breaking | `references/code-health.md` |
| readiness to go live | what must change before other people use it | `references/going-live.md` |
| architecture | does the way the parts fit together hold | `references/architecture.md` |

A **step** is one area on one part of the map. A small project with one part gets one step
per area. Every step:

1. Say in one sentence what you are about to look at.
2. Read that area's guidance, then look inside that part only, as deep as the area needs.
3. Add the findings to the report, update *Coverage*, revise the verdict if they change it.
4. Tell the owner what you found, and recommend the next step by risk — or say that nothing
   further looks worth their time.
5. Ask one question: continue with that step, stop, or start fixing. Wait for the answer.

No report yet and the owner asks for a deep look → build the map first, then take the first
step on the riskiest part: the one that handles money, signing in or private data, that
changes most often, that is largest. One step, then the owner. What a step finds often
changes which step is worth taking next, and each one costs the owner time; that is why the
next one is theirs to choose, also when the next part is small and you are already there.

## What counts as a finding

- **No evidence, no finding.** A file and line, a log line, or a command and its output. Say
  whether you saw it happen or read it in the code.
- **No consequence, no finding.** State what it costs the owner: orders lost on restart,
  strangers can read addresses, a change here breaks three other places. Taste, formatting,
  missing polish and features the owner never asked for are not findings.
- **Judged against the brief.** What is wrong for a public shop can be right for a tool one
  person uses.
- **Judged against who uses it today.** Settings that are right while building — a
  development server, a mode that shows errors in the page, simple local passwords, the login
  created for the owner — go under *Before going live* while only the owner uses the project,
  and do not touch the verdict. Once other people use it they are `fix now` findings. A
  problem that hurts the owner alone, such as data lost on restart, is a finding either way.
  So is a missing part, which is not a setting: private pages with no sign-in are `fix soon`
  while only the owner uses the project and `fix now` once anyone else does. So is a key
  for an outside service written into the code: `fix now`, whoever uses the project.
- **Good news to the same standard.** *In good shape* lists what is right, each line with its
  evidence, so a good project learns why it is good.
- **Say what you did not look at.**

| Severity | Means |
|---|---|
| `fix now` | losing data, open to strangers, or falls over in normal use |
| `fix soon` | will hurt as the project grows or is changed |
| `worth knowing` | real, with a small consequence |

Findings are numbered `F1`, `F2`… in the order found and listed worst first. Each carries
the nearest of the six areas above, also when the quick look found it. A project with two
findings has two; do not look for a third to fill the page.

## The verdict

| Verdict | When |
|---|---|
| `solid` | no `fix now`; at most a couple of `fix soon` findings, inside one part |
| `sound, needs some repairs` | a `fix now`, or several `fix soon` findings, each repairable inside the part where it sits |
| `needs serious repair` | a finding that cuts across parts — how data is kept, how access is checked, how parts depend on each other — and the structure can carry the repair |
| `cheaper to rebuild` | cross-cutting `fix now` findings in most parts, so that repairing means rewriting most of the project's own code |

How bad outranks where. A project that cannot yet do what the brief says it is for — it loses
what it must remember, or its main job does not work — is never `solid` or `sound`, however
few files the repair touches; it is `needs serious repair` at the least. On a project that is
a single part, "cuts across" means the repair changes how most of the code reaches its data
or checks who is asking. One finding about the whole project, such as no tests anywhere, is
still one finding.

The verdict names the depth it rests on ("from a quick look"). A quick look that did not read
most of the project's own code never says `cheaper to rebuild`: it says `needs serious
repair`, names rebuilding as a possibility, and recommends an architecture step to settle it.
`solid` is a normal result. Say it plainly and do not soften it with invented caveats.

## The report

Copy `assets/audit.md` to `docs/audit.md`, fill every section, delete its comments. Update it
after every step, before you tell the owner. The plain-words sections are the owner's; the
evidence lines are for the next session. A secret is named by where it sits, never by its
value — in the report and in chat.

Commit the report only when the project is already a git repository ("Audit: quick look",
"Audit: security of checkout"), and commit nothing else. Never `git init`, never push. The
project has a remote → tell the owner once that the report is part of the project's files and
goes wherever the project is sent.

## Telling the owner

One message per step, in this shape: the verdict and what it rests on · at most five things
that matter, worst first, each with what it means for them · what is in good shape, briefly ·
what you did not look at · one question. Everything else stays in the report.

The question is the same after the quick look as after a deep step: continue with the step
you recommend, stop, or — when there is something to fix — start fixing. When the project
was small enough to read whole and a deeper look would add little, say so and recommend the
repairs instead of a step.

Below `developer` (the level in `~/.eggie/owner.md`), no file names and no technology words:

| Do not say | Say instead |
|---|---|
| in memory, no persistence, database | "keeps it in its working memory and never saves it" |
| authentication, authorization | "signing in", "checking who is asking" |
| injection, vulnerability | "someone can slip their own commands into a search box" |
| dependencies, libraries | "building blocks other people wrote" |
| debug mode, development server | "a builder's mode that shows its insides when something goes wrong" |
| refactor, technical debt | "repair", "reorganise" |
| a file or folder name | "the part that takes orders" |

> The app keeps everything it knows in its working memory and never saves it. That is why it
> keeps running out of memory, and why everything is gone whenever it restarts.

A `developer` gets the same findings with files, lines, causes and the report's path.

## Repairs

Offer to fix only when there are `fix now` or `fix soon` findings. Below `developer`,
recommend a set — the `fix now` ones first — and ask yes or no; never ask the owner to choose
between technical options. Yes → **use `eggie-plan`** with them, and once the plan file is
written set those findings to `planned` with its path.

When the repairs are done, come back to the report: revise *Verdict* and *What matters most*
from the findings still open, and tell the owner the new verdict.

`cheaper to rebuild` → say why in plain words and ask before anything else. Yes → a new
project through `eggie-setup`'s flow for a new app, starting from the existing
`docs/brief.md`; the old project stays untouched as the reference and the source of its data.

## Common mistakes

These are what agents did with the same projects before this skill existed.

- Answering in chat and saving nothing, so the next session audits from zero.
- One pass over the whole of a large project, ending in "shall I fix these?" — no map, no
  step, no point where the owner could have said "enough".
- A long tail of "smaller things": price formatting, missing design, a button the owner might
  like. It buries the two findings that matter.
- "A fair start" and "not ready" instead of one of the four verdicts.
- Skipping the usage question because the brief seemed to answer it.
- Reading every file of a small project and calling that the method. It only worked because
  the project was small.
- Running the project's code in place and leaving caches behind in its folder.
- Reporting a builder's setting as a security hole while only the owner uses the project.
