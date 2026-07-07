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

## Getting Started

### Prerequisites

- Python 3.9+
- Docker (for containerized setup)
- Kubernetes cluster (for cloud deployment)

### Local Setup

```bash
# Clone the repository
git clone https://github.com/griffinholcombe/personal-rag-api.git
cd personal-rag-api

# Install dependencies
pip install -r requirements.txt

# Prepare your documents (place .txt or .pdf files in docs/)
# Then generate embeddings
python embed_docs.py

# Start the API server
python app.py
```

The API will be available at `http://localhost:8000`

### API Endpoints

```bash
# Health check
GET /health

# Query the RAG system
POST /query
Content-Type: application/json

{
  "question": "Your question here"
}
```

### Docker Setup

```bash
# Build the Docker image
docker build -t personal-rag-api .

# Run the container
docker run -p 8000:8000 personal-rag-api
```

### Kubernetes Deployment

```bash
# Apply Kubernetes manifests
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

# Verify deployment
kubectl get pods
kubectl get svc personal-rag-api
```

## Testing

Run semantic tests to validate retrieval accuracy:

```bash
python semantic_test.py
```

Tests verify that:

- Retrieved documents are semantically relevant to queries
- Embedding similarity scores are within expected ranges
- Response generation works end-to-end

## CI/CD Pipeline

Automated workflows (`.github/workflows/`) handle:

- **Build** - Docker image creation and registry push
- **Test** - Unit and semantic tests on every push
- **Deploy** - Automated deployment to Kubernetes on merge to main

## Key Skills Demonstrated

- **Backend Development** - FastAPI, REST API design, async Python
- **Machine Learning** - Embeddings, semantic search, vector databases
- **DevOps** - Docker containerization, Kubernetes orchestration
- **CI/CD** - GitHub Actions workflow automation
- **Testing** - Unit tests, integration tests, semantic validation
- **Cloud Native** - Microservices architecture, container deployments

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
└── requirements.txt       # Python dependencies
```

## Future Enhancements

- [ ] Multi-model support for embeddings
- [ ] Caching layer for frequently accessed documents
- [ ] Async document processing for large datasets
- [ ] Metrics and monitoring integration
- [ ] Admin endpoints for document management

## License

MIT

---

**Questions or contributions?** Feel free to open an issue or submit a pull request.
