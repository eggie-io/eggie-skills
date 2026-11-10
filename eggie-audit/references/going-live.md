# Readiness to go live step

## What this step answers

What has to change before other people use this — or, if they already do, what should have?

This area is about the whole project, not one part. On a small project the whole list is
one step; on a large one, a step covers one group from the list.

Everything here is read, never tried: do not restart, stop or rebuild the project to see
what happens.

## Where to look first

1. **Builder's settings.** A development server, a mode that shows errors in the page,
   simple local passwords, a signing secret written into a committed file, the login created
   for the owner, automatic reloading of changed code.
2. **Secrets.** Every outside credential comes from the environment and none is in the code
   or its history; the project starts with a clear message when one is missing.
3. **Data safety.** The data sits in a named volume; something makes copies of it; changes to
   its structure are applied on start or by one documented command.
4. **Starting and restarting.** What the files say would happen: whether the documented
   command can start it from nothing, where data sits when the process ends, whether the
   service is set to come back after a crash.
5. **Being able to see problems.** Errors land in a log someone can read (`eggie logs`), with
   enough in them to find the cause, and without passwords or personal data.
6. **What strangers can reach.** Admin pages, test pages and sample accounts that were handy
   while building.

## What is a finding here

Three things are findings whoever uses the project, as the main skill says: a key for an
outside service in the code or its history, data that a restart or rebuild loses, and
private pages with no sign-in. The rest of this list goes under *Before going live* while
only the owner uses the project, as a plain checklist that does not change the verdict.
Once other people use it:

| Finding | Usual severity |
|---|---|
| builder's mode or a development server serving other people | `fix now` |
| a signing secret or password that is in the repository | `fix now` |
| sample or default accounts that still work | `fix now` |
| no copies of data other people depend on | `fix soon` |
| a restart or fresh start needs steps nobody wrote down | `fix soon` |
| errors that leave no trace | `fix soon` |

## What is not a finding here

- The builder's settings and the checklist items on a project that will only ever be used
  by its owner on this computer. Read *Where it will live* in the brief.
- Monitoring, scaling and deployment machinery the project's size does not call for.

## A project too large for one step

Take the groups in the order above; the first two are where the harm is quickest.
