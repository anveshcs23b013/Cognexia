# 🧠 Cognexia: Dynamic Research Assistant (RAG)

**A Full-Stack AI Application for "Chatting" with Research Papers.** *Built for the Spazorlabs AI/ML Internship Assessment (Task 1).*

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://cognexia.streamlit.app)
[![Deployed on Render](https://img.shields.io/badge/Backend-Render-46E3B7)](https://cognexia-backend.onrender.com/docs)
[![Python 3.10](https://img.shields.io/badge/Python-3.10-blue)](https://www.python.org/)

---

**Live Demo:** [https://cognexia.streamlit.app/](https://cognexia.streamlit.app/)

## 📖 Overview

**Cognexia** is an end-to-end **Retrieval-Augmented Generation (RAG)** system that allows users to upload complex PDF documents (such as research papers) and ask questions about them. The system uses embeddings, a vector store, and an LLM to generate answers with citations pointing to page numbers in the source PDFs.

> *"Build an end-to-end RAG system with document ingestion, chunking, embeddings, vector database search, and LLM-based answer generation **with citations**."*

### 🚀 Key Features
* **📄 PDF Ingestion:** Parses complex PDF structures using `PyMuPDF` to extract text while preserving page metadata.
* **🧩 Intelligent Chunking:** Uses Recursive Character Splitting to create context-aware text chunks.
* **⚡ High-Performance Embeddings:** Optimized for memory-constrained environments using **FastEmbed** (Quantized ONNX models), reducing RAM usage compared to standard PyTorch transformers.
* **🔍 Vector Search:** Serverless vector storage and retrieval using **Pinecone** for low-latency queries.
* **🤖 LLM Reasoning:** Powered by an efficient LLM for rapid, accurate, and context-aware responses.
* **📍 Accurate Citations:** Every answer includes precise **Page Number references** so users can verify the source.
* **☁️ Cloud Native:** Deployed with a **FastAPI** backend and a **Streamlit** frontend.

---

## 🛠️ Tech Stack

| Component | Technology | Reasoning |
| :--- | :--- | :--- |
| **Frontend** | Streamlit (Python) | Rapid UI development and interactive chat interface. |
| **Backend** | FastAPI | High-performance, asynchronous REST API capabilities. |
| **LLM** | Llama-3-8b (Groq) / compatible | Fast inference for generation. |
| **Embeddings** | FastEmbed (`bge-small-en`) | Lightweight ONNX runtime (No-GPU required). |
| **Vector DB** | Pinecone | Managed serverless vector database for scalable similarity search. |
| **PDF Parser** | PyMuPDF (LangChain) | Fast and accurate text extraction with metadata support. |
| **Hosting** | Render + Streamlit Cloud | Decoupled hosting to scale logic separate from UI. |

---

## 🏗️ Architecture

1.  **Ingestion:** User uploads a PDF -> Backend chunks text -> Generates embeddings -> Stores vectors in Pinecone.
2.  **Retrieval:** User asks a question -> Query is embedded -> Pinecone returns the most relevant chunks.
3.  **Generation:** Retrieved chunks + Question are sent to the LLM -> LLM generates an answer with citations.

---

## 💻 Local Setup

If you want to run this repository locally, follow these steps.

### 1. Clone the Repository
```bash
git clone https://github.com/anveshcs23b013/Cognexia.git
cd Cognexia
```

### 2. Set Environment Variables
Create a `.env` file in the root directory and add your API keys. Example:

```bash
# .env
GROQ_API_KEY=gsk_...
PINECONE_API_KEY=pc-...
PINECONE_INDEX_NAME=cognexia-index
```

Replace the placeholders with your actual keys.

### 3. Install Dependencies
Backend:

```bash
pip install -r backend.txt
```

Frontend:

```bash
pip install -r requirements.txt
```

### 4. Run the Application
You need two terminals running simultaneously.

Terminal 1 (Backend):

```bash
uvicorn main:app --reload
```

Terminal 2 (Frontend):

```bash
streamlit run app.py
```

### 🌐 API Documentation
The backend exposes the following endpoints (Auto-generated docs available at `/docs`):

- GET / : Health check.
- POST /ingest : Uploads a PDF, processes it, and indexes vectors into Pinecone.
  - Input: file (UploadFile)
  - Output: JSON with chunk count.
- POST /chat : Asks a question to the RAG pipeline.
  - Input: query (string)
  - Output: JSON with answer and sources list.

---

## 🚧 Notes & Troubleshooting

- Memory constraints on free-tier hosts may require using lightweight embeddings and ONNX-based models.
- If the backend is sleeping (e.g., Render free tier), the first request may take longer while the service wakes up.

---

## 📄 License
This project is open-source and available under the MIT License.

Author: anveshcs23b013
