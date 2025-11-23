# PaperMind – Document Intelligence & RAG Platform

PaperMind is a full-stack Retrieval-Augmented Generation (RAG) platform designed to transform unstructured PDFs into searchable knowledge and provide accurate, context-grounded answers through a conversational interface.

The system combines:
- A React frontend  
- A FastAPI backend  
- A fully automated ingestion pipeline  
- Qdrant as a vector database  
- OpenAI models for embeddings, HyDE generation, reranking, and summarization  

The goal is to deliver a scalable and reliable document-questioning experience that supports research, technical documentation, and complex multi-PDF workflows.

---

## 🚀 Core Features

### **1. Automated PDF Ingestion Pipeline**
Once PDFs are uploaded, PaperMind triggers a background pipeline that runs independently of user-facing requests:

- PDF → JSON conversion  
- Metadata enrichment (title, topic, keywords, language)  
- Semantic chunking  
- Embedding generation (OpenAI `text-embedding-3-large`)  
- Upsert into Qdrant  
- Cleanup of temporary files  

The pipeline is async, fault-tolerant, and designed to handle multiple documents in parallel.

---

### **2. Vector Search Powered by Qdrant**
Qdrant stores:
- Document-level vectors  
- Chunk-level vectors  
- Topic centroid vectors  

It enables:
- High-performance semantic search  
- Filtering by topic, discipline, filename, or level  
- Scalable HNSW indexing for low-latency retrieval  

This provides the backbone for all RAG operations.

---

### **3. Hybrid Retrieval-Augmented Generation**
PaperMind’s retrieval flow is designed for accuracy and robustness:

- Query embedding  
- Query rewriting (multiple paraphrases)  
- HyDE (Hypothetical Document Embeddings)  
- Vector search over multiple variants  
- LLM-based reranking (gpt-4o-mini)  
- Context summarization  
- Final answer generation with source grounding  

This multi-step pipeline significantly improves recall and quality compared to standard vector search alone.

---

### **4. Real-Time Conversational Interface**
The React frontend provides:

- Streaming chat responses  
- Markdown rendering (with code blocks)  
- Persistent conversation history  
- Scenario-building form sidebar  
- PDF upload interface with drag-and-drop  
- PDF export of answers (jsPDF)

---

### **5. Backend API (FastAPI)**
The backend exposes:

- `/ask` – streaming LLM responses  
- `/api/upload-pdfs` – file ingestion  
- `/api/processing-status` – pipeline progress  
- `/convos` – conversation history  
- `/config-debug` – debug mode visibility  

The API is stateless and easy to scale horizontally behind an ASGI server.

---

## 🏗️ System Architecture (High-Level)

Frontend (React)
|— Chat UI / Streaming
|— PDF Upload
|— Conversation Management
↓
Backend (FastAPI)
|— Streaming Chat Endpoint
|— Upload Endpoint
|— RAG Controller
↓
Background Pipeline
|— pdfTojson
|— json_enrichment
|— vector_store_service
↓
Qdrant Vector Store
|— Document Vectors
|— Chunk Vectors
|— Topic Centroids
↓
OpenAI LLMs
|— Embeddings
|— HyDE
|— Reranking
|— Summarization
|— Final Chat Model

yaml
Copy code

---

## ⚙️ Tech Stack

**Frontend**
- React (Hooks + Context)
- Markdown rendering (react-markdown)
- Streaming via ReadableStream API

**Backend**
- FastAPI  
- httpx (streaming OpenAI responses)
- PyMuPDF  
- Python-dotenv  
- Subprocess-based pipeline orchestration  

**Vector Store**
- Qdrant Cloud (HNSW index)

**LLM / AI**
- OpenAI GPT-4o-mini (rerank + summarize + HyDE)
- text-embedding-3-large (embeddings)

---

## 📦 Pipeline Components

| Component                | Responsibility                                        |
|--------------------------|--------------------------------------------------------|
| `pdfTojson.py`           | Text extraction + initial JSON                         |
| `json_enrichment.py`     | Metadata enrichment + summary                          |
| `vector_store_service.py`| Embedding + Qdrant upsert                              |
| `main_embeding.py`       | Orchestration + logging + cleanup                      |

All components run in isolation from the API to guarantee responsiveness.

---

## 🔒 Security & Privacy

- Uploaded PDFs are not retained long-term  
- Temporary files are cleaned after embedding  
- API keys stored only server-side  
- Qdrant interactions over HTTPS  
- No client-side secrets  
- No user data shared between tenants  

---

## 📈 Scalability

- FastAPI is stateless → horizontally scalable  
- Qdrant cluster autoscales  
- Pipeline can run multiple workers in parallel  
- React is fully static → deploy anywhere (CDN, S3, Netlify, etc.)  
- Vector search O(log n) due to HNSW topology  

---

## ⚠️ Known Limitations

- HyDE increases latency and cost  
-  figures or curve of a function may be poorly RAGed if complex as PDF-to-text
extractor llm might find them difficult to describe 
- Summaries are constrained strictly to retrieved context  

---

## 🔮 Future Improvements

- Adaptive semantic chunking  
- OCR + layout parsing for tables and figures  
- Cross-document reasoning (multi-hop retrieval)  
- Caching layer for embeddings and HyDE  
- Local embedding model fallback  
- Fine-grained access control + encryption  

---

## 📥 Code Access

The full source code for PaperMind is stored in a **private GitHub repository**.  
To maintain IP protection and prevent unauthorized reuse, access is granted **upon request**.

If you are a recruiter, hiring manager, or interviewer and would like to review the code,  
**please contact me and I will provide read-only access.**
please contact me with your:
Full name
Company / Role
GitHub username

You can reach me at:

Email: walid7benmaarouf@gmail.com
LinkedIn: www.linkedin.com/in/walid-benmaarouf-08089a275
---

## 📄 License
This project is private and not licensed for public redistribution.

---

## 👤 Author
**Walid BENMAAROUF**

AI & Computer Vision Engineer  

Based in France 🇫🇷

For questions or read-only code access, feel free to contact me.
