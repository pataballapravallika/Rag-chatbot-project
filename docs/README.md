
---

## 🚀 Setup Instructions

### Prerequisites

- n8n (self-hosted or cloud)
- Hugging Face account + API key
- Pinecone account + API key
- A PDF or text file for testing (uploaded to Google Drive or local)

### Step-by-Step Setup

1. Clone or download the repo.
2. Open `n8n`, import `rag-chatbot-workflow.json` under **Workflows → Import**.
3. Go to **Credentials**:
   - Create Hugging Face API key
   - Create Pinecone API key
4. Update the credentials in the nodes:
   - `Embeddings HuggingFace`
   - `Pinecone Vector Store`
5. Upload a document (PDF/Text) to the data loader node.
6. Execute the **Execute Workflow** to insert vector data.
7. Open **Chat Workflow**, test with your queries.

---

## 🧪 Sample Queries

See [`tests/sample-queries.json`](../tests/sample-queries.json) for input examples like:

- "What is Artificial Intelligence?"
- "Which models are used in RAG?"
- "Explain semantic search."

---

## 📈 Performance Considerations

- Use `768` dimension embeddings for compatibility.
- Enable caching or real-time updates for scalability.
- Monitor similarity scores for evaluation transparency.

---

## 🙋‍♀️ About the Developer

This project was created by **Pataballa Pravallika** as part of the Altibbe Generative AI Internship screening task.

---

## 📫 Contact

For issues or queries:  
📧 Email: pataballapravallika@gmail.com  
🔗 LinkedIn: [linkedin.com/in/pravallika-pataballa-923572286](https://linkedin.com/in/pravallika-pataballa-923572286)

