# AGENTS.md

Guidance for AI agents working in this repository.

## Project shape

`xiaozhi-esp32-server` is the backend for the `xiaozhi-esp32` hardware device: it speaks the
Xiaozhi protocol over WebSocket/MQTT+UDP and runs the voice pipeline (VAD → ASR → LLM → TTS)
for ESP32 clients. The code lives under `main/` as five separately-deployable subprojects:

| Path | What it is |
| --- | --- |
| `main/xiaozhi-server` | Python asyncio voice server (WebSocket `:8000`, HTTP `:8003`) |
| `main/manager-api` | Spring Boot console backend (`/xiaozhi`, container port `8003`) |
| `main/manager-web` | Vue 3 management console (served by Nginx on `:8002`) |
| `main/manager-mobile` | uni-app (Vue 3 + Vite) mobile/H5/mini-program client |
| `main/digital-human` | Standalone digital-human test page + wakeword runtime (`:8006`) |

Architecture, voice-flow and deployment diagrams are in `docs/diagrams/` (open the `.html`
files directly; the JSON next to each one is the editable source).

## Repository state

`origin` is `eazlong/xiaozhi_server` (push target). It is a standalone repository, not a GitHub
fork: its history was re-initialised to a single `first commit`, so upstream history is not
present locally. `upstream` is `xinnan-tech/xiaozhi-esp32-server`, kept for fetching only — its
push URL is disabled. See `docs/FORK.md`.

Some upstream references are deliberately kept pointing at `xinnan-tech`: the container image
coordinates in `docker-compose*.yml` / `docker-setup.sh` / `Dockerfile-server`, the README
release and star badges, and issue deep links. The reasons are recorded in `docs/FORK.md`;
don't "fix" them without checking there first.

## Testing

`make test-fast` runs all three suites (`test-python`, `test-java`, `test-web`). Run the suite
for the subproject you touched rather than the full matrix when iterating.

## Agent skills

### Issue tracker

Issues live in GitHub Issues on `eazlong/xiaozhi_server`. See `docs/agents/issue-tracker.md`.

### Triage labels

Five canonical triage roles, each label string equal to its role name. See `docs/agents/triage-labels.md`.

### Domain docs

multi-context. See `docs/agents/domain.md`.