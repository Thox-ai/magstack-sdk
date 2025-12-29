# MagStack™ SDK

<div align="center">

[![Coming Soon](https://img.shields.io/badge/Status-Coming%20Soon-purple?style=for-the-badge)](https://thox.ai)
[![Public Beta](https://img.shields.io/badge/Public%20Beta-Q2%202026-blue?style=for-the-badge)](https://thox.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

**Official SDK for MagStack™ Magnetic Clustering Technology**

[Documentation](https://thox.ai/docs/magstack-sdk) • [Website](https://thox.ai) • [Discord](https://discord.gg/thoxai)

</div>

---

> **🚀 Coming Soon - Public Beta**
>
> The MagStack™ SDK is currently in private development and will be released as a public beta alongside the Thox.ai Edge Device launch. Join our [waitlist](https://thox.ai) to get early access!

---

## Overview

MagStack™ enables modular AI computing through magnetically-coupled device clusters. This SDK provides comprehensive tools for:

- **Cluster Management**: Monitor topology, power contracts, and node health
- **Distributed Inference**: OpenAI-compatible API for running AI models across clusters
- **Model Management**: Load, unload, and manage AI models
- **Device Discovery**: Find MagStack devices on your network
- **Cluster Coordination**: Leader election and distributed coordination

## Quick Links

- [Full Specification](./SPECIFICATION.md)
- [Protocol Definition](./protocol/magstack.proto)
- [TypeScript SDK](./typescript/)
- [Python SDK](./python/)
- [Examples](./examples/)

## Roadmap

| Phase | Status | Description |
|-------|--------|-------------|
| **Alpha** | ✅ Complete | Internal testing with partner developers |
| **Private Beta** | 🔄 In Progress | Limited access for early adopters |
| **Public Beta** | 📅 Q2 2026 | Open access with Thox.ai device launch |
| **1.0 Release** | 📅 Q3 2026 | Production-ready stable release |

### Upcoming Features

- [ ] TypeScript SDK v1.0
- [ ] Python SDK v1.0
- [ ] React hooks for cluster status
- [ ] CLI tool for development
- [ ] WebSocket streaming support
- [ ] Async batch inference
- [ ] Model fine-tuning API

## Installation

> **Note:** Packages will be published to npm and PyPI when the public beta launches. For now, you can build from source for early access.

### TypeScript/JavaScript

```bash
# Coming soon to npm
npm install @thox/magstack-sdk

# Build from source (early access)
git clone https://github.com/Thox-ai/magstack-sdk.git
cd magstack-sdk/typescript
npm install && npm run build
```

### Python

```bash
# Coming soon to PyPI
pip install magstack-sdk

# Build from source (early access)
git clone https://github.com/Thox-ai/magstack-sdk.git
cd magstack-sdk/python
pip install -e .
```

## Quick Start

### TypeScript

```typescript
import { MagStackClient } from '@thox/magstack-sdk';

const client = new MagStackClient({
  host: '192.168.1.100',
  apiKey: 'your-api-key'
});

// Get cluster status
const cluster = await client.cluster.getStatus();
console.log(`${cluster.nodeCount} nodes, ${cluster.totalTops} TOPS`);

// Run inference
const response = await client.inference.chat({
  model: 'llama-3.1-8b',
  messages: [{ role: 'user', content: 'Hello!' }]
});
```

### Python

```python
from magstack import MagStackClient

client = MagStackClient("192.168.1.100", api_key="your-api-key")

# Get cluster status
cluster = client.cluster.get_status()
print(f"{cluster.node_count} nodes, {cluster.total_tops} TOPS")

# Run inference
response = client.inference.chat(
    model="llama-3.1-8b",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

## SDK Components

### Client Libraries

| Component | TypeScript | Python |
|-----------|------------|--------|
| Core Client | ✅ | ✅ |
| Cluster Management | ✅ | ✅ |
| Inference API | ✅ | ✅ |
| Model Management | ✅ | ✅ |
| Device Discovery | ✅ | ✅ |
| Coordinator | ✅ | ✅ |

### Host Daemon (Rust)

The `magstackd` daemon runs on Thox.ai devices and provides:

- REST API for cluster management
- MS-Link protocol handling
- Power contract negotiation
- Topology management

### Module Firmware (C)

Reference firmware for accessory modules:

- MS-Link framing implementation
- Power negotiation
- CRC32 validation
- Safe state handling

### Protocol Definition

The MagStack protocol uses protobuf for message serialization:

- `magstack.proto` - Full protocol schema
- Message types for discovery, power, firmware, and control
- Forward-compatible design

## Development

### Build All Components

```bash
make all
```

### Run Tests

```bash
make test
```

### Generate Test Vectors

```bash
make vectors
```

### Full CI Pipeline

```bash
make ci
```

## Project Structure

```
magstack-sdk/
├── SPECIFICATION.md      # Full SDK specification
├── README.md             # This file
├── Makefile              # Build automation
├── protocol/             # Protobuf definitions
│   └── magstack.proto
├── typescript/           # TypeScript/JavaScript SDK
│   ├── src/
│   └── package.json
├── python/               # Python SDK
│   ├── magstack/
│   └── pyproject.toml
├── host-daemon/          # Rust host daemon
│   ├── src/
│   └── Cargo.toml
├── module-fw/            # C module firmware
│   ├── src/
│   ├── include/
│   └── CMakeLists.txt
├── tests/                # Conformance tests
│   ├── test_*.py
│   └── requirements.txt
└── examples/             # Usage examples
    ├── typescript/
    └── python/
```

## Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                     MagStack Cluster                          │
├──────────────────────────────────────────────────────────────┤
│  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐   │
│  │ Device  │────│ Device  │────│ Device  │────│ Module  │   │
│  │ (Node)  │    │ (Node)  │    │ (Leader)│    │         │   │
│  └────┬────┘    └────┬────┘    └────┬────┘    └────┬────┘   │
│       │              │              │              │        │
│       └──────────────┴──────────────┴──────────────┘        │
│                    MS-Link Data Bus                          │
├──────────────────────────────────────────────────────────────┤
│                    Shared Power Plane                        │
└──────────────────────────────────────────────────────────────┘
```

## API Endpoints

### Inference API (Port 8080)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/v1/chat/completions` | POST | Chat completion |
| `/v1/completions` | POST | Text completion |
| `/v1/embeddings` | POST | Generate embeddings |
| `/v1/models` | GET | List models |

### Cluster API (Port 5381)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/v1/topology` | GET | Get cluster topology |
| `/v1/cluster` | GET | Get cluster status |
| `/v1/nodes` | GET | List all nodes |
| `/v1/power/contract` | POST | Negotiate power |
| `/v1/health` | GET | Get health status |

## Certification

MagStack™ certification ensures safe interoperability:

| Tier | Capabilities |
|------|--------------|
| Tier C | Power-only (charging + magnetic attach) |
| Tier B | Power + MS-Link + telemetry |
| Tier A | Full-trust (power + data + firmware + cluster) |

## Get Notified

Want to know when the public beta launches?

- **Waitlist**: [Join at thox.ai](https://thox.ai) for early access
- **Discord**: [discord.gg/thoxai](https://discord.gg/thoxai) for community updates
- **Twitter**: [@ThoxAI](https://twitter.com/ThoxAI) for announcements
- **GitHub**: Watch this repo for release notifications

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

> **Note:** Public contributions will be accepted starting with the public beta in Q2 2026. Until then, please join our Discord to share feedback and ideas.

## Support

- **Documentation**: [thox.ai/docs/magstack-sdk](https://thox.ai/docs/magstack-sdk)
- **Issues**: [GitHub Issues](https://github.com/Thox-ai/magstack-sdk/issues)
- **Email**: developers@thox.ai
- **Discord**: [discord.gg/thoxai](https://discord.gg/thoxai)

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Trademark

MagStack™ is a trademark of Thox.ai LLC. The MagStack magnetic stacking and automatic cluster formation technology is proprietary and patent pending.

---

<div align="center">

**Built with precision by [Thox.ai](https://thox.ai)**

*Bringing frontier AI to the edge*

</div>
