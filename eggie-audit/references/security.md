# Security step

## What this step answers

Can a stranger, or a signed-in person who should not, read, change or break something?

## Where to look first

1. **Every way in.** List the entry points of this part: pages, form targets, API routes,
   background jobs fed from outside, uploads. A search for how routes are declared finds them
   all without reading each file.
2. **Entry points that change something or show private data.** For each: is the caller
   checked, and is it checked that this record is *theirs*? Search for the odd one out — the
   handler that lacks the check its neighbours have.
3. **Input that reaches something powerful.** Follow request values to queries, shell
   commands, file paths, page output and redirects. Search for queries and commands assembled
   by joining strings.
4. **Secrets.** Keys and passwords in the code, in committed settings, in the git history.
5. **Sign-in itself.** How passwords are stored, how a session is proven, what a guessed or
   stolen session can do, whether forms can be submitted from another site.
6. **Dependencies with known holes**, when the ecosystem has a check for them.

## What is a finding here

| Finding | Usual severity |
|---|---|
| private data or a changing action reachable without a check | `fix now` |
| request input joined into a query, command or path | `fix now` |
| a live credential in the code or its history | `fix now` |
| signed in, but any person can open any other person's records | `fix now` when the data is private |
| passwords stored readable; sessions that can be forged | `fix now` |
| a dependency with a known hole that this project's use can reach | `fix soon` |
| no limit on sign-in attempts on a public project | `fix soon` |

## What is not a finding here

- A known hole in a dependency that this project cannot reach. Note it under *Before going
  live* as "update", not as a finding.
- Builder's settings while only the owner uses the project.
- Missing hardening with nothing to protect: a page with opening hours needs no sign-in.
- A hole you suspect and cannot point at. Say you could not check it.

Never try a hole against a project other people are using, and never use a found credential.

## A part too large for one step

Cut by entry points: first the ones that take money or change records, then the ones that
show private data, then the rest. Tell the owner which group this step covered.
