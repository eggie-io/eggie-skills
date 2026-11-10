# Speed and resource use step

## What this step answers

Will it stay fast, and will it fit in the memory it has, as it is used more?

## Where to look first

1. **Measure before reading**, when the project runs: `docker stats --no-stream` at rest;
   again after opening the main pages a few dozen times; the time the main pages take
   (`curl -s -o /dev/null -w '%{time_total}\n' <url>`). Memory that climbs and does not come
   back is the finding; the code search below says why.
2. **Things that only grow.** Lists, maps, caches and logs held by the process and added to
   on every request, with nothing that removes from them.
3. **Work that grows with the data.** Loading every record to show ten; a query inside a
   loop over the results of another query; sorting or filtering in code what the data store
   could have done.
4. **Work repeated on every request** that could be done once: reading a large file, calling
   an outside service for something that rarely changes.
5. **Slow work done while the visitor waits**: sending mail, resizing images, long imports.

Not running → say so in *Coverage* and report only what the code makes certain. Never give a
number you did not measure.

## What is a finding here

| Finding | Usual severity |
|---|---|
| memory grows with use until the project stops | `fix now` |
| a main page that takes seconds with the data the project has today | `fix now` on a project in use |
| every record loaded where a page shows a few; a query per row | `fix soon` — sooner the more data the brief expects |
| slow outside work inside a request | `fix soon` |
| no limit on how much one request can ask for | `worth knowing` |

## What is not a finding here

- Code that could be faster on a page that is already fast with realistic data.
- Missing caches, queues or indexes that the project's size does not call for.
- Guesses about "scale" beyond what the brief says the project is for.

## A part too large for one step

Cut by what people do most: the pages every visitor opens first, then the heaviest
background work, then the rest.
