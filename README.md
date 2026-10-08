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
