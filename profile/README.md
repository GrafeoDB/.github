# GrafeoDB

**High-performance graph database ecosystem:** Pure Rust core with Python bindings, browser support, and visualization tools.

## Core

| Project | Description | Install |
|---------|-------------|---------|
| [**grafeo**](https://github.com/GrafeoDB/grafeo) | Embeddable graph database with LPG/RDF support, multi-language queries (GQL, Cypher, Gremlin, GraphQL, SPARQL), MVCC transactions | `uv add grafeo` / `cargo add grafeo` |
| [**grafeo-web**](https://github.com/GrafeoDB/grafeo-web) | Browser-based Grafeo via WebAssembly: zero backend, IndexedDB persistence | *Coming soon* |

## Visualization Widgets

| Project | Description | Install |
|---------|-------------|---------|
| [**anywidget-graph**](https://github.com/GrafeoDB/anywidget-graph) | Interactive graph visualization for notebooks: Sigma.js, multi-backend (Neo4j, Grafeo, ArangoDB), Cypher/GQL/SPARQL/Gremlin support | `uv add anywidget-graph` |
| [**anywidget-vector**](https://github.com/GrafeoDB/anywidget-vector) | 3D vector/embedding visualization: Three.js, 6D encoding (position, color, shape, size), multi-backend (Qdrant, ChromaDB, LanceDB) | `uv add anywidget-vector` |

## Tools

| Project | Description |
|---------|-------------|
| [**graph-bench**](https://github.com/GrafeoDB/graph-bench) | Benchmark suite comparing graph databases: 25 benchmarks across 8 engines (Grafeo, Neo4j, DuckDB, Memgraph, ArangoDB, etc.) |

## Quick Start

```python
from grafeo import Database

db = Database()
db.query("""
    INSERT (:Person {name: 'Alice'})-[:KNOWS]->(:Person {name: 'Bob'})
""")

for row in db.query("MATCH (p:Person) RETURN p.name"):
    print(row["p.name"])
```

## Links

- [Documentation](https://grafeo.dev)
- [PyPI](https://pypi.org/project/grafeo/)
- [crates.io](https://crates.io/crates/grafeo)
