# AI Playbooks

[![skills.sh](https://skills.sh/b/richard-parayno/ai-playbooks)](https://skills.sh/richard-parayno/ai-playbooks)

A personal collection of reusable skills for [Hermes Agent](https://hermes-agent.nousresearch.com/) and other agent harnesses.

Each skill encodes a trigger → steps → gotchas → verification workflow for recurring tasks. Drop them into your Hermes skills directory and they'll load automatically when relevant.

## Quick Start

```bash
# Clone the repo
git clone https://github.com/richard-parayno/ai-playbooks.git

# Install a specific skill (via skills.sh ecosystem)
npx skills add richard-parayno/ai-playbooks -s rails_remote_devenv

# Or install all skills from the collection
npx skills add richard-parayno/ai-playbooks --all
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