# Readiness to go live step

## What this step answers

What has to change before other people use this — or, if they already do, what should have?

This area is about the whole project, not one part: a step covers one group from the list
below.

## Where to look first

1. **Builder's settings.** A development server, a mode that shows errors in the page,
   simple local passwords, a signing secret written into a committed file, the login created
   for the owner, automatic reloading of changed code.
2. **Secrets.** Every outside credential comes from the environment and none is in the code
   or its history; the project starts with a clear message when one is missing.
3. **Data safety.** The data sits in a named volume; something makes copies of it; changes to
   its structure are applied on start or by one documented command.
4. **Starting and restarting.** A fresh start from nothing works with the documented
   command; a restart loses nothing; a crash brings the service back.
5. **Being able to see problems.** Errors land in a log someone can read (`eggie logs`), with
   enough in them to find the cause, and without passwords or personal data.
6. **What strangers can reach.** Admin pages, test pages and sample accounts that were handy
   while building.

## What is a finding here

While only the owner uses the project, everything in this list goes under *Before going
live* in the report, as a plain checklist, and does not change the verdict. Once other
people use it:

| Finding | Usual severity |
|---|---|
| builder's mode or a development server serving other people | `fix now` |
| a signing secret or password that is in the repository | `fix now` |
| sample or default accounts that still work | `fix now` |
| no copies of data other people depend on | `fix soon` |
| a restart or fresh start needs steps nobody wrote down | `fix soon` |
| errors that leave no trace | `fix soon` |

## What is not a finding here

- Anything in this list on a project that will only ever be used by its owner on this
  computer. Read *Where it will live* in the brief.
- Monitoring, scaling and deployment machinery the project's size does not call for.

## A project too large for one step

Take the groups in the order above; the first two are where the harm is quickest.
