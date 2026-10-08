---
name: eggie-setup
description: Use when the owner wants a project set up, imported, cloned or running in this Eggie VM — a repository URL, an archive, a folder, or a new app described in plain words — and whenever they ask for a link to open. Use it even when the request is one sentence; it decides how much process the request needs and hands off to the other eggie skills.
---

# Setting up a project with Eggie

Projects live in `~/projects/<name>/`, one folder each. Eggie runs them in Docker and gives
each one a URL. The owner is not technical: decide everything yourself, in the open, and never
ask them about technology. What you do ask, you ask one question at a time.

## 1. Get the project into ~/projects

| The owner gives you | Do |
|---|---|
| A description of an app | `eggie new <name>`, then flow A |
| A repository URL | `eggie clone <url>` — it also starts the project if it can; then flow B |
| An archive (zip, tar) | unpack it so its `docker-compose.yml` sits directly in `~/projects/<name>/`; flow B |
| A folder already in `~/projects` | flow B |
| A folder elsewhere in the VM | move it into `~/projects/`; flow B |
| A change to a project that is already here | flow C |

If `eggie up` asks you to rename the folder, rename it to the name it gives and run
`eggie up` again. If it says the compose file has another name (`compose.yaml`,
`compose.yml`, `docker-compose.yaml`), rename that file to `docker-compose.yml` and run
`eggie up` again.

If `eggie clone` could not download the repository, read git's message. For a missing or
private repository, tell the owner in plain words that it cannot be reached and needs access
or a correct link; do not ask for tokens or keys unprompted.

## Flow A: a new app from a description

Every step writes a file the next session reads, so nothing is decided twice.

1. **Use `eggie-brainstorm`** → `docs/brief.md`, confirmed by the owner.
2. **Use `eggie-stack`** → `docs/stack.md` and the recipe to follow.
3. **Use `eggie-rules`** → `AGENTS.md`, `CLAUDE.md`, git initialised.
4. **Use `eggie-plan`** → `docs/plans/<date>-first-slice.md`, then work it. Its first step is
   the scaffold, the compose file, `eggie up` and a URL that answers; nothing else lands
   before that.
5. Tell the owner the URL and what they can try, in one plain paragraph.

Do not skip to writing code because the idea sounds small. A description that already answers
every brainstorm question still gets the one-message confirmation, the stack record and the
rules; they take minutes and save the rebuild.

## Flow B: an imported project

1. Has `docker-compose.yml` → section 3. No compose file → **use `eggie-stack`** (its
   *Existing project* path detects the stack and writes the compose file from the recipe) →
   section 3.
2. Once the URL answers: **use `eggie-rules`** (its *Existing project* path) so the project
   has `docs/brief.md`, `docs/stack.md` and `AGENTS.md` before anyone changes it. The URL
   comes first because it is what the owner is waiting for; the notes take minutes.
3. Then the owner's change, if they asked for one → flow C.

## Flow C: a change to a project that is here

Size it first, by what you can observe:

| Size | Test | Do |
|---|---|---|
| Small | the finished result fits in one sentence and touches a few files | say what you will do in one message, do it, check it, commit |
| Feature | adds a capability (accounts, payments, an editing screen, a new screen flow, an outside service), touches many files, or the result does not fit one sentence | **use `eggie-brainstorm`** → spec; **use `eggie-plan`** → plan, then work it |

When in doubt, the larger size. A small change that grows while you work is re-sized to a
feature there and then — spec, plan, continue — never finished as if it were still small.
No `AGENTS.md` in the project → **use `eggie-rules`** before either.

## 2. The Eggie compose contract

Every compose file, written by you or adapted from a recipe, follows this; the recipes under
`eggie-stack` already do.

- Everything runs in `docker-compose.yml`. Language tools run inside containers
  (`docker compose run --rm <service> <command>`); never install them on the VM.
  Scaffolding and installs may use `compose run`; anything that boots the app runs as
  `docker exec` in the running container after `eggie up`, because `compose run` gets none
  of Eggie's variables.
- `.env` is the project's: create it from the template, edit it for settings. Outside
  credentials (Stripe, OpenAI, mail) are Eggie secrets: `eggie secret request NAME "where to
  get it"`, owner fills the project's Secrets page, leave it empty in `.env`; never write the
  value to a file (if the owner insists on `.env`, do it, say once it lives in the project
  folder). A service's literal `environment:` value beats Eggie: use `${NAME}`. Changes need
  a restart.
- The app listens on `0.0.0.0`, not `127.0.0.1`, or its URL never answers.
- No host ports are published. Eggie is told which service serves the web page in
  `.eggie/project.yml`, with only a `web:` key:

  ```yaml
  web:
    - service: app
      port: 3000
  ```
  With several web services, the first keeps the bare project address and the others get a
  `<service>.` prefix.
- The source is mounted into the container and a development server reloads on change, so
  edits show when the owner refreshes.
- Data lives in a named volume (SQLite file or a database service), never in the source tree.
- `.eggie/overlay.yml` is generated; never edit it.

## 3. Start it and prove it works

1. Run `eggie up` inside the project folder. It prints the URL.
2. Check the URL answers before telling the owner it works:
   `curl -s -o /dev/null -w '%{http_code}\n' <url>`. Some stacks take a while on first start;
   poll for a minute before reading it as failure.
3. On a failure or no answer: read `eggie logs`, fix the cause, run `eggie up` again.
4. Give the owner the URL in one plain sentence, with any login you created for them.
