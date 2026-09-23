# Omelet Skills

Skills for coding agents — Claude Code, Codex, Cursor — that turn a plain-words
idea into a running project: an interview, a stack choice, a plan, and the rules
the agent follows while building.

They are written for an [Omelet](https://github.com/ihorklymchukdev/local-environment)
box, where the `omelet` command runs projects for you, but nothing here needs one
to install.

## Install

    npx skills add ihorklymchukdev/omelet-skills -s '*' -g -a claude-code codex

## The skills

- **omelet-setup** — the entry point; runs the others in order.
- **omelet-brainstorm** — a plain-words interview, written up as `docs/brief.md`.
- **omelet-stack** — chooses adopt, assemble or build, and records `docs/stack.md`.
- **omelet-rules** — writes the project's `AGENTS.md`.
- **omelet-plan** — writes and works through `docs/plans/<date>-<slug>.md`.
