---
name: rails_remote_devenv
description: Start a devenv project, serve it to the tailnet via Tailscale, and let a collaborator preview in their browser.
triggers:
  - "run the dev server"
  - "preview in browser"
  - "tailscale serve"
  - "start devenv project"
  - "devenv shell"
  - "bin/dev"
environment:
  workdir: ~/work/<project>
  project: auto-detect from current directory or context
  tailscale_status: must be connected to tailnet
---

# Devenv Remote Dev — Tailscale Serve Workflow

Use when working on a local devenv project and a collaborator wants to preview changes in their browser.

## Workflow

### Step 1 — Start backing services (regular shell, outside devenv)

```bash
cd ~/work/<project>
devenv up
```

`devenv up` starts Postgres, Redis, and other services. **Do NOT run this inside `devenv shell`** — it belongs in the regular shell.

### Step 2 — Enter devenv shell and start dev server

```bash
devenv shell
bin/dev
```

- `bin/dev` uses Foreman to start Rails + Vite + background workers
- Wait for the server to be fully up before proceeding

### Step 3 — Serve to tailnet (separate terminal)

Keep the dev server running, then in a **new terminal window**:

```bash
tailscale serve --http=3000
```

Share the resulting URL with the collaborator. They can open it in their browser on their tailnet.

## Project Setup (first time only per project)

```bash
cd ~/work/<project>
bundle install
npm install
rails db:create db:migrate db:seed
```

**Note on seed failures:** If `rails db:seed` fails, it is almost always a stale/bad config hardcoded in the seed script. Ignore the error and continue — the app will still run.

## Gotchas

| Situation | Action |
|-----------|--------|
| Stripe CLI asks to login | Send the auth link to the collaborator so they can authorize |
| `devenv up` hangs | Check that no other instance is already running |
| `bin/dev` fails to start | Verify `devenv up` completed successfully first |
| Tailscale not connected | Run `tailscale up` before `tailscale serve` |

## Verification

After starting, confirm:
1. `devenv up` completed without error
2. `bin/dev` shows rails + vite processes running
3. `tailscale serve` reports a reachable URL
4. Collaborator confirms they can access the URL in their browser