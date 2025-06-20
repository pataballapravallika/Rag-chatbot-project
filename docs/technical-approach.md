# 📘 Technical Approach: RAG-Powered FAQ Chatbot using n8n

This document outlines the rationale, implementation strategy, challenges, and improvements made while developing a **Retrieval-Augmented Generation (RAG)** based chatbot using **n8n**, **Hugging Face**, and **Pinecone**.

---

## 🔍 Problem Statement

To build a chatbot that:
- Accepts user questions via a web form or webhook.
- Retrieves relevant content from provided documents using semantic search.
- Generates accurate and ethically framed answers using a language model.
- Is fully implemented and orchestrated within the **n8n** workflow platform.

---

## 🧠 RAG System Design

### 1. **Document Processing**
- **Loader**: Used LangChain's `Default Document Loader` in n8n to ingest documents (PDF, TXT, MD).
- **Splitter**: Split the content using the `Text Splitter` node with a chunk size of **800 tokens** and 100 overlap.
- **Embeddings**: Generated using Hugging Face model:
  - `sentence-transformers/all-MiniLM-L6-v2` (dimension: 384) or
  - `distilbert-base-nli-mean-tokens` (dimension: 768)

### 2. **Vector Storage**
- Stored embeddings in **Pinecone** with:
  - Index dimension: **768**
  - Metric: **cosine**
  - Region: `us-east-1 (AWS)`
- Inserted documents via `Pinecone Vector Store` node (mode: insert).

### 3. **Retrieval Component**
- Used `Vector Store Retriever` node to fetch top 3 most similar chunks based on user query.
- Enabled similarity score for traceability.

### 4. **Augmentation**
- Combined user query + retrieved chunks inside the `Question and Answer Chain` node to form a prompt.

### 5. **Answer Generation**
- Hugging Face Inference node used with model:  
  `sentence-transformers/all-MiniLM-L6-v2`  
  for both embedding generation and answering queries.

---

## 🔧 Workflow Architecture

### 🟦 Execute Workflow
- `Google Drive` → `Default Document Loader` → `Text Splitter` → `Embeddings HF` → `Pinecone Vector Store`

### 🟩 Chat Workflow
- `Chat Trigger` → `Retriever` → `Question & Answer Chain` → `LLM (HF)` → Response to user

---

## 🧪 Testing and Sample Queries

Tested using questions like:
- *“What is Artificial Intelligence?”*
- *“How does semantic search work?”*
- *“Explain Pinecone vector storage.”*

Results were relevant, accurate, and based on uploaded documents.

---

## ⚠️ Challenges & Solutions

| Challenge | Solution |
|----------|----------|
| Hugging Face embedding model mismatch | Matched Pinecone index dimension to 768 |
| 429 Rate Limit on OpenAI | Switched to Hugging Face’s free model |
| `Missing argument: 'sentences'` in HF node | Properly structured input as array of texts |
| Execution delay | Reduced embedding size and used lightweight models |
| API Key errors | Created new key and stored securely in n8n credentials |

---

## 🛡️ Responsible AI Considerations

- Responses include source context and never hallucinate if answer is unknown.
- Ensured privacy by processing only local or authorized documents.
- Handled errors gracefully with fallback messages.

---

## 📈 Future Improvements

- Add **conversation memory** to retain history across queries.
- Integrate **real-time document indexing** with webhook on upload.
- Support for **Slack/Discord** via webhook triggers.
- Enable **multi-modal input** (images, tables).
- Cache frequent questions for faster response.

---

## ✅ Summary

The chatbot meets all the technical and ethical criteria for a RAG-powered assistant built on n8n. It demonstrates:
- Semantic retrieval using vector embeddings.
- Modular, reusable workflows.
- Scalable integration with Pinecone and Hugging Face.

---

### ✨ Developed by: Pravallika Pataballa
