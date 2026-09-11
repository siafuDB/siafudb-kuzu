# Contributing to SiafuDB

Thank you for your interest in contributing to SiafuDB. Every contribution strengthens the colony.

SiafuDB is an open-source project maintained by [Nyuchi Africa](https://nyuchi.com) and governed by the [Mukoko Foundation](https://mukoko.com/foundation). We welcome contributions from everyone — whether you're fixing a typo, improving documentation, reporting a bug, or building a major new feature.

## Getting Started

### 1. Fork and Clone

```bash
git clone https://github.com/your-username/siafudb.git
cd siafudb
```

### 2. Build from Source

**Prerequisites:**

- CMake 3.15+
- C++20 compiler (GCC 11+, Clang 14+, MSVC 2022+)
- Python 3.9+ (for Python bindings)

```bash
make release
```

### 3. Run Tests

```bash
make test
```

All tests must pass before submitting a pull request.

## How to Contribute

### Reporting Bugs

- Use [GitHub Issues](https://github.com/nyuchitech/siafudb/issues) to report bugs
- Search existing issues first to avoid duplicates
- Include your environment details: OS, compiler version, language binding, SiafuDB version
- Provide a minimal reproduction case — the smallest possible code that demonstrates the bug
- Include the full error message or unexpected output

### Suggesting Features

- Use [GitHub Discussions](https://github.com/nyuchitech/siafudb/discussions) for feature ideas and design discussions
- Describe the problem you're trying to solve, not just the solution you want
- Explain how the feature fits into SiafuDB's mission (device, edge, Web3, graph sync)

### Submitting Pull Requests

1. **Create an issue first** for anything beyond trivial fixes. This lets the community discuss the approach before you invest time coding.
2. **Fork the repository** and create a feature branch from `main`:

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Write tests** for your changes. New features require tests. Bug fixes require a test that would have caught the bug.
4. **Follow the code style** (see below).
5. **Ensure all tests pass:**

   ```bash
   make test
   ```

6. **Commit with a clear message** and sign off (see below).
7. **Push to your fork** and submit a pull request against `main`.

### Commit Messages

Write clear, descriptive commit messages. Use the following format:

```
<component>: Short summary of the change (max 72 chars)

Longer description if needed. Explain what changed and why,
not how (the code shows how). Wrap at 72 characters.

Signed-off-by: Your Name <your.email@example.com>
```

**Components:** `core`, `cypher`, `storage`, `vector`, `fts`, `algo`, `sync`, `wasm`, `python`, `nodejs`, `rust`, `java`, `swift`, `kotlin`, `arkts`, `docs`, `ci`, `build`

**Examples:**

```
core: Fix memory leak in hash index scan

The hash index scan was not releasing pinned buffer pages when
the scan terminated early due to a LIMIT clause. This caused
gradual memory growth on long-running embedded instances.

Signed-off-by: Tatenda Moyo <tatenda@example.com>
```

```
sync: Add graph change log capture for vertex mutations

Implements local change log capture for VERTEX_CREATED and
VERTEX_DELETED events. Edge mutations will follow in a
subsequent PR. Part of the Graph Sync Protocol (Phase 2).

Signed-off-by: Rumbi Chikwanha <rumbi@example.com>
```

### Sign-Off (DCO)

SiafuDB uses the [Developer Certificate of Origin](https://developercertificate.org/) (DCO). Every commit must include a `Signed-off-by` line certifying that you have the right to submit the code under the Apache 2.0 licence.

Add it automatically with:

```bash
git commit -s -m "your commit message"
```

Or add it manually to your commit message:

```
Signed-off-by: Your Name <your.email@example.com>
```

## Contribution Areas

We especially welcome contributions in these areas:

### High Priority

- **Graph Sync Protocol** — CRDT-based subgraph replication between SiafuDB instances and JanusGraph. This is the most architecturally significant feature in development. Start with the [design discussion](https://github.com/nyuchitech/siafudb/discussions).
- **WASM optimisation** — Performance improvements for Cloudflare Workers and Durable Object runtimes. The existing WASM build works but needs optimisation for constrained edge environments.
- **Rebrand tracking** — Renaming internal `kuzu`/`kuzudb` references to `siafudb` across the codebase. See the [rebrand issue](https://github.com/nyuchitech/siafudb/issues).

### Always Welcome

- **Bug fixes** — especially in the core engine, query parser, and storage layer
- **Performance improvements** — query execution, storage I/O, memory usage
- **Graph algorithms** — new algorithms for the `algo` extension
- **Vector search** — ANN improvements, additional distance metrics, incremental indexing
- **Documentation** — tutorials, getting started guides, API reference, architecture docs
- **Testing** — expanded test coverage, edge cases, fuzzing, benchmarks
- **Native bindings** — Swift (iOS), Kotlin (Android), ArkTS (HarmonyOS) platform bindings

### Future Work

- **Multi-model extensions** — document (JSON/JSONB), key-value, and time-series storage alongside graph
- **Web3 pod integration** — embedded graph store for decentralised personal data pods
- **Browser improvements** — WASM-compiled graph engine for client-side use

## Code Style

### C++ (core engine)

- Follow the existing code style in the repository
- Use the included `.clang-format` configuration
- Format your code before committing:

  ```bash
  clang-format -i your_file.cpp
  ```

- Use C++20 features where they improve clarity
- Prefer `std::unique_ptr` and `std::shared_ptr` over raw pointers
- All public APIs must have documentation comments

### Python (bindings and tests)

- Follow PEP 8
- Use type hints for function signatures
- Format with `black` and lint with `ruff`

### General

- No trailing whitespace
- End files with a newline
- Use UTF-8 encoding
- Keep lines under 120 characters where practical

## Pull Request Review

All pull requests require at least one review from a project maintainer before merging. Reviewers will look for:

- **Correctness** — Does the code do what it claims?
- **Tests** — Are there sufficient tests? Do they cover edge cases?
- **Performance** — Does the change introduce regressions? (Benchmark for hot-path changes)
- **Style** — Does the code follow the project's conventions?
- **Documentation** — Are new features documented? Are changes reflected in relevant docs?
- **Scope** — Is the PR focused on a single concern? (Split large changes into smaller PRs)

Don't be discouraged by review feedback — it's how we maintain quality together. Every contributor's code gets reviewed, including maintainers'.

## Community

- **[GitHub Discussions](https://github.com/nyuchitech/siafudb/discussions)** — Questions, ideas, design discussions
- **[GitHub Issues](https://github.com/nyuchitech/siafudb/issues)** — Bug reports, feature requests, task tracking
- **<conduct@siafudb.org>** — Code of Conduct concerns

Please read our [Code of Conduct](CODE_OF_CONDUCT.md) before participating in any community space.

## Licence

By contributing to SiafuDB, you agree that your contributions will be licensed under the [Apache License, Version 2.0](LICENSE). You retain copyright over your contributions.

The Apache 2.0 licence will never change. SiafuDB is governed by the Mukoko Foundation — a legal entity with no shareholders that exists for the community. The Foundation's charter structurally prevents relicensing.

---

_Every contribution strengthens the colony. Every ant matters._

_Built with Ubuntu — I am because we are._
