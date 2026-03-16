
## Live Demo

https://papermind-frontend.onrender.com

> The full source code is maintained in a private repository.  
> This public repository is intended to showcase the product, architecture, features, and deployment approach.

---

# PaperMind – AI Document Intelligence Platform

PaperMind is a full-stack AI platform that transforms PDF documents into a searchable knowledge base and allows users to interact with their documents through a conversational interface powered by Retrieval-Augmented Generation (RAG).

It is designed as a modern document intelligence system with:

- a React frontend
- a FastAPI backend
- authentication with Supabase
- Google sign-in
- Bring Your Own Key (BYOK) support
- a trial mode for quick product evaluation
- automated PDF ingestion and embedding
- Qdrant for vector storage
- OpenAI-powered semantic retrieval and answer generation
- Dockerized deployment
- production deployment on Render

The goal of PaperMind is to provide a practical, deployable, and scalable AI product for document querying, technical knowledge exploration, and multi-file semantic search.

---

## Core Product Features

### 1. Authentication & User Access Management

PaperMind now includes a real access layer instead of a simple demo-only interface.

Supported access modes:

- Google authentication via Supabase Auth
- session-based secured access
- protected user flows
- trial access path for product discovery
- Bring Your Own Key (BYOK) mode for users who want to use their own OpenAI API key

This makes the project closer to a real SaaS product than a simple RAG prototype.

---

### 2. Trial Version + BYOK Mode

PaperMind supports two user experiences:

#### Trial mode
A lightweight product experience for users who want to test the platform quickly.

Typical purpose:
- evaluate the UI
- test document querying
- explore the workflow before committing

#### BYOK (Bring Your Own Key)
Users can provide their own API key to run the platform with their own usage budget.

Advantages:
- lower platform-side inference cost
- flexible experimentation
- SaaS-friendly architecture
- easier monetization path

This design is especially useful for AI products where inference cost management matters.

---

### 3. Automated PDF Ingestion Pipeline

Once PDFs are uploaded, PaperMind launches a background ingestion workflow that runs independently from chat requests.

Pipeline stages include:

- PDF to JSON conversion
- metadata extraction and enrichment
- semantic chunk preparation
- embedding generation
- vector upsert into Qdrant
- cleanup of temporary files

This pipeline is designed to keep the user-facing app responsive while documents are processed asynchronously.

---

### 4. RAG-Based Question Answering

PaperMind uses a multi-step Retrieval-Augmented Generation pipeline to improve answer quality and retrieval precision.

The retrieval flow includes:

- query embedding
- query rewriting
- multiple semantic variants
- HyDE-style retrieval expansion
- vector search in Qdrant
- reranking
- context summarization
- grounded answer generation

This architecture improves recall and reduces the weakness of naive single-query vector retrieval.

---

### 5. Vector Search with Qdrant

Qdrant is used as the semantic retrieval engine for PaperMind.

Stored vector layers include:

- document-level vectors
- chunk-level vectors
- topic-level representations

This enables:

- semantic similarity search
- scalable retrieval
- low-latency vector lookups
- flexible metadata-based filtering
- document-aware answer grounding

---

### 6. Real-Time Conversational Interface

The frontend provides a user experience closer to a real AI product than a research script.

Main capabilities:

- streaming responses
- chat-based document interaction
- persistent conversation history
- markdown rendering
- drag-and-drop PDF upload
- scenario / context side panel
- PDF export of answers

The goal is to make document interaction feel natural and product-oriented.

---

### 7. Production Deployment

PaperMind is no longer just a local prototype.

The application has been prepared for deployment with:

- Dockerized services
- separated frontend and backend images
- production deployment on Render
- managed Supabase backend services
- hosted Qdrant vector database
- cloud-ready architecture

This makes the project demonstrably closer to production engineering standards.

---

## High-Level Architecture

```text
User
↓
React Frontend
├── Authentication UI
├── Google Sign-In
├── Trial Access
├── BYOK Input
├── Chat Interface
├── PDF Upload
└── Conversation History
↓
FastAPI Backend
├── Auth-aware API layer
├── Streaming chat endpoint
├── Upload endpoint
├── Processing status endpoint
└── RAG orchestration
↓
Document Processing Pipeline
├── PDF extraction
├── JSON enrichment
├── chunk preparation
├── embedding generation
└── Qdrant upsert
↓
Qdrant Vector Store
├── document vectors
├── chunk vectors
└── topic-level representations
↓
OpenAI Models
├── embeddings
├── retrieval expansion
├── reranking
├── summarization
└── final answer generation
↓
Supabase
├── authentication
├── Google OAuth
└── user/session management
