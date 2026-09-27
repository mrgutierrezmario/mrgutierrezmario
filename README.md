# Mario Gutierrez

**[M.G. Network and Technology Solutions](https://mgnetsolutions.com)** — I
build practical software around real infrastructure: services that run on
hardware I manage, with the auth, storage, backups, monitoring and runbooks
done properly — not just the demo.

The three apps below run in production on a Mac mini at home, are open
source, and have a documented way back up when they break. The fourth
project is the Kubernetes staging platform built around them.

## Projects

### [InsiderTrack](https://github.com/mrgutierrezmario/insidertrack) — who is buying, and did it work?

Tracks the stock trades of U.S. Congress members, corporate insiders (SEC
Form 4) and institutional investors (13F) from their legally required
disclosures. Scores every ticker on who is buying, weights each member by how
their past buys actually did against SPY, and snapshots every score so the
hit-rate of each label at 30/60/90 days is a number, not a claim.
[Live site](https://insidertrack.mgnetsolutions.com) — no account needed.

`Python · FastAPI · PostgreSQL · React + TypeScript · APScheduler · Docker · Tailscale Funnel`

### [InsiderTrack MCP](https://github.com/mrgutierrezmario/insidertrack-mcp) — ask it in plain English

A [Model Context Protocol](https://modelcontextprotocol.io) server that lets
Claude (or any MCP client) question InsiderTrack: *"Where are several insiders
buying their own stock this month, did anyone in Congress buy the same names,
and how good is that member's record?"* — three tool calls, one answer no
page on the site can give. Read-only by construction, token-gated,
rate-limited, audit-logged, stateless; eleven tools, two resources, two prompts.

`Python · mcp SDK · httpx · Docker`

### [AI Lecture Notes](https://github.com/mrgutierrezmario/lecture-note-app) — the one that started it

Records a lecture from the browser (desktop or phone), transcribes it live
with Whisper, writes structured notes as the class runs, and answers
questions about it afterwards from the transcript, notes and slides. Exports
to PDF, Word, Markdown, MP3, or the user's own Google Drive. In daily use for
a graduate course since March 2026.

`Python · FastAPI · WebSockets · faster-whisper · PostgreSQL · MinIO · React · Docker · OAuth 2.0`

### [homelab-gitops](https://github.com/mrgutierrezmario/homelab-gitops) — staging that proves the backups

A Kubernetes (k3s) staging environment, managed with Argo CD, that runs
*copies* of all three apps restored from the previous night's encrypted
backups — with production credentials scrubbed from each copy. Every merge
to `main` is built by CI, pushed to GHCR, and deployed to staging by Argo CD
Image Updater committing the new digest to git, so `git log` is the
deployment history; a weekly job restores both apps again and smoke-tests
them. Built and verified in September 2026, then paused until it moves to
its own machine — the write-up of why is in the repo. Production is watched
meanwhile by Prometheus + Grafana on the Mac.

`Kubernetes (k3s) · Argo CD · Helm · Sealed Secrets · GitHub Actions · GHCR · Prometheus · Grafana`

## How they're built

- **Operations first:** nightly encrypted off-site backups with a scripted
  restore drill, uptime monitoring, log rotation, a one-page operator runbook
  per project (what to do weekly, monthly, when it's down, when data is lost).
- **Boring on purpose:** pinned dependencies, Dependabot with CI-gated
  auto-merge, secret scanning, CodeQL, branch protection, semantic versions
  and changelogs.
- **AI where it earns its place:** pluggable providers (local Ollama, Claude,
  Gemini, OpenAI) with automatic fallback, routed per job so free local
  models do the bulk work and cloud keys are spent only where they matter.
- Developed with [Claude Code](https://claude.com/claude-code) as a
  pair-programming assistant; every feature came from real use and the
  problems it surfaced.

## What I work with

| | |
|---|---|
| Languages | Python, TypeScript/JavaScript, SQL, Bash |
| Backend | FastAPI, SQLAlchemy + Alembic, PostgreSQL, WebSockets, APScheduler |
| Frontend | React, Vite, TypeScript |
| AI | Anthropic Claude, Google Gemini, OpenAI, Ollama; MCP servers; Whisper |
| Infrastructure | Docker & Compose, Kubernetes (k3s), Helm, Argo CD, Linux and macOS servers, Tailscale, Cloudflare Tunnel, S3/MinIO, GitHub Actions |
| Observability | Prometheus, Grafana, UptimeRobot, health endpoints built for monitors |
| Practices | migrations, encrypted backups and tested restores, OAuth integrations, rate limiting, runbooks |

## Contact

[mgnetsolutions.com](https://mgnetsolutions.com) · mario.gutierrez@mgnetsolutions.com
