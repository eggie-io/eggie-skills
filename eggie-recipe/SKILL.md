---
name: eggie-recipe
description: Use when the owner asks to download, use or follow an Eggie recipe — "download the Eggie recipe photography-portfolio and follow it", a line copied from the Eggie website, "use the stripe recipe" — or names several recipes to combine. Use it before setting anything up yourself; the recipe already made the brief and stack decisions.
---

# Following an Eggie recipe

An Eggie recipe is published on the Eggie website: a `RECIPE.md` with instructions for you, and
sometimes scripts, files or a whole project template next to it. Work with the owner at the
level `~/.eggie/owner.md` names.

1. **Get it.** Run `eggie recipe get <slug>` for every recipe the owner named. It downloads the
   recipe into `~/projects/.recipes/<slug>/<version>/` and prints that folder, then the whole
   `RECIPE.md`. No slug given ("is there a recipe for a shop?"): run `eggie recipe list`, pick by
   the summary, and confirm the pick with the owner in one question. A command fails: tell the
   owner in plain words what it said and stop.
2. **Read every `RECIPE.md` in full before doing anything.** Files it mentions are in its folder.
3. **Several recipes:** follow the one that creates the project first, then apply the others to
   that project. Where two recipes ask for different things, ask the owner which way to go.
4. **A recipe that becomes a project:** ask the owner what to call it, in one question, offering
   the recipe's slug as the default. Copy everything, hidden files too (`.eggie/` holds the
   project's routing), without the recipe-only files: `mkdir ~/projects/<name> && cp -a
   <folder>/. ~/projects/<name>/ && rm -f ~/projects/<name>/RECIPE.md
   ~/projects/<name>/actions.yml`. Then, in `~/projects/<name>`, run `eggie recipe add <slug>`
   (nothing changes if the template's `project.yml` already lists it) and `eggie up`. The
   template's `.eggie/docs/` pages come along with the copy.
   - **A recipe added to a project the owner already has:** after following it, run
     `eggie recipe add <slug>` in that project's folder (or with `--project <id>`) and copy the
     bundle's `.eggie/docs/*.md` pages into the project's `.eggie/docs/`. Ask before
     overwriting a page with the same name.
   - **In both cases** never put `actions.yml` in a project: it does nothing there. Actions come
     only from Eggie, through `eggie recipe add`; `eggie actions` lists them.
5. **The recipe already decided the brief and the stack.** Skip `eggie-brainstorm` and
   `eggie-stack` unless `RECIPE.md` hands off to them.
6. **Ask first** before anything that runs for a long time (hours of processing) and before
   changing a project the owner already has. Run a recipe's scripts only as `RECIPE.md` says.
7. **Never edit anything under `~/projects/.recipes/`.** Work in the project's own folder.
8. **When it is done**, the project's `AGENTS.md` is the rulebook for every later change. Give
   the owner the URL, after opening it yourself.
