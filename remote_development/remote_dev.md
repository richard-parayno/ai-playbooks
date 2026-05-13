# Remote Dev — Tailscale Serve Workflow

Use this when working on a local devenv project with Richard and he wants to preview changes in his browser.

## Policy

All of Richard's projects use [devenv](https://devenv.sh/). This workflow applies to any devenv-based project.

## Steps

### 1. Start services (outside devenv shell)

```bash
cd ~/work/<project>
devenv up
```

This starts backing services (Postgres, Redis, etc.) — does NOT need to be run inside `devenv shell`.

### 2. Enter devenv shell and start dev server

```bash
devenv shell
bin/dev
```

- `bin/dev` uses Foreman to fire up Rails + Vite + background workers
- If Stripe CLI asks for auth → send Richard the login link so he can authorize

### 3. Serve to tailnet

In a **separate terminal** (keep dev server running), run:

```bash
tailscale serve --http=3000
```

Share the resulting URL with Richard. He can preview the app directly in his browser on his tailnet.

## Setup (first time per project)

```bash
cd ~/work/<project>
bundle install
npm install
rails db:create db:migrate db:seed   # seed failures are safe to ignore
```

## Gotchas

- `devenv up` goes in the **regular shell**, NOT inside `devenv shell`
- Stripe CLI may need authorization — ping Richard with the auth link
- Seed script failures = likely just stale config in the seed script, ignore and continue