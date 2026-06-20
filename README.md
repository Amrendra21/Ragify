# RAGify — Semantic Vector Engine

A high-performance vector database with **HNSW**, **KD-Tree**, and **Brute Force** search algorithms, plus a full **RAG (Retrieval-Augmented Generation)** pipeline powered by local AI via Ollama.

## Features

- **3 Search Algorithms**: HNSW (fast), KD-Tree (balanced), Brute Force (accurate)
- **Distance Metrics**: Cosine, Euclidean, Manhattan
- **Document Management**: Upload, chunk, embed, and search documents
- **RAG Pipeline**: Ask questions and get AI-generated answers with citations
- **Web UI**: Interactive dashboard for vector search and analytics
- **Local AI**: Powered by Ollama (100% privacy, no cloud)

## Requirements

- **C++17 or later**
- **g++ or MSVC compiler**
- **Ollama** (optional, for LLM features) — [download here](https://ollama.com)

## Quick Start

### 1. Compile

```bash
g++ -std=c++17 -O2 main.cpp -o ragify -lws2_32
```

Windows users: Add `-lws2_32` flag for socket linking.

### 2. Install Ollama (optional)

For RAG features, install Ollama and pull models:

```bash
ollama pull nomic-embed-text
ollama pull llama3.2
```

### 3. Run the Server

```bash
./ragify
# or on Windows:
ragify.exe
```

You should see:

```
=== VectorDB Engine ===
http://localhost:8080
[number] demo vectors | 16 dims | HNSW+KD-Tree+BruteForce
Ollama: ONLINE
```

### 4. Open Web UI

Navigate to **http://localhost:8080** in your browser.

---

## API Endpoints

### Demo Vector Search

- **GET** `/search?v=<vector>&k=5&metric=cosine&algo=hnsw`
- **POST** `/insert` — Add vector to database
- **DELETE** `/delete/<id>` — Remove vector
- **GET** `/items` — List all vectors
- **GET** `/benchmark` — Performance comparison

### Document + RAG

- **POST** `/doc/insert` — Upload document
- **DELETE** `/doc/delete/<id>` — Delete document
- **GET** `/doc/list` — List documents
- **POST** `/doc/search` — Semantic search
- **POST** `/doc/ask` — Full RAG pipeline (search + generate)

### Status

- **GET** `/status` — Server and Ollama status
- **GET** `/stats` — Database statistics

---

## Architecture

```
┌─────────────────────────────────────┐
│     Web UI (index.html)             │
└──────────────┬──────────────────────┘
               │ HTTP/JSON
┌──────────────▼──────────────────────┐
│  HTTP Server (httplib)              │
├─────────────────────────────────────┤
│  Vector DB        │  Document DB    │
│  ├─ HNSW          │  ├─ Embeddings  │
│  ├─ KD-Tree       │  ├─ Chunks      │
│  └─ Brute Force   │  └─ Metadata    │
└────────┬──────────┴────────┬────────┘
         │                   │
         └─────────┬─────────┘
                   │
        ┌──────────▼──────────┐
        │  Ollama (Local AI)  │
        │  ├─ Embeddings      │
        │  └─ Generation      │
        └─────────────────────┘
```

---

## Project Structure

```
Ragify/
├── main.cpp           # Core engine
├── httplib.h          # HTTP server library (header-only)
├── index.html         # Web UI
├── README.md          # This file
├── .gitignore         # Git configuration
└── LICENSE            # Open source license
```

---

## Building with CMake (Alternative)

```bash
cmake -B build
cmake --build build
./build/ragify
```

---

## Performance

Tested with 1000+ vectors:

- **HNSW**: ~1-5ms (fastest, approximate)
- **KD-Tree**: ~2-10ms (balanced)
- **Brute Force**: ~10-50ms (accurate, slow)

---

## License

MIT License — See LICENSE file for details.

---

## Contributing

Contributions welcome! Feel free to:

- Report issues
- Submit pull requests
- Improve documentation
- Add new distance metrics or algorithms

---
