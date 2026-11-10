# Architecture step

## What this step answers

Does the way the parts fit together hold — for what the brief says the project is for, and
for the changes the owner is likely to ask for next?

## Where to look first

1. **What depends on what.** From the imports of each part, draw who uses whom. Look for
   parts that reach into each other's insides, and for circles.
2. **One decision, how many places.** Pick the decisions that are expensive to change — how
   data is stored, how access is checked, how an outside service is called — and search for
   where each is made. One place is a structure; forty places is a habit.
3. **Does a change stay local?** Take two changes the brief makes likely (a new kind of
   user, a new thing to sell, a second language) and trace which files each would touch.
4. **Fit to purpose.** Compare the shape with the brief: a public shop held together like a
   one-person tool, or a one-page site carrying machinery for a platform.
5. **The platform, if there is one.** Does the project extend it the way the platform
   intends, or has its code been edited in place, so that an update would erase the work?

## What is a finding here

| Finding | Usual severity |
|---|---|
| the platform's own code edited in place | `fix now` when updates are already being skipped because of it; else `fix soon` |
| storage, access or an outside service handled separately in many places | `fix soon`; this is what turns one repair into many |
| parts that cannot be changed or tested apart | `fix soon` |
| a shape that cannot carry what the brief asks for | `fix now` when the brief's need is today's |
| far more machinery than the purpose needs | `worth knowing`, unless it is what makes changes slow |

## What is not a finding here

- A structure you would not have chosen that carries the purpose and keeps changes local.
- "Not layered", "not modular" or any other label without a change it makes expensive.
- A small project in a few files. Small is a structure.

## Settling `cheaper to rebuild`

This step, or a quick look that read most of the project's own code, may say it. Say it
only when all three hold, each with evidence: the cross-cutting `fix now` findings sit in
most parts; repairing them means rewriting most of the project's own code; and the brief
can be met by a much smaller or more standard project. Otherwise the verdict is `needs
serious repair`, with the order of repairs.

## A project too large for one step

Take the dependency picture of the whole first — it is cheap — then one expensive decision
per step, starting with how data is stored.
