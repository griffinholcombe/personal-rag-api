# Personal RAG API

A production-ready Retrieval-Augmented Generation (RAG) API that retrieves context from your documents and generates accurate answers using local AI models. Built with FastAPI, containerized with Docker, and deployed to Kubernetes with automated CI/CD pipelines.

## Overview

This project implements a complete RAG pipeline that:

- **Ingests** documents and converts them into semantic embeddings
- **Retrieves** relevant context based on semantic similarity
- **Augments** prompts with retrieved documents
- **Generates** accurate responses using local LLMs

The API is production-ready with automated testing, containerization, and cloud-native deployment capabilities.

## Tech Stack

| Layer | Technology |
| --- | --- |
| **API Framework** | FastAPI |
| **Language** | Python 3.9+ |
| **Embeddings** | SentenceTransformers (local, no external API calls) |
| **Containerization** | Docker |
| **Orchestration** | Kubernetes (deployment.yaml, service.yaml) |
| **CI/CD** | GitHub Actions |
| **Testing** | Python unittest framework |

## Architecture

### Components

```
Document Ingestion → Embedding Generation → Vector Storage →
Query Processing → Semantic Retrieval → LLM Augmentation → Response
```

**Core Modules:**

- `app.py` - FastAPI server with RAG endpoints
- `embed.py` - Embedding model initialization and query encoding
- `embed_docs.py` - Batch document processing and embedding storage
- `semantic_test.py` - Integration tests for retrieval accuracy

### Data Flow

1. **Ingestion Phase** (`embed_docs.py`)
   - Load documents from disk
   - Generate embeddings using SentenceTransformers
   - Store embeddings for efficient retrieval

2. **Query Phase** (`app.py` + `embed.py`)
   - Accept user query via HTTP endpoint
   - Encode query using same embedding model
   - Perform semantic similarity search across document embeddings
   - Retrieve top-k most relevant document chunks

3. **Response Phase**
   - Augment prompt with retrieved context
   - Pass to LLM for answer generation
   - Return complete response to client

## Key Features

- ✅ **Local-First Design** - No external API dependencies; all processing runs locally
- ✅ **Semantic Search** - Retrieves contextually relevant documents, not just keyword matches
- ✅ **Containerized** - Dockerfile for consistent deployment across environments
- ✅ **Cloud-Native** - Kubernetes manifests for scalable deployments
- ✅ **Automated Testing** - Semantic accuracy tests included
- ✅ **CI/CD Pipeline** - Automated build, test, and deployment workflows
- ✅ **RESTful API** - Clean, documented endpoints via FastAPI

## CI/CD Pipeline

Automated workflows (`.github/workflows/`) handle:

- **Build** - Docker image creation and registry push
- **Test** - Unit and semantic tests on every push
- **Deploy** - Automated deployment to Kubernetes on merge to main

## Project Structure

```
personal-rag-api/
├── app.py                 # FastAPI server
├── embed.py               # Embedding model utilities
├── embed_docs.py          # Document ingestion pipeline
├── semantic_test.py       # Integration tests
├── Dockerfile             # Container configuration
├── deployment.yaml        # Kubernetes deployment
├── service.yaml           # Kubernetes service
├── .github/workflows/     # CI/CD pipelines
├── docs/                  # Sample documents
```

## License

MIT

---

**Questions or contributions?** Feel free to open an issue or submit a pull request.
