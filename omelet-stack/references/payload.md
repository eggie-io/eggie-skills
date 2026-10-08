# Recipe: Payload CMS (custom site with an editing screen, one codebase)

## When this recipe
A content site whose front must look and behave exactly as the owner wants, plus an editing
screen for a non-technical person — and WordPress's themes are not the right fit. Payload 3
runs inside Next.js: one service, admin at `/admin`, the public pages in the same app.

## Services
- `web`: Node 22, Next.js with Payload.
- `db`: Postgres 16 (Payload's Postgres adapter); SQLite adapter for a single editor.

## docker-compose.yml
```yaml
services:
  web:
    image: node:22-alpine
    working_dir: /app
    command: sh -c "npm install && npx next dev -H 0.0.0.0 -p 3000"
    environment:
      DATABASE_URI: postgresql://app:app@db:5432/app
      PAYLOAD_SECRET: ${PAYLOAD_SECRET}
    volumes:
      - .:/app
      - node_modules:/app/node_modules
      - media:/app/media
    depends_on:
      - db
  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: app
      POSTGRES_PASSWORD: app
      POSTGRES_DB: app
    volumes:
      - db_data:/var/lib/postgresql/data
volumes:
  node_modules:
  media:
  db_data:
```

## .omelet/project.yml
```yaml
web:
  - service: web
    port: 3000
```

## First run
```bash
docker compose run --rm web npx create-payload-app@latest . --template website --db postgres --use-npm --no-git -y
# it writes .env: move its non-secret keys into .env.example as NAME=default, then delete it
rm .env
# placeholder secrets there (PAYLOAD_SECRET=YOUR_SECRET_HERE, CRON_SECRET, PREVIEW_SECRET)
# become bare NAME=; generate each into Eggie, and set NEXT_PUBLIC_SERVER_URL to the project URL
openssl rand -hex 32 | eggie secret set PAYLOAD_SECRET
openssl rand -hex 32 | eggie secret set CRON_SECRET
openssl rand -hex 32 | eggie secret set PREVIEW_SECRET
eggie up
```
Then the first visit to `<URL>/admin` creates the first user; do it yourself, tell the owner
the address, user and password in chat (never in a file) and to change the password.
Collections (`src/collections/`) are the things the owner edits; one per kind of content.
Each secret is a bare `NAME=` line in `.env.example`; never write its value into a file.
`.gitignore`: `node_modules/`, `.next/`, `media/`, `.env`.

## Existing project
Use the project's `dev` script with `-H 0.0.0.0`; read `.env.example` for the
variables it expects; never create `.env`, generate `PAYLOAD_SECRET` as above.

## Gotchas
- Same live-reload origin rule as `nextjs.md`: `allowedDevOrigins: ["*.127-0-0-1.sslip.io"]`.
- After changing a collection, Payload writes a migration in dev automatically; commit it.
- Uploaded media lives in the `media` volume, not in git.
