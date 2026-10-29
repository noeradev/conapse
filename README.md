<div align="center">
  
# conapse

**Privacy-first, ultra-lightweight social context engine & personal memory co-pilot**

Passively ingests chat streams · extracts structured long-term facts & relationship graphs via LLM · serves context summaries and prompts via Telegram Mini App

![status](https://img.shields.io/badge/status-concept-orange)
![go](https://img.shields.io/badge/go-1.24+-00ADD8?logo=go&logoColor=white)
![next.js](https://img.shields.io/badge/next.js-16-black?logo=next.js)
![postgres](https://img.shields.io/badge/postgres-pgvector-4169E1?logo=postgresql&logoColor=white)
![license](https://img.shields.io/badge/license-MIT-green.svg)

</div>

---

## Concept

**Conapse** (*Context + Synapse*) is an open-source, privacy-first social intelligence engine designed to solve human memory limits in digital communication.

It works as an asynchronous personal co-pilot that listens to messaging streams, extracts key relational facts (preferences, life events, habits), maintains a dual-layer memory store, and presents structured user dossiers and context prompts via a Telegram Mini App.

---

## Key Principles

- **Passive Event Listener** — operates as a passive MTProto update listener. No automated spamming, no aggressive polling, zero rate-limit risks.
- **Asynchronous Fact Extraction** — message streams are buffered locally and batched during conversation lulls, then processed via lightweight LLM models (e.g., DeepSeek-V3 / `gpt-4o-mini` via OpenRouter).
- **Fact Invalidation** — temporal resolution mechanism to update evolving preferences while preserving historical context.
- **Dual-Layer Memory Architecture**:
  - **Relational Store (PostgreSQL):** Structured dossiers, core preferences, and relationship trees.
  - **Vector Store (`pgvector`):** High-performance semantic search over past topics and historical context within the same database engine.
- **Privacy-First & Self-Hosted** — personal messages, vector embeddings, and API keys never leave your local environment.

---

## Planned Stack

| Layer | Stack | Role |
|---|---|---|
| **Engine** | Go, `gotd/td`, PostgreSQL + `pgvector` | MTProto listener, LLM extraction pipeline, vector & relational memory store |
| **MiniApp** | Next.js 16, React 19, FSD, Tailwind | Embedded Telegram Mini App for viewing dossier cards & relationship graphs |
| **Contracts** | Protobuf, ConnectRPC | Type-safe API contract between Go engine and Next.js client |
| **Deployment** | Docker Compose | Isolated self-hosted runtime |

---

## Architecture (Concept)

```
                                  [ Telegram MTProto ]
                                           │
                                    (gotd/td Event)
                                           │
                                           ▼
┌──────────────┐   ConnectRPC   ┌─────────────────────┐   OpenRouter API   ┌─────────────────┐
│   miniapp    │───────────────▶│       engine        │───────────────────▶│ DeepSeek / LLM  │
│ Next.js 16   │                │        Go           │                    │ Fact Extraction │
└──────────────┘                └──────────┬──────────┘                    └─────────────────┘
                                           │
                                ┌──────────┴──────────┐
                                ▼                     ▼
                        [ Relational Store ]  [ Vector Memory ]
                            (PostgreSQL)         (pgvector)
```

---

## Status

> **Note:** This project is currently in the **Concept & Planning** phase.

---

## License

Copyright © 2026 Maxim Potapchenko.

This project is licensed under the **PolyForm Noncommercial License 1.0.0**. You are free to modify, inspect, and redistribute this software for personal and non-commercial purposes, provided that original copyright attribution is preserved. Commercial use, resale, or deployment as a paid managed service is strictly prohibited without explicit written consent from the author.
```
