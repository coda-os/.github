# Coda OS

Coda OS builds two products: **Argus**, an elephant-detection and early-warning system for human–wildlife conflict, and **Coda**, an operating system for restaurants.

## Argus

Argus is a distributed system. Edge nodes (Jetson Orin Nano / Raspberry Pi) run detection on-site, publish events to `coda-argus-core` over MQTT, and receive OTA updates and control commands. Postgres + TimescaleDB, Redis, MinIO and the MQTT broker are shared infrastructure.

| Repo | What it is | Status |
| --- | --- | --- |
| coda-argus-core | Central platform API. Auth, device management, event ingestion, fleet state, OTA, alerts, telemetry, analytics. Java 21, Spring WebFlux. | active |
| coda-argus-edge | On-site runtime. Camera capture, AI detection, event publishing, local actuation. | active |
| coda-argus-command | Forest-department dashboard. Login, live monitoring, alerts, remote control. | active |
| coda-argus-fleet | Engineering dashboard. OTA pushes, device management, logs. | in development |
| coda-argus-ml | Training pipeline for the detection models delivered OTA to the edge. | in development |
| coda-argus-infra | Deployment automation. Docker, Kubernetes, Terraform, CI/CD. | active |

**Status:** in production for the Kerala Forest Department's Ele Fence initiative, with sites running in Wayanad and Kothamangalam / Ernakulam. Detection accuracy is 9/10 on test cases after training on the dataset.

## Coda

Coda is the restaurant operating system: ordering, kitchen workflow, payments, customer retention and analytics. It is a single Next.js 16 application on Supabase, with Clerk for auth, Inngest for background jobs, and PhonePe (primary) and Razorpay (fallback) for payments.

| Repo | What it is | Status |
| --- | --- | --- |
| oneiros-coda-serve | The Coda application. | active |
| coda-os | Marketing site, [oneiros-coda.in](https://oneiros-coda.in). | maintained |

**Status:** Phase 1. Ordering, kitchen display, payment integration and customer loyalty are operational. Piloting at Bridge cafe.

## License

Proprietary. Copyright (c) 2025–2026 Oneiros Coda Private Limited.
