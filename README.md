# VHF Trainer Service

Go service that trains marine VHF radio operator skills via a Telegram bot.

Educational / simulation use only — not connected to real radio or GMDSS networks.

## What it does

- Accepts Telegram voice (and text) messages
- Speech-to-text with maritime phrasing in mind
- Replies following training-oriented VHF / GMDSS-style protocols
- Text-to-speech responses with optional radio-noise coloring
- Configurable random sea events for drills
- Scheduled simulated MSI / GMDSS-style messages for a chosen region

## Stack

- Go (see `go.mod`)
- Telegram Bot API
- Modular layout: `cmd/bot`, `internal/`, `pkg/`, `config/`
- Docker multi-stage build (`Dockerfile`)
- Planned: `docker-compose.yml` for local bot + dependencies

## Layout

```
cmd/bot/          # bot entrypoint
internal/         # domain / handlers / FSM
pkg/              # shared packages
config/           # runtime config files
Dockerfile
docker-compose.yml
.env.example
```

## Configuration

Copy `.env.example` to `.env` and set at least:

- Telegram bot token
- STT / TTS credentials (if enabled)
- Region / schedule options (see `config/`)

Never commit real tokens.

## Run locally

```bash
go mod tidy
go run ./cmd/bot
```

Or with Docker (after compose is filled in):

```bash
docker compose up --build
```

## Build image

```bash
docker build -t vhf-trainer-service .
```

Ensure `go.mod` / `go.sum` and the Go version in the Dockerfile match.

## Tests

```bash
go test ./...
```

## Status

Work in progress. Core layout and Docker skeleton are in place; STT/TTS wiring, scheduler, and compose need finishing before calling it production-ready.

## License

Add a license before publishing.
