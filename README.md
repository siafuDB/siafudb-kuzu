<div align="center">

# SiafuDB

**The embedded graph database for device, edge, and Web3.**

*Named after the African army ant (Dorylus) — small, embedded, unnoticed,*
*but the ecosystem collapses without it.*

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/nyuchitech/siafudb.svg)](https://github.com/nyuchitech/siafudb/stargazers)

[Website](https://siafudb.org) · [Documentation](https://siafudb.org/docs) · [Getting Started](https://siafudb.org/docs/getting-started) · [Community](https://github.com/nyuchitech/siafudb/discussions)

</div>

---

## What is SiafuDB?

SiafuDB is an embedded, high-performance property graph database purpose-built for environments where server-side databases cannot reach — mobile devices, edge runtimes, Web3 nodes, and browsers.

SiafuDB is forked from [KuzuDB](https://github.com/kuzudb/kuzu) v0.11.3, which was archived when Apple acquired Kùzu Inc. in October 2025. The original MIT-licensed codebase has been relicensed under **Apache 2.0** — and will never change. This is a structural guarantee enforced by the [Mukoko Foundation](https://mukoko.com/foundation), not a corporate promise.

### Why SiafuDB?

Every major platform — Facebook, Google, Amazon, Netflix — started with relational databases and spent billions building graph layers on top of them. The relational model was designed in 1970 for accounting ledgers. The human brain is a graph. AI systems reason over graphs. The world is connected through relationships, not rows.

Server-side graph databases (Neo4j, JanusGraph, TigerGraph) solve this for the cloud. But the device, the edge, and the decentralised web have been left behind — still running SQLite, still thinking in tables.

SiafuDB brings graph-native intelligence to every environment where data lives:

- **On your phone** — your AI assistant reasons over your personal knowledge graph locally, even offline
- **At the edge** — Cloudflare Workers and Durable Objects hold cached regional subgraphs via WASM
- **In your Web3 node** — sovereign personal data stored as a graph, cryptographically bound to your identity
- **In your browser** — WASM-compiled graph engine running client-side with zero server dependency

### Key Features

**Inherited from KuzuDB v0.11.3:**
- Embedded C++ engine — runs in-process, zero network overhead, sub-millisecond queries
- OpenCypher query language — the same Cypher used by Neo4j and the emerging GQL standard
- Columnar storage with SIMD-vectorised execution — 374x faster than Neo4j on path queries
- Vector search (ANN) — semantic similarity queries for AI/ML workloads
- Full-text search — built-in text indexing
- Graph algorithms — PageRank, community detection, shortest path
- Multi-language bindings — Python, Java, Node.js, Rust, C, C++
- WebAssembly support — runs in browsers and WASM runtimes
- Single-file database format — easy backup, replication, encryption

**Built by Nyuchi (in development):**
- **Graph Sync Protocol** — CRDT-inspired bidirectional subgraph replication between SiafuDB instances and server-side graph databases (JanusGraph)
- **WASM edge runtime** — optimised compilation for Cloudflare Durable Objects and Workers
- **Web3 pod integration** — embedded graph store for decentralised personal data pods
- **Multi-model extensions** — document, key-value, and enhanced vector storage alongside graph
- **Native mobile bindings** — Swift/iOS, Kotlin/Android, ArkTS/HarmonyOS

## Quick Start

### Python
```bash
pip install siafudb
```

```python
import siafudb

db = siafudb.Database('./my_graph.db')
conn = siafudb.Connection(db)

# Create schema
conn.execute("CREATE NODE TABLE Person(name STRING, age INT64, PRIMARY KEY (name))")
conn.execute("CREATE REL TABLE Knows(FROM Person TO Person, since INT64)")

# Add data
conn.execute("CREATE (:Person {name: 'Tatenda', age: 28})")
conn.execute("CREATE (:Person {name: 'Rumbi', age: 25})")
conn.execute("""
    MATCH (a:Person {name: 'Tatenda'}), (b:Person {name: 'Rumbi'})
    CREATE (a)-[:Knows {since: 2020}]->(b)
""")

# Query
result = conn.execute("MATCH (a:Person)-[:Knows]->(b:Person) RETURN a.name, b.name")
while result.has_next():
    print(result.get_next())
```

### Node.js
```bash
npm install siafudb
```

### Rust
```bash
cargo add siafudb
```

### Java
```xml
<dependency>
    <groupId>com.siafudb</groupId>
    <artifactId>siafudb</artifactId>
</dependency>
```

## Architecture

SiafuDB is designed as one half of a two-engine graph fabric:

| Environment | Engine | Query Language | Role |
|-------------|--------|---------------|------|
| Server (cloud) | JanusGraph on ScyllaDB/Cassandra | Gremlin + Cypher | Platform knowledge graph (billions of nodes) |
| Device (mobile) | **SiafuDB** (native) | Cypher | Personal subgraph, offline AI reasoning |
| Edge (CDN) | **SiafuDB** (WASM) | Cypher | Cached regional subgraphs |
| Web3 (pod) | **SiafuDB** (embedded) | Cypher | Sovereign personal data graph |
| Browser (web) | **SiafuDB** (WASM) | Cypher | Client-side graph cache |

The **Graph Sync Protocol** connects SiafuDB instances to the server-side JanusGraph, enabling bidirectional subgraph replication. Write on your phone, sync to the cloud. Update on the platform, sync to your device. One graph, expressed everywhere.

## Building from Source

### Prerequisites
- CMake 3.15+
- C++20 compiler (GCC 11+, Clang 14+, MSVC 2022+)
- Python 3.9+ (for Python bindings)

### Build
```bash
git clone https://github.com/nyuchitech/siafudb.git
cd siafudb
make release
```

### Run Tests
```bash
make test
```

For detailed build instructions, see the [Developer Guide](https://siafudb.org/docs/developer-guide).

## Roadmap

### Phase 1 — Foundation (Current)
- [x] Fork KuzuDB v0.11.3 under Apache 2.0
- [ ] Rebrand codebase (package names, imports, documentation)
- [ ] Publish initial SiafuDB releases (Python, Node.js, Rust, Java)
- [ ] Set up CI/CD pipeline
- [ ] Launch siafudb.org documentation site

### Phase 2 — Graph Sync Protocol
- [ ] Design graph change log format (vertex/edge CRUD events)
- [ ] Implement local change log capture
- [ ] Implement bidirectional sync with JanusGraph
- [ ] CRDT-based conflict resolution for concurrent edits
- [ ] Integration with CouchDB replication protocol

### Phase 3 — Edge & WASM
- [ ] Optimised WASM compilation for Cloudflare Workers/DOs
- [ ] Geographic subgraph caching in Durable Objects
- [ ] User subgraph caching in Durable Objects
- [ ] Browser-based graph engine improvements

### Phase 4 — Web3 & Pod
- [ ] Nyuchi Honeycomb node integration
- [ ] Cryptographic binding to identity tokens
- [ ] Pod replication across Honeycomb nodes
- [ ] Heritage graph transformation (PII stripping on ancestral transition)

### Phase 5 — Multi-Model Extensions
- [ ] Document storage (JSON/JSONB as vertex properties)
- [ ] Key-value operations
- [ ] Enhanced vector search (multiple dimensions, configurable metrics)
- [ ] Time-series support

### Phase 6 — Native Platform Bindings
- [ ] Swift/SwiftUI binding (iOS) via C interop
- [ ] Kotlin/JVM binding (Android) improvements
- [ ] ArkTS/ArkUI binding (HarmonyOS) via N-API
- [ ] React Native bridge

## Contributing

We welcome contributions to SiafuDB. Whether it's bug fixes, performance improvements, documentation, or new features — every contribution strengthens the colony.

Please read our [Contributing Guide](CONTRIBUTING.md) before submitting a pull request. By contributing to SiafuDB, you agree that your contributions will be licensed under the Apache 2.0 License.

### Code of Conduct

SiafuDB is built on the Ubuntu philosophy — *I am because we are*. We are committed to providing a welcoming and inclusive environment for everyone. Please read our [Code of Conduct](CODE_OF_CONDUCT.md).

## Licence

SiafuDB is licensed under the [Apache License, Version 2.0](LICENSE).

The original KuzuDB source code is licensed under the [MIT License](THIRD_PARTY_NOTICES). The MIT copyright notice is preserved as required.

**The Apache 2.0 licence will never change.** SiafuDB is governed by the [Mukoko Foundation](https://mukoko.com/foundation) (Mauritius, Foundations Act 2012) — a legal entity with no shareholders that exists for the community. The Foundation's charter structurally prevents relicensing. This is not a promise. It is a legal guarantee.

## About

SiafuDB is maintained by [Nyuchi Africa](https://nyuchi.com) and governed by the [Mukoko Foundation](https://mukoko.com/foundation).

Nyuchi Africa is building [Mukoko](https://mukoko.com) — Africa's super app, targeting one billion users across 54 African countries. SiafuDB is the embedded graph engine that powers every device, every edge node, and every sovereign data pod in the Mukoko ecosystem. Built in Africa. Shared with the world.

---

<div align="center">

*The army ant carries the graph.*

**[Website](https://siafudb.org)** · **[Documentation](https://siafudb.org/docs)** · **[GitHub](https://github.com/nyuchitech/siafudb)** · **[Community](https://github.com/nyuchitech/siafudb/discussions)**

</div>
