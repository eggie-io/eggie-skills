# Data and reliability step

## What this step answers

Can what the project remembers be lost or damaged, and does it keep working when something
around it fails?

## Where to look first

1. **Where state lives.** For each thing the brief says the project remembers, find where it
   is written: a database service, a file, a variable that lives as long as the process. Then
   ask what survives a restart, and whether it sits in a named volume or in the source tree.
2. **Two people at once.** Where two requests can change the same record: read-then-write
   without a transaction or a constraint, counters, "is it free" checks.
3. **Half-done work.** Steps that must all happen or none — take payment and save the order —
   and what state is left when the second fails.
4. **Changes to the shape of data.** Are migrations written down and committed, or was the
   structure changed by hand?
5. **Outside services.** What happens when a call fails or hangs: a timeout, a retry, an
   error the user sees, or a crash.
6. **Copies.** Is there any backup of the data, and has anyone restored one?

## What is a finding here

| Finding | Usual severity |
|---|---|
| data the brief says is remembered lives only in the process | `fix now` |
| data inside the source tree or the container, gone on rebuild | `fix now` |
| money or stock can be counted twice or lost between two requests | `fix now` on a project in use |
| a failed outside call loses or corrupts what was already done | `fix soon` |
| structure changed by hand, no migrations | `fix soon` |
| no backup of data other people depend on | `fix soon`; under *Before going live* while only the owner uses it |

## What is not a finding here

- A simple single-file database for a tool one person uses. Judge it against the brief.
- No retries around a call whose failure the user simply sees and can repeat.
- A race nobody can trigger at the project's real number of users. Mention it as `worth
  knowing` only when the brief says the project will grow.

## A part too large for one step

Cut by what is remembered: take the records that are money or cannot be re-entered first
(orders, payments, bookings), then accounts, then content that can be rebuilt.
