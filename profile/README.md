# GrafeoDB

**Embeddable graph database built in pure Rust.** Dual data models (LPG + RDF), six query languages, HNSW vector search, MVCC transactions. Now in beta.

## Why Grafeo?

- **6 query languages**: GQL (ISO), Cypher, Gremlin, GraphQL, SPARQL, SQL/PGQ. Use what you know or want to learn.
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

### AI & Integrations

| Project | Description | Install |
|---------|-------------|---------|
| [**grafeo-memory**](https://github.com/GrafeoDB/grafeo-memory) | AI memory layer. Extract, reconcile, and search memories from conversations. No Docker, no Neo4j, one `.db` file + one LLM | `uv add grafeo-memory` |
| [**grafeo-mcp**](https://github.com/GrafeoDB/grafeo-mcp) | Use Grafeo as an MCP server, expose to AI agents over stdio or HTTP | `uv add grafeo-mcp` |
| [**grafeo-memory**](https://github.com/GrafeoDB/grafeo-memory) |AI memory layer powered by Grafeo | `uv add grafeo-memory` |
| [**grafeo-langchain**](https://github.com/GrafeoDB/grafeo-langchain) | LangChain GraphStore & GraphVectorStore for knowledge-graph RAG | `uv add grafeo-langchain` |
| [**grafeo-llamaindex**](https://github.com/GrafeoDB/grafeo-llamaindex) | LlamaIndex PropertyGraphStore with structured + vector queries | `uv add grafeo-llamaindex` |

### Benchmarking

| Project | Description |
|---------|-------------|
| [**graph-bench**](https://github.com/GrafeoDB/graph-bench) | Custom benchmark suite using LDBC benchmarks, 25 tests across 8 graph database engines |
| [**ann-benchmarks**](https://github.com/GrafeoDB/ann-benchmarks) | Fork of [ann-benchmarks](https://github.com/erikbern/ann-benchmarks) extended with a Grafeo HNSW adapter for vector search benchmarking |

## Links

- [Documentation](https://grafeo.dev)
- [Docker Hub](https://hub.docker.com/r/grafeo/grafeo-server)
- [crates.io](https://crates.io/crates/grafeo)
- [PyPI grafeo](https://pypi.org/project/grafeo/)
- [PyPI grafeo-memory](https://pypi.org/project/grafeo-memory/)
- [PyPI grafeo-langchain](https://pypi.org/project/grafeo-langchain/)
- [npm](https://www.npmjs.com/package/@grafeo-db/js)

