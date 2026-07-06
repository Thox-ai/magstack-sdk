<!-- thox-badges -->
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=flat-square&labelColor=09090b)](LICENSE)
[![THOX.ai](https://img.shields.io/badge/THOX.ai-portfolio-0a0a0a?style=flat-square&labelColor=09090b)](https://thox.ai)
[![Status](https://img.shields.io/badge/status-coming%20soon-9b59b6?style=flat-square&labelColor=09090b)](https://github.com/Thox-ai/magstack-sdk)
[![Release](https://img.shields.io/github/v/release/Thox-ai/magstack-sdk?style=flat-square&labelColor=09090b&logo=github)](https://github.com/Thox-ai/magstack-sdk/releases)
[![Last Commit](https://img.shields.io/github/last-commit/Thox-ai/magstack-sdk?style=flat-square&labelColor=09090b)](https://github.com/Thox-ai/magstack-sdk/commits/main)
[![Issues](https://img.shields.io/github/issues/Thox-ai/magstack-sdk?style=flat-square&labelColor=09090b)](https://github.com/Thox-ai/magstack-sdk/issues)
<!-- /thox-badges -->

# MagStack SDK

Official SDK for MagStack magnetic clustering technology, by Thox.ai LLC.

> **Status: Coming Soon.** The MagStack SDK is in private development and will
> be released as a public beta alongside the THOX Nova device launch. This
> repository currently contains the specification overview and license; the
> TypeScript/Python client libraries, `magstackd` host daemon, module firmware
> reference, and protocol definition will land here at public beta. Join the
> waitlist at [thox.ai](https://thox.ai) for early access.

## Overview

MagStack enables modular AI computing through magnetically-coupled device
clusters. THOX Nova devices stack magnetically and automatically form a
compute cluster over the MS-Link data bus and a shared power plane.

**Architecture scope.** MagStack is a **cluster fabric only**:

- **Data-parallel workloads**: supported (batched inference sharded across
  nodes).
- **Task-parallel workloads**: supported (independent models/services across
  nodes).
- **Model-parallel sharding**: deferred to a future board revision. Single
  large models are not split across nodes in the current MagStack generation.

The SDK provides tools for:

- **Cluster Management**: monitor topology, power contracts, and node health.
- **Distributed Inference**: OpenAI-compatible API for running models across
  the cluster (data-parallel and task-parallel).
- **Model Management**: load, unload, and manage models per node.
- **Device Discovery**: find MagStack devices on the network.
- **Cluster Coordination**: leader election and distributed coordination.

## Planned Components

| Component | Language | Status |
|-----------|----------|--------|
| Client libraries (TS + Python) | TypeScript, Python | Forthcoming |
| `magstackd` host daemon | Rust | Forthcoming |
| Module firmware reference | C | Forthcoming |
| Protocol definition (`magstack.proto`) | Protobuf | Forthcoming |
| Examples | Mixed | Forthcoming |

Until public beta, packages are not published to npm/PyPI and the source
directories are not yet present in this repository.

## Conceptual Architecture

```
+--------------------------------------------------------------+
|                     MagStack Cluster                          |
+--------------------------------------------------------------+
|  +---------+    +---------+    +---------+    +---------+    |
|  | Device  |----| Device  |----| Device  |----| Module  |    |
|  | (Node)  |    | (Node)  |    | (Leader)|    |         |    |
|  +----+----+    +----+----+    +----+----+    +----+----+    |
|       |              |              |              |         |
|       +--------------+--------------+--------------+         |
|                    MS-Link Data Bus                           |
+--------------------------------------------------------------+
|                    Shared Power Plane                         |
+--------------------------------------------------------------+
```

## Planned API Surface

### Inference API (port 8080, OpenAI-compatible)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/v1/chat/completions` | POST | Chat completion |
| `/v1/completions` | POST | Text completion |
| `/v1/embeddings` | POST | Generate embeddings |
| `/v1/models` | GET | List loaded models |

### Cluster API (port 5381)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/v1/topology` | GET | Get cluster topology |
| `/v1/cluster` | GET | Get cluster status |
| `/v1/nodes` | GET | List all nodes |
| `/v1/power/contract` | POST | Negotiate power |
| `/v1/health` | GET | Get health status |

## Certification Tiers

MagStack certification ensures safe interoperability:

| Tier | Capabilities |
|------|--------------|
| Tier C | Power-only (charging + magnetic attach) |
| Tier B | Power + MS-Link + telemetry |
| Tier A | Full-trust (power + data + firmware + cluster) |

## Roadmap

| Phase | Description |
|-------|-------------|
| Alpha | Internal testing with partner developers |
| Private Beta | Limited access for early adopters |
| Public Beta | Open access with the THOX Nova device launch |
| 1.0 | Production-ready stable release |

## Current Repository Contents

```
magstack-sdk/
├── LICENSE      # MIT license (Thox.ai LLC)
└── README.md    # This overview
```

Client libraries, daemon, firmware, and protocol source will be added here at
public beta.

## Get Notified

- **Waitlist**: [thox.ai](https://thox.ai) for early access
- **Discord**: [discord.gg/thoxai](https://discord.gg/thoxai) for community updates
- **GitHub**: Watch this repo for release notifications

## Support

- **Documentation**: [thox.ai/docs/magstack-sdk](https://thox.ai/docs/magstack-sdk)
- **Issues**: [GitHub Issues](https://github.com/Thox-ai/magstack-sdk/issues)
- **Email**: developers@thox.ai

## Trademark

MagStack is a trademark of Thox.ai LLC. The MagStack magnetic stacking and
automatic cluster formation technology is proprietary and patent pending.

## Legal

Copyright (c) 2026 Thox.ai LLC. All rights reserved.

Thox.ai LLC is an independent Texas limited liability company.

- **Tommy Xaypanya** - Chief Technology Officer (CTO)
- **Craig Ross** - Chief Executive Officer (CEO)

Licensed under the [MIT License](LICENSE).