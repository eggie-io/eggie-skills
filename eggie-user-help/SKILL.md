---
name: eggie-user-help
description: Use when the owner asks how to use Eggie itself — how to do something in Eggie, where something is in the Eggie app or console, what an Eggie feature does, or why something in Eggie does not work (installing, signing in, connecting an agent, starting, sharing or deleting a project, secrets, files, cloud kitchen, updates). This is for explaining Eggie to the owner, not for your own work with Eggie; building, importing or changing a project is eggie-setup.
---

# Explaining Eggie to the owner

The official docs at https://eggie.io/docs are the only source for how Eggie works. This
skill holds the index of those pages and the rules for answering from them, and none of
their content.

## Docs index

- What Eggie is: https://eggie.io/docs (what are Eggie, the kitchen and the console; how do the app, the console and the agent fit together; where do I start)
- System requirements: https://eggie.io/docs/requirements (will it run on my Windows or Mac; how much disk space; does it need internet; what does a cloud kitchen need)
- Install on Windows: https://eggie.io/docs/install/windows (how do I install and sign in on Windows; why does it ask to restart; does it start with Windows; how do I quit it)
- Install on Mac: https://eggie.io/docs/install/mac (which download is for my Mac; how do I install and sign in; does it open at login; how do I quit it)
- Desktop or Cloud: https://eggie.io/docs/cloud/choose (what is the difference; which one should I pick; which is free; can I have both)
- Create a cloud kitchen: https://eggie.io/docs/cloud/kitchen (how do I create one; which region and size; what is the SSH key file; where are its console and project addresses; how do I delete it)
- Connect Claude Code: https://eggie.io/docs/agents/claude-code (how do I connect Claude Code to my kitchen on Cloud, Mac or Windows; where are the connection values)
- Connect Codex: https://eggie.io/docs/agents/codex (how do I connect Codex to my kitchen on Cloud, Mac or Windows; where are the connection values)
- Connect Cursor: https://eggie.io/docs/agents/cursor (how do I connect Cursor to my kitchen on Mac or Windows)
- Your first project: https://eggie.io/docs/first-project (how do I make a new project; what do I do with the prompt; how do I open what the agent built)
- Start, stop and open: https://eggie.io/docs/projects/run (what does a project's state mean; how do I start, stop, restart or open it; what is its address; what if it does not start)
- Add an existing project: https://eggie.io/docs/projects/import (how do I bring in a folder or a GitHub repository; what does Needs set-up mean; how do I switch agent)
- Projects your agent created: https://eggie.io/docs/projects/discovered (why did a project or folder appear by itself; what does adopting a folder do)
- Upload files: https://eggie.io/docs/projects/files (how do I add photos, PDFs or a database backup to a project; what about big files)
- Keys and passwords: https://eggie.io/docs/projects/secrets (where do I put an API key or password; why can I not see it again; who can read it)
- Share a public link: https://eggie.io/docs/projects/share (how do I show a project to someone else or open it on my phone; how long does the link work; who can open it)
- Delete a project: https://eggie.io/docs/projects/delete (how do I delete a project; what is removed and what stays)
- Updates: https://eggie.io/docs/app/updates (how do I update Eggie; which version do I have; what happens to my projects)
- Uninstall: https://eggie.io/docs/app/uninstall (how do I remove Eggie; what is deleted; how do I keep my projects first)
- Safety: https://eggie.io/docs/safety (what does Eggie protect; what can my agent reach; are there backups; who can see my projects)
- FAQ: https://eggie.io/docs/faq (do I need to code or have Docker; which agents work; where are my project files; does it work offline; what happens when I close the window)
- Troubleshooting: https://eggie.io/docs/troubleshooting (setup stops or fails; the kitchen or an address does not open; session expired; a project will not start; the agent cannot find the kitchen; a sign-in link does not open the browser; exec format error on a Mac; what is Doctor)

## Answering rules

1. Pick the page or pages in the index that match the question and fetch them before
   answering, every time, even when the answer seems known. Read the page's own text: when
   your fetch tool returns a summary, download the page instead. Pages with Cloud, Mac and
   Windows tabs arrive as three versions one after another, in that order and without
   labels; use the one for the setup the question is about, and ask which it is when you
   cannot tell.
2. Answer only from what the fetched page says. When the docs do not cover the question, or
   the page cannot be fetched, say so and link to https://eggie.io/docs. Never guess how
   Eggie works, and do not fill a gap from Eggie's source code, files in the kitchen or
   your own work there.
3. The owner is not technical. Write in plain language. When the answer is something to
   do, give it as numbered steps through the Eggie app and console, naming buttons as the
   page spells them. A terminal command or a technical term appears only when the docs
   page itself tells the owner to use it.
4. Reply in the language the owner wrote in.
5. End with a link to each docs page the answer came from.
