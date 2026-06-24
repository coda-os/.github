# coda-os

Coda OS hosts two products: the Coda restaurant operating system and the Argus wildlife-monitoring stack.

## Repositories

| name | what it is | status |
| --- | --- | --- |
| coda-argus-core | Central platform API for the Argus elephant-detection system. Auth, device management, event ingestion, fleet state, OTA, alerts, telemetry, analytics. Java 21, Spring WebFlux, PostgreSQL + TimescaleDB, MQTT, Redis, MinIO. | active |
| coda-argus-edge | On-site runtime for Jetson Orin Nano and Raspberry Pi. Camera capture, AI detection, event publishing to core, local actuation. | active |
| coda-argus-command | Forest-department dashboard. Login, live monitoring, alerts, remote control. | active |
| coda-argus-fleet | Engineering dashboard. OTA pushes, device management, logs. | in development |
| coda-argus-ml | Training pipeline that produces the detection models OTA-delivered to the edge. | in development |
| coda-argus-infra | Deployment automation for the Argus stack. Docker, Kubernetes, Terraform, CI/CD. | active |
| coda-os | Marketing site (oneiros-coda.in). | maintained |
| oneiros-coda-serve | Coda, the restaurant operating system. Ordering, kitchen workflow, payments, customer retention, analytics. Next.js 16, Supabase, Clerk, Inngest, PhonePe, Razorpay. | active |

## Architecture

**Argus** is a distributed system: edge nodes (Jetson / RPi) on-site run detection, publish to `coda-argus-core` over MQTT, and receive OTA updates and control commands. MQTT broker, Postgres + TimescaleDB, Redis, and MinIO are shared infrastructure. Dashboards are `coda-argus-command` (forest-department operators) and `coda-argus-fleet` (engineering). The full protocol and data-flow document is [`argus-architecture.md`](/home/jishnnp/argus/argus-architecture.md) in the working tree, not yet published to a GitHub repo.

**Coda** runs as a single Next.js application on Supabase with Clerk for auth and Inngest for background jobs. PhonePe is the primary payment processor, Razorpay the fallback. All monetary values are integer paise. Server Actions are the data layer. The full technical reference is in `AGENTS.md` in the [oneiros-coda-serve](https://github.com/coda-os/oneiros-coda-serve) repo.

## Build / run

Each repo has its own quickstart.

- `coda-argus-core` — `make up` after `coda-argus-infra` is running. See repo README.
- `coda-argus-edge` — Python service. See repo README.
- `coda-argus-command`, `coda-argus-fleet` — Node apps. `npm install && npm run dev`.
- `coda-argus-ml` — Python training pipeline. See repo README.
- `coda-argus-infra` — `docker compose up` for the shared stack.
- `oneiros-coda-serve` — `npm install && npm run dev`. App on `http://localhost:3000`.

## Status

Argus is in production for the Kerala Forest Department's Ele Fence initiative. Sites are running in Wayanad and Kothamangalam / Ernakulam. Detection accuracy is 9/10 on test cases after training on the dataset.

Coda is in Phase 1: core ordering, kitchen display, payment integration, and customer loyalty are operational. Piloting at Bridge cafe.

`coda-argus-fleet` and `coda-argus-ml` are not yet at first release.

## License

Proprietary. Copyright (c) 2025–2026 Oneiros Coda Private Limited.
