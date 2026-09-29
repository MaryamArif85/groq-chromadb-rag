# 🤖 AI Knowledge Assistant — Groq + ChromaDB RAG

A Retrieval-Augmented Generation (RAG) application built with **FastAPI, Groq, ChromaDB, and Sentence Transformers**.

The application allows users to ask questions about a collection of local documents. Instead of relying only on the language model's general knowledge, the system first searches the provided documents for relevant information and then uses **Groq's LLM** to generate an answer based on the retrieved context.

---

## 📌 Project Overview

This project implements a complete RAG pipeline:

```text
User Question
      ↓
FastAPI Web Interface
      ↓
Question Embedding
      ↓
ChromaDB Similarity Search
      ↓
Relevant Document Chunks
      ↓
Context Construction
      ↓
Groq LLM
      ↓
Generated Answer
      ↓
Sources / Retrieved Documents

The system supports:

PDF documents
TXT files
Markdown (.md) files
Local document embeddings
Vector similarity search
Retrieval-Augmented Generation
Source information for retrieved chunks
FastAPI REST API
Browser-based user interface
ChromaDB persistent vector storage

✨ Features
**Document Ingestion**

Documents placed inside the data/ directory are automatically loaded and processed.

Supported formats:

.pdf
.txt
.md

🛠️ Technologies Used

| Technology            | Purpose                         |
| --------------------- | ------------------------------- |
| Python                | Main programming language       |
| FastAPI               | Backend API and web server      |
| Uvicorn               | ASGI server                     |
| Groq                  | Large Language Model            |
| ChromaDB              | Vector database                 |
| Sentence Transformers | Text embeddings                 |
| PyTorch               | ML framework used by embeddings |
| PyPDF                 | PDF text extraction             |
| python-dotenv         | Environment variable management |
| HTML                  | Web interface                   |
| CSS                   | UI styling                      |
| JavaScript            | Frontend API communication      |

📂 Project Structure

groq_chromadb_rag/
│
├── app/
│   ├── chunker.py
│   ├── config.py
│   ├── document_loader.py
│   ├── embedding_service.py
│   ├── groq_service.py
│   ├── ingest_service.py
│   ├── rag_service.py
│   └── vector_store.py
│
├── chroma_db/
│   └── Persistent ChromaDB storage
│
├── data/
│   ├── document1.pdf
│   ├── document2.pdf
│   ├── document3.md
│   ├── document4.md
│   ├── document5.txt
│   └── ...
│
├── templates/
│   └── index.html
│
├── static/
│   ├── style.css
│   └── script.js
│
├── .env
├── api.py
├── cli.py
├── ingest.py
├── README.md
└── requirements.txt

# 📄 Project Structure - Important Files

### `api.py`
The main FastAPI application.

It provides:
- Web interface
- Health-check endpoint
- RAG question endpoint
- Static file serving

**Main endpoints:**
- `GET /` - Serves UI
- `GET /health` - Health check
- `POST /rag/query` - RAG question answering

---

### `app/document_loader.py`
Responsible for loading documents from the `data/` directory.

Supports:
- PDF
- TXT
- Markdown

> PDF files are processed page by page.

---

### `app/chunker.py`
Responsible for splitting documents into smaller chunks.

Chunking improves retrieval because the system can retrieve specific relevant sections rather than an entire document.

---

### `app/embedding_service.py`
Responsible for generating embeddings 

📈 Current Project Results

The project has successfully demonstrated document ingestion and vector storage.

Example ingestion result:

Documents loaded: 41
Chunks stored: 114
Embedding model:
sentence-transformers/all-MiniLM-L6-v2

The same embedding process is used when ingesting documents and when processing user questions.

---

### `app/vector_store.py`
Handles interaction with ChromaDB.

Responsible for:
- Creating/accessing the ChromaDB collection
- Storing embeddings
- Storing document chunks
- Performing similarity searches
- Returning relevant results

---

### `app/ingest_service.py`
Coordinates the document ingestion process.

Flow: `Load Documents → Chunk → Generate Embeddings → Store in ChromaDB`

---

### `app/groq_service.py`
Handles communication with the Groq API.

It sends the user's question together with the retrieved document context and receives the generated answer.

---

### `app/rag_service.py`
This is the main RAG orchestration layer.

**Flow:**

Embedding Service
       ↓
ChromaDB
       ↓
Retrieved Context
       ↓
Groq LLM

Returns:
- Question
- Answer
- Retrieved sources

---

### `ingest.py`
Command-line script used to process documents and populate ChromaDB.

```bash
python ingest.py --reset



📚 RAG Architecture Summary

                 ┌──────────────────┐
                 │      User        │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   Web Interface  │
                 │ HTML/CSS/JS      │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │     FastAPI      │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Question         │
                 │ Embedding        │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │    ChromaDB      │
                 │ Vector Search    │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Relevant Chunks  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │   Groq LLM       │
                 │ Answer Generation│
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Answer + Sources │
                 └──────────────────┘

🚀 Future Improvements

Possible future improvements include:

Document upload directly from the web interface
Streaming AI responses
Conversation history
User authentication
Multiple knowledge bases
Source highlighting
Better citation formatting
Document preview
File deletion from the UI
Advanced retrieval strategies
Re-ranking retrieved chunks
Hybrid keyword + vector search
Production deployment
Chat history storage

🎯 Learning Objectives

This project demonstrates several important concepts in modern AI application development:

Retrieval-Augmented Generation (RAG)
Large Language Models
Vector databases
Semantic search
Text embeddings
Document chunking
Metadata management
FastAPI REST APIs
Frontend/backend communication
Environment variable management
Local AI application development
📚 RAG Architecture Summary
                 ┌──────────────────┐                 

👩‍💻 Author: Maryam Arif

Developed as an AI/RAG project demonstrating the integration of:

FastAPI + Groq + ChromaDB + Sentence Transformers