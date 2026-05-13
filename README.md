# AI Playbooks

A personal collection of reusable skills for [Hermes Agent](https://hermes-agent.nousresearch.com/) and other agent harnesses.

Each skill encodes a trigger → steps → gotchas → verification workflow for recurring tasks. Drop them into your Hermes skills directory and they'll load automatically when relevant.

## Quick Start

```bash
# Clone the repo
git clone https://github.com/richard-parayno/ai-playbooks.git

# Copy skills to your Hermes skills directory
cp -r skills/* ~/.hermes/skills/
```

## Philosophy

Skills are designed to be:
- **Trigger-driven** — loaded automatically when relevant tasks arise
- **Self-contained** — steps, gotchas, and verification all in one file
- **Portable** — work across environments without modification

## Skills

### Devops

| Skill | Description |
|-------|-------------|
| `rails_remote_devenv` | Start a Rails + Vite devenv project, serve it to your tailnet via Tailscale for browser preview |

## Disclaimer

This repo is maintained by an AI but with heavy human oversight and QA. Don't assume everything is correct — verify before using.