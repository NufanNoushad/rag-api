# RAG API with CI/CD 

A **Retrieval-Augmented Generation (RAG) API** with a **GitHub Actions CI/CD pipeline** that automatically detects **knowledge regressions** using **semantic tests**.
Built to demonstrate production-ready AI system practices.

---

## 🚀 Project Overview

This project implements a lightweight **RAG-powered API** using FastAPI and ChromaDB, backed by a **CI/CD pipeline** that validates not just code correctness — but **answer quality**.

### Why this matters

Traditional CI pipelines only test:

* ✅ Code compiles
* ✅ Tests pass

This project goes further by:

* ❌ **Blocking deployments when critical knowledge is lost**
* ✅ Ensuring AI responses still contain required concepts (e.g. *“orchestration”* for Kubernetes)

---

## 🧠 Key Features

* **FastAPI-based RAG API**
* **ChromaDB vector store** for document embeddings
* **Mock LLM mode** for deterministic CI testing
* **Semantic regression tests** (answer-level validation)
* **GitHub Actions CI pipeline**
* **Deployment gate based on AI response quality**

---

## 🏗 Architecture

**High-level flow:**

1. Knowledge base (`k8s.txt`) stored in GitHub
2. Embeddings rebuilt on every relevant commit
3. API started in **mock LLM mode**
4. Semantic tests validate retrieved answers
5. CI blocks deployment if meaning regresses

```
Developer → GitHub → GitHub Actions → RAG API → Semantic Tests
                                          ↓
                               Pass ✅ or Block ❌
```

---

## 🔧 Tech Stack

| Category       | Tools                        |
| -------------- | ---------------------------- |
| API            | FastAPI                      |
| Vector DB      | ChromaDB                     |
| Language Model | Ollama (prod), Mock LLM (CI) |
| CI/CD          | GitHub Actions               |
| Language       | Python 3.11                  |
| Testing        | Custom semantic assertions   |

---

## 📁 Repository Structure

```
.
├── app.py                 # FastAPI RAG API
├── embed.py               # Embedding rebuild script
├── semantic_test.py       # Semantic regression tests
├── k8s.txt                # Knowledge base document
├── .github/workflows/
│   └── ci.yml             # GitHub Actions CI pipeline
└── README.md
```

---

## 🔍 Semantic Testing (Key Highlight)

Instead of checking for exact strings, this project validates **meaning**.

Example test:

```python
assert "orchestration" in answer.lower()
```

### What this catches

* Accidental removal of key concepts
* Degraded retrieval quality
* Broken embeddings
* Silent AI regressions

This is a **production-grade pattern** used in real-world AI systems.

---

## ⚙️ CI/CD Workflow

The GitHub Actions pipeline runs on changes to:

* `k8s.txt`
* `app.py`
* `embed.py`

### CI Steps

1. Checkout code
2. Set up Python 3.11
3. Install dependencies
4. Rebuild embeddings
5. Start API in **mock LLM mode**
6. Run semantic tests
7. ✅ Allow deployment or ❌ block regression

```yaml
USE_MOCK_LLM=1 uvicorn app:app --host 0.0.0.0 --port 8000 &
python semantic_test.py
```

---

## 🧪 Local Testing

### Run the API

```bash
pip install fastapi uvicorn chromadb requests
python embed.py
uvicorn app:app --reload
```

### Query the API

```bash
curl -X POST "http://127.0.0.1:8000/query" \
  -G --data-urlencode "q=What is Kubernetes?"
```

---

## 🧑‍💻 What This Project Demonstrates

* AI-aware CI/CD design
* Semantic regression prevention
* Practical RAG system architecture
* Mocking LLMs for deterministic testing
* DevOps best practices for AI products

---

## 📚 Built With

This project was built following the **NextWork AI DevOps curriculum**:

👉 [https://learn.nextwork.org/projects/ai-devops-githubactions](https://learn.nextwork.org/projects/ai-devops-githubactions)

---
