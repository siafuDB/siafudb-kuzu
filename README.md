# SiafuDB-Kuzu

> An Apache 2.0 fork of the archived KuzuDB C++ engine, held as the
> high-performance counterpart to the pure-Rust [SiafuDB](https://siafudb.org).

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Upstream: MIT](https://img.shields.io/badge/upstream-KuzuDB_MIT-yellow.svg)](THIRD_PARTY_NOTICES)
![C++](https://img.shields.io/badge/C%2B%2B-20-00599C?logo=cplusplus&logoColor=white)
![Status](https://img.shields.io/badge/divergence-none_yet-lightgrey)

- **Default branch:** `master`
- **Fork point:** [`kuzudb/kuzu@89f0263`][fork] (10 Oct 2025)
- **Licence:** Apache 2.0, upstream MIT preserved
- **Sibling:** [`siafuDB/siafudb`](https://github.com/siafuDB/siafudb)

[fork]: https://github.com/kuzudb/kuzu/commit/89f0263cc7a1fd9c396d2c4953747a013556a7f9

---

## What this repository is

This is a **fork**, not a product. It exists to keep the KuzuDB C++ engine
alive under a licence the Bundu Foundation can build on, after Kùzu Inc. was
acquired by Apple in October 2025 and
[`kuzudb/kuzu`](https://github.com/kuzudb/kuzu) was archived.

Read this section before reading anything else in the tree, because the tree
does not yet say any of it:

**The source is upstream's, unchanged.** Six files differ from the upstream
fork point — `README.md`, `LICENSE`, `THIRD_PARTY_NOTICES`, `CONTRIBUTING.md`,
`CODE_OF_CONDUCT.md` and `.github/FUNDING.yml`. Not one line of C++ has been
modified. The CMake project is still `project(Kuzu VERSION 0.11.2.2)`, the
headers are still `kuzu.hpp`, the build still produces `kuzu` artefacts, and
roughly sixteen hundred files under `src/` still say Kuzu. Anything you read
in `docs/`, `examples/`, `test/` or the extension tree is upstream KuzuDB
documentation describing upstream KuzuDB behaviour. It is accurate about the
engine and says nothing about SiafuDB.

**The relicensing is the change that has actually been made.** Upstream is
MIT. `LICENSE` in this repository is the Apache License 2.0, © 2026 Nyuchi
Africa (Pvt) Ltd and SiafuDB Contributors. The MIT licence and the Kùzu Inc.
copyright notice are reproduced in full in
[`THIRD_PARTY_NOTICES`](THIRD_PARTY_NOTICES), as MIT requires; that file is
the authoritative attribution and must not be removed or summarised. The
"Kuzu" and "KuzuDB" names and trademarks belong to their owners and are not
claimed by this project.

**Nothing is published.** There is no SiafuDB-Kuzu release, package or
binary. `pip install siafudb`, `npm install siafudb` and `cargo add siafudb`
do not work — nothing has been published under those names on any registry.
Build from source, or use upstream KuzuDB directly.

## The fork point, precisely

**Upstream repository** — [`kuzudb/kuzu`](https://github.com/kuzudb/kuzu),
archived, MIT.

**Commit forked** — `89f0263cc7a1fd9c396d2c4953747a013556a7f9`, "remove logo
(#6054)", 10 October 2025.

**What that commit is** — the final commit on upstream `master`. This fork is
byte-identical to upstream `master` at the moment it was archived.

**In-tree version string** — `0.11.2.2` in `CMakeLists.txt`; extension
version `0.11.1`.

**Relationship to the `v0.11.3` tag** — the upstream `v0.11.3` tag sits on a
**separate release branch**. Measured from this fork point it is 20 commits
behind and 92 ahead; the two histories diverged. This fork does **not**
contain the `v0.11.3` tag.

The repository description and `THIRD_PARTY_NOTICES` both describe this fork
as "KuzuDB v0.11.3". That is a reasonable shorthand for _the engine as it
stood at the end of upstream's life_, and it is what the attribution notice
says, so it is left alone — but the commit above is the exact provenance, and
it is what a licence audit or a rebase should work from.

## Why the fork exists

SiafuDB is an embedded property graph database for environments a server-side
database cannot reach: phones, edge runtimes, Web3 nodes, browsers. The
Foundation is pursuing that in two tracks.

| Track     | Language             | State                                 |
| --------- | -------------------- | ------------------------------------- |
| Primary   | Rust, on [Grafeo][g] | 5-crate workspace, 0.1.0, pre-release |
| This fork | C++20                | Preserved upstream, no divergence yet |

[g]: https://grafeo.dev

The primary track is [`siafuDB/siafudb`](https://github.com/siafuDB/siafudb);
this fork is `siafuDB/siafudb-kuzu`.

The Rust track is where new SiafuDB work happens. This fork is the archive
and the reference: it preserves a complete, working, Apache-2.0-licensed
implementation of worst-case-optimal joins, factorised execution,
morsel-driven parallelism and columnar SIMD execution, so that the published
research behind them can be re-implemented in Rust with the original source
available to check against. See the "Engine Roadmap" in
[`siafuDB/siafudb`](https://github.com/siafuDB/siafudb#engine-roadmap) for
how that is sequenced.

## What the upstream engine does

Unchanged from KuzuDB v0.11.x, and documented upstream rather than here:
an embedded C++ engine with openCypher, columnar storage with vectorised
execution, vector (ANN) and full-text search, graph algorithms, WebAssembly
builds, a single-file database format, bindings for Python, Java, Node.js,
Rust, C and C++, and the extension set under `extension/` (algo, azure,
delta, duckdb, fts, httpfs, iceberg, json, llm, neo4j, postgres, sqlite,
unity_catalog, vector).

For how to use any of it, read the upstream project's documentation. This
README deliberately does not restate it — a copy would only drift.

## Building

Upstream's build, unchanged:

```bash
git clone https://github.com/siafuDB/siafudb-kuzu.git
cd siafudb-kuzu
make release
make test
```

Requires CMake 3.15+ and a C++20 compiler (GCC 11+, Clang 14+, MSVC 2022+);
Python 3.9+ for the Python bindings. The GitHub Actions workflows in
`.github/workflows/` are upstream's build and benchmark matrix and are
inherited as-is.

## If you are picking this up

The work this fork has not done, in the order it should be done:

1. Decide whether the C++ engine is actually going to diverge. If the answer
   is no, say so here and treat the repository as a licence-preserving
   archive.
2. If yes: rename the project in `CMakeLists.txt`, decide what happens to
   `kuzu.hpp` and the 1,600 files carrying the upstream name, and write down
   the compatibility promise for anyone who links against it.
3. Reconcile the governance line — see below.
4. Only then publish anything.

## Licence and governance

This fork is licensed under the [Apache License, Version 2.0](LICENSE).

The original KuzuDB source is licensed under the MIT License. That licence
and the Kùzu Inc. copyright notice are reproduced in
[`THIRD_PARTY_NOTICES`](THIRD_PARTY_NOTICES) and are preserved as MIT
requires.

**The Apache 2.0 licence will not change.** SiafuDB is governed by the
**Bundu Foundation** (Zimbabwean Company Limited by Guarantee) — a legal
entity with no shareholders that exists for the community — and operated by
[Nyuchi](https://nyuchi.com). The Foundation's charter structurally prevents
relicensing.

> **Known inconsistency.** `THIRD_PARTY_NOTICES` names "the Mukoko Foundation
> Ltd (Mauritius)" as the governing entity. The Bundu Foundation is the
> governance body across the estate, and the sibling
> [`siafuDB/siafudb`](https://github.com/siafuDB/siafudb) says so. That notice
> is a licensing document and is left untouched by this README change;
> correcting it is a separate, deliberate edit.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) and
[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md). Contributions are licensed under
Apache 2.0.

SiafuDB is built on the Ubuntu philosophy — _I am because we are_.

---

_The army ant carries the graph._
