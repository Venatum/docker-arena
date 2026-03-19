# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Docker-arena is a Dockerized web dashboard for monitoring job queues (Bull, Bee-Queue, BullMQ). It wraps [bull-arena](https://github.com/bee-queue/arena) in a container, serving a UI on port 4567. Queue configuration is externalized in `index.json`.

## Commands

```bash
# Build Docker image
npm run build

# Run locally (requires Redis)
docker-compose up

# Development with hot-reload
npm run start:dev
```

There are no tests in this project.

## Architecture

Single-file application (`index.js`) that:
1. Loads queue config from `index.json` (gracefully handles missing file)
2. Lazy-loads queue libraries (Bull, Bee, BullMQ) on first access
3. Passes everything to bull-arena which serves the web UI

Key files:
- `index.js` — entry point, ~25 lines
- `index.json` — queue definitions (name, hostId, type, redis URL, prefix)
- `docker-compose.yml` — arena + redis services

## Commit Conventions

Conventional commits expected. Semantic-release automates versioning:
- **MAJOR**: any commit type with `!` (breaking change)
- **MINOR**: `feat`
- **PATCH**: `fix`, `docs`, `perf`, `revert`, `chore(deps)`, `build(docker)`
- **No release**: `test`, `ci`, `build`, `chore(dev-deps)`, `style`, `refactor`

Use scopes `deps` / `dev-deps` for dependency updates, `docker` for Dockerfile changes.

## CI/CD

- **Release** (`master` push): semantic-release creates GitHub releases
- **Docker publish** (tags `v*.*.*`): builds multi-arch images (amd64/arm64), publishes to `docker.io/venatum/arena`
- **Renovate** (weekly Friday): automated dependency updates with automerge for dev-deps, actions, and semantic-release packages
