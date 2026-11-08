# MProxy

Proxy manager that pulls nodes from subscription URLs and exposes each node as its own local proxy port, powered by [Mihomo](https://github.com/MetaCubeX/mihomo) (Clash.Meta). Includes a web UI and ships as one Docker image.

## Features

- Manage subscriptions and refresh them on demand
- One local listener per node, starting at port 7901
- Start, stop and restart Mihomo, view logs and regenerate the config from the UI
- SQLite storage

## Tech stack

Python 3.12, FastAPI, SQLAlchemy, SQLite, Vue 3, Vite, Tailwind CSS 4, Mihomo

## Getting started

```bash
docker compose up -d --build
```

| Port | Purpose |
| --- | --- |
| 8080 | Web UI and API |
| 9090 | Mihomo external controller |
| 7901-8100 | Per-node proxy listeners |

Data is stored in `./data`.

## Development

```bash
# backend (from the repository root)
pip install -r backend/requirements.txt
uvicorn backend.main:app --port 8080 --reload

# frontend
cd frontend && npm install && npm run dev
```

## API

| Prefix | Purpose |
| --- | --- |
| `/api/subscriptions` | Create, update, delete and refresh subscriptions |
| `/api/nodes` | List and update nodes |
| `/api/proxy` | Status, start, stop, restart, logs, generate config |

## Project structure

```text
backend/    FastAPI app, Mihomo manager, config generator, routers/
frontend/   Vue 3 SPA (Dashboard, Subscriptions, Nodes)
docs/plans/ Design and implementation plan
```
