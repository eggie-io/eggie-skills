# Eggie Skills

Skills for coding agents — Claude Code, Codex, Cursor — that turn a plain-words
idea into a running project: an interview, a stack choice, a plan, and the rules
the agent follows while building.

They are written for an [Eggie](https://github.com/eggie-io/eggie)
box, where the `eggie` command runs projects for you, but nothing here needs one
to install.

## Install

    npx skills add eggie-io/eggie-skills -s '*' -g -a claude-code codex

## The skills

- **eggie-setup** — the entry point; runs the others in order.
- **eggie-brainstorm** — a plain-words interview, written up as `docs/brief.md`.
- **eggie-stack** — chooses adopt, assemble or build, and records `docs/stack.md`.
- **eggie-rules** — writes the project's `AGENTS.md`.
- **eggie-plan** — writes and works through `docs/plans/<date>-<slug>.md`.
- **eggie-recipe** — downloads an Eggie recipe with `eggie recipe get` and follows its
  `RECIPE.md`.
- **eggie-user-help** — answers the owner's questions about using Eggie from the
  [official docs](https://eggie.io/docs).

## License

Source-available under the [Functional Source License 1.1 (FSL-1.1-ALv2)](LICENSE.md).
Each version becomes Apache 2.0 two years after its release.
