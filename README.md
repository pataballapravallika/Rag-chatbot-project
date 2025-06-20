# Rag-chatbot-project
# 🤖 RAG-Powered FAQ Chatbot using n8n, Hugging Face & Pinecone

This project demonstrates a **Retrieval-Augmented Generation (RAG)** based FAQ chatbot built entirely using **n8n** (a no-code/low-code platform), **Hugging Face** (for text embeddings and/or LLM), and **Pinecone** (for vector storage).  
It is developed for the **Altibbe Generative AI Developer Internship** screening task.

---

## 📌 Project Highlights

- 📄 Upload document (PDF, TXT, or Markdown)
- 🔎 Semantic search on document content
- 💬 Chatbot responds with accurate answers using LLM
- 🔁 Entire flow designed in **n8n** (no full-code required)
- 🧠 Powered by Hugging Face models and Pinecone

---

## 📁 Folder Structure

    '''bash
    rag-chatbot-project/
    ├── workflows/
    │ └── rag-chatbot-workflow.json # Exported n8n workflow
    ├── scripts/
    │ └── setup.py # Optional, to automate setup
    ├── docs/
    │ ├── README.md # Main setup guide (this file)
    │ └── technical-approach.md # Implementation details
    ├── data/
    │ └── sample-documents/ # PDF/TXT/Markdown files
    ├── tests/
    │ └── sample-queries.json # Sample input-output queries


---

## 🚀 Step-by-Step Setup Guide

### 🧩 1. Prerequisites

Before you begin, ensure the following:

- ✅ n8n (installed locally or via [n8n.cloud](https://n8n.io))
- ✅ Hugging Face account & [API key](https://huggingface.co/settings/tokens)
- ✅ Pinecone account & [API key](https://app.pinecone.io/)
- ✅ Sample document (in `.pdf`, `.txt`, or `.md` format)

---

### 🛠️ 2. Create Pinecone Index

1. Go to [Pinecone Dashboard](https://app.pinecone.io/)
2. Create a new index:
   - Name: `chatbot`
   - Metric: `cosine`
   - Dimension: `768` (for distilbert / MiniLM)
   - Region: `us-east-1 (AWS)`
3. Save the **API key** and **environment**.

---

### 🧠 3. Create Hugging Face API Key

1. Visit [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)
2. Create a new token with **"read"** permission.
3. Save it safely (you'll need it for credentials in n8n).

---

### 🧪 4. Setup Credentials in n8n

1. Go to **n8n Dashboard → Credentials**
2. Create:
   - **HuggingFaceApi** with your token
   - **PineconeApi** with your index details
3. Link these credentials in relevant nodes:
   - Hugging Face Embeddings
   - Pinecone Vector Store

---

### 🧰 5. Import the Workflow in n8n

1. Go to **n8n → Workflows → Import**
2. Upload the file:  
   `workflows/rag-chatbot-workflow.json`
3. Click **Activate** or **Execute Workflow**

---

### 📥 6. Upload a Document

1. Use the `Default Document Loader` node
2. Upload any `.pdf`, `.txt`, or `.md` file (you can also connect it with Google Drive)
3. The content is automatically split and embedded using Hugging Face
4. Embeddings are stored in Pinecone

---

### 💬 7. Ask a Question (Chat Flow)

1. Trigger the chatbot by typing a question via webhook or form
2. The flow:
   - Retrieves similar chunks from Pinecone
   - Sends them with the question to the QA Chain
   - Returns a generated response using Hugging Face model

---

## 📌 Sample Questions to Test

You can test with these queries:

   ```json
    [
      "What is Artificial Intelligence?",
      "How does semantic search work?",
      "Explain RAG pipeline.",
     "What are Hugging Face embeddings?"
    ]

Refer to tests/sample-queries.json for more.

🧠 Models Used
Embedding Model: sentence-transformers/all-MiniLM-L6-v2 or distilbert-base-nli-mean-tokens

LLM (Optional): GPT-2, or use same HF model for QA chain

Ensure embedding model and Pinecone index dimensions match (e.g., 768).

🧯 Error Handling & Logs
Graceful fallback messages if document not found

All query-response pairs logged in the workflow

Retry logic and error nodes in place for robustness

📈 Suggestions for Improvement
Add Slack/Discord webhook for live queries

Enable real-time indexing when document is uploaded

Add conversation memory using Redis or database

Integrate a frontend chatbot UI using Streamlit or Bubble


👤 Author
Pataballa Pravallika
📧 pataballapravallika@gmail.com
🔗 LinkedIn
