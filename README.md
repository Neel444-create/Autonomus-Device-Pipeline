# Autonomous Device Pipeline

A Python platform for planning, allocating, executing, and monitoring tasks across simulated or real robots and device workers.

## Tech Stack

- Python, FastAPI, gRPC
- LLM-based and algorithmic task planning/allocation
- PostgreSQL
- Docker Compose
- React + TypeScript dashboard
- WebSockets for live execution updates

## Architecture

```text
User/API → Gateway :8000 → Fleet Server :50051 → Device Workers
                                ↓
             Telemetry :9000 + PostgreSQL + Dashboard :5173
```

- **Gateway** — REST and WebSocket API
- **Fleet Server** — planning, task-DAG generation, allocation, and execution
- **Telemetry** — device heartbeats and health tracking
- **Device Workers** — simulated or physical capability providers
- **Dashboard** — live plans, task status, events, and device health

## Execution Flow

1. Submit a goal.
2. Generate a dependency-aware task graph.
3. Allocate tasks by capability, cost, or LLM policy.
4. Dispatch tasks in dependency order.
5. Monitor telemetry and task progress.
6. Retry or re-plan on failure.

## Quick Start

```bash
cd robot_fleet
docker compose -f docker-compose.yml -f docker-compose.dev.yml up --build
```

Dashboard: `http://localhost:5173`  
Gateway API: `http://localhost:8000`

## Project Structure

```text
robot_fleet/
├── services/   # fleet server, gateway, telemetry, dashboard
├── robots/     # simulated and real device integrations
├── packages/   # shared config, SDKs, models, metrics
└── scripts/    # demo data and simulated-device scripts
```

## Configuration

| Variable | Purpose |
|---|---|
| `DATABASE_URL` | PostgreSQL connection |
| `OPENAI_API_KEY` | Required only for LLM planning/allocation |
| `GATEWAY_PORT` | REST/WebSocket API port |
| `TELEMETRY_PORT` | Health-monitoring port |

## Monitoring and Reliability

- Device health and heartbeat monitoring
- Structured execution logs
- Failure detection, retry, and re-planning
- Simulated devices for development and integration testing

## Attribution

Originally forked from [therohangupta/agent-fleet](https://github.com/therohangupta/agent-fleet). The upstream license and attribution remain applicable.