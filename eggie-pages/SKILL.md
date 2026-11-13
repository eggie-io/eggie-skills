---
name: eggie-pages
description: Use when the owner will need something about a project again outside this chat — a QR code to open a phone app, steps to publish to the app stores or deploy, a login you created, how to reach an admin page — or when such a page in the project's .eggie/docs/ is out of date. Also use when the owner asks to "write it down", "keep this somewhere" or "make a page for it".
---

# Pages the owner keeps

Eggie shows every Markdown file in the project's `.eggie/docs/` on the project page, under
**Docs**. Write what the owner will look for next week there, not in the chat alone.

## Where

- `<project>/.eggie/docs/<name>.md`, one level only: no subfolders of pages. Not `docs/`: that
  folder is the agents' notes.
- `index.md` opens first. With more than one page, keep `index.md` as the landing page and link
  the others from it.
- Start each page with a `# Title` line; it names the page on the page row. Keep it short ("Try
  it on your phone", "Publish to the stores").

## Format

Plain Markdown: headings, lists, tables, `code`, quotes, links.

- **QR code** — a fenced block with the language `qr`; Eggie draws the text as a QR code. It
  must hold an address the phone can open, never `localhost` or this VM's own IP:

  ````
  ```qr
  exp://abc123-anonymous-8081.exp.direct
  ```
  ````

- **Images** — a file in the project, linked by a path relative to the page: `![Home screen](home.png)`
  next to it, `![Logo](../../public/logo.png)` elsewhere. Images from other websites are not shown.
- **Links** — another page: `[Publish to the stores](stores.md)`. A website: a full `https://`
  address; it opens in the owner's browser.
- **No HTML.** It is shown as text, not run.

## What goes on a page

- Only what the owner acts on: what to open, what to tap, where to sign in, what to do next.
  Write at the owner's level from `~/.eggie/owner.md`.
- Never a password or a secret value: pages are committed and travel with the project. Write the
  user name and where to sign in; give the password in the chat and ask them to save it. Keys
  for outside services are on the **Secrets** page.
- When a fact on a page changes (a new address, a step done), update the page in the same
  change. Delete a page that no longer applies.

Then tell the owner in one sentence that it is under **Docs** on the project's page in Eggie.
