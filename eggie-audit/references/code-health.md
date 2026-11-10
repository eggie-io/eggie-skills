# Code health step

## What this step answers

Can this be changed without breaking it — by an agent that has never seen it before?

## Where to look first

1. **The safety net.** Run the project's tests in a container. Do they pass? Then read a
   few: would they fail if the logic that matters broke, or do they only prove that pages
   load and functions exist?
2. **The files that change most** (`git log --format= --name-only | sort | uniq -c | sort -rn
   | head`). They show where work happens, and where a tangle costs the most.
3. **The largest files and functions.** Size alone is not a finding; one function doing five
   unrelated things is.
4. **The same logic in several places.** Search for a distinctive line of a rule — a price
   calculation, a permission check — and count where it appears.
5. **Failures that are hidden.** Errors caught and ignored, or turned into an empty result,
   so that a broken feature looks like "nothing found".
6. **Code nothing calls.** Whole files or features that are not reachable from any entry
   point.

## What is a finding here

| Finding | Usual severity |
|---|---|
| tests fail, or cannot run | `fix soon`; `fix now` if the failures are real bugs in use |
| no tests on logic where a wrong result costs money or data | `fix soon` |
| a rule copied to several places that must all change together | `fix soon` |
| errors swallowed so that failures are invisible | `fix soon` |
| a function or file nobody can follow, in a place that changes often | `fix soon` |
| dead code large enough to mislead the next person | `worth knowing` |

## What is not a finding here

- Naming, formatting, comment style, file layout you would have chosen differently.
- Low test coverage as a number. Name the logic that is unprotected, or say nothing.
- A large file that is simple and rarely changes.
- An older but supported way of doing something that works.

## A part too large for one step

Take the most-changed files of the part first; they are where the owner's next request will
land. Then the largest. Say which files the step covered.
