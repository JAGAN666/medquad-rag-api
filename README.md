# 🩺 MedQuAD RAG API

A production-ready **Medical Q&A RAG system** powered by 17,000+ NIH documents from the [MedQuAD dataset](https://github.com/abachaa/MedQuAD).

**Live Demo** → [https://medquad-rag-api-243637556513.us-central1.run.app](https://medquad-rag-api-243637556513.us-central1.run.app)

---

## ✨ Features

- **Hybrid RRF Search** — Dense (NVIDIA embeddings) + Sparse (BM25) with Reciprocal Rank Fusion
- **Verbatim Answers** — Retrieves exact text from NIH XML files, no hallucination
- **17,000+ Documents** — Full MedQuAD dataset indexed in Qdrant Cloud
- **Beautiful Frontend** — Dark-themed UI served directly from FastAPI
- **Cloud Ready** — Deployed on Google Cloud Run (scales to zero when idle)

---

## 🚀 Stack

| Layer | Technology |
|---|---|
| API | FastAPI + Uvicorn |
| Embeddings | NVIDIA `llama-3.2-nv-embedqa-1b-v2` |
| Sparse Search | FastEmbed BM25 |
| Vector DB | Qdrant Cloud |
| Deployment | Google Cloud Run |

---

## ⚙️ Local Setup

```bash
# 1. Clone
git clone https://github.com/JAGAN666/medquad-rag-api.git
cd medquad-rag-api

# 2. Create virtual env
python3.10 -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# 3. Copy env file and fill in your keys
cp .env.example .env
# → Edit .env with your NVIDIA_API_KEY and Qdrant credentials

# 4. Run locally
uvicorn api:app --reload --port 8000
```

Open http://localhost:8000 to see the UI.

---

## 🌐 API Endpoints

| Endpoint | Description |
|---|---|
| `GET /` | Web UI |
| `GET /health` | Health check |
| `GET /query?q=<question>&top_k=5` | Query the RAG |
| `GET /docs` | Interactive Swagger docs |

### Example Query

```bash
curl "https://medquad-rag-api-243637556513.us-central1.run.app/query?q=symptoms+of+diabetes&top_k=3"
```

---

## ☁️ Deployment (Google Cloud Run)

```bash
gcloud run deploy medquad-rag-api \
  --source . \
  --region us-central1 \
  --allow-unauthenticated \
  --port 8080 \
  --memory 1024Mi \
  --set-env-vars "NVIDIA_API_KEY=...,QDRANT_URL=...,QDRANT_API_KEY=...,RUN_ENV=docker"
```

---

## 📄 License

MIT
