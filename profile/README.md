# GrafeoDB

**Embeddable graph database built in pure Rust.** Dual data models (LPG + RDF), five query languages, HNSW vector search, MVCC transactions.

## Why Grafeo?

- **5 query languages**: GQL (ISO), Cypher, Gremlin, GraphQL, SPARQL. Use what you know.
- **LPG + RDF in one engine**: Property graphs and triples with optimized storage for each.
- **Vector search**: HNSW indexes with scalar, binary, and product quantization. SIMD-accelerated.
- **Embeddable**: Link as a library (Rust, Python, Node.js, WASM) or run as a server. No external processes.
- **Fast(est)**: Push-based vectorized execution, morsel-driven parallelism, columnar storage with zone maps. Benchmarked with [ann-benchmarks](https://github.com/GrafeoDB/ann-benchmarks) and [graph-bench](https://github.com/GrafeoDB/graph-bench).

## Quick Start

```python
import grafeo

db = grafeo.GrafeoDB()

# Build a graph
db.execute("INSERT (:Person {name: 'Alice', age: 30})-[:KNOWS {since: 2020}]->(:Person {name: 'Bob', age: 25})")
db.execute("INSERT (:Person {name: 'Bob'})-[:KNOWS]->(:Person {name: 'Carol', age: 28})")

# Traverse it
for row in db.execute("""
    MATCH (p:Person)-[:KNOWS]->(friend)-[:KNOWS]->(fof)
    WHERE fof <> p
    RETURN p.name, fof.name AS friend_of_friend
"""):
    print(row)
```

## Ecosystem

### Core

| Project | Description | Install |
|---------|-------------|---------|
| [**grafeo**](https://github.com/GrafeoDB/grafeo) | Embeddable graph database engine | `uv add grafeo` / `cargo add grafeo` / `npm install @grafeo-db/js` |
| [**grafeo-server**](https://github.com/GrafeoDB/grafeo-server) | HTTP server & web UI: REST API, transactions, ~40MB Docker image | `docker pull grafeo/grafeo-server` |
| [**grafeo-web**](https://github.com/GrafeoDB/grafeo-web) | Browser-based Grafeo via WebAssembly with IndexedDB persistence | `npm install @grafeo-db/web` |

### Visualization

| Project | Description | Install |
|---------|-------------|---------|
| [**anywidget-graph**](https://github.com/GrafeoDB/anywidget-graph) | Interactive graph visualization for notebooks (Marimo, Jupyter, VS Code, Colab) | `uv add anywidget-graph` |
| [**anywidget-vector**](https://github.com/GrafeoDB/anywidget-vector) | 3D vector/embedding visualization with 6D encoding | `uv add anywidget-vector` |

### Benchmarking

| Project | Description |
|---------|-------------|
| [**graph-bench**](https://github.com/GrafeoDB/graph-bench) | Custom benchmark suite using LDBC benchmarks, 25 tests across 8 graph database engines |
| [**ann-benchmarks**](https://github.com/GrafeoDB/ann-benchmarks) | Fork of [ann-benchmarks](https://github.com/erikbern/ann-benchmarks) extended with a Grafeo HNSW adapter for vector search benchmarking |

## Links

- [Documentation](https://grafeo.dev)
- [Docker Hub](https://hub.docker.com/r/grafeo/grafeo-server)
- [crates.io](https://crates.io/crates/grafeo)
- [PyPI](https://pypi.org/project/grafeo/)
- [npm](https://www.npmjs.com/package/@grafeo-db/js)

