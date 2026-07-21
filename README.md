# 🤖 Telegram AI RAG Assistant

A complete Retrieval-Augmented Generation (RAG) workflow built with **n8n**, **OpenAI**, and **Supabase Vector Store**. This project enables an AI assistant to answer user questions on Telegram using information retrieved from a private knowledge base instead of relying only on the language model.

---

# 📌 Overview

This workflow demonstrates how to build an AI-powered customer support assistant that combines Large Language Models (LLMs) with Retrieval-Augmented Generation (RAG).

The workflow starts by downloading documents from Google Drive, extracting the PDF content, generating vector embeddings with OpenAI, and storing them inside Supabase Vector Store.

When a user sends a message through Telegram, the AI Agent performs a semantic search against the vector database, retrieves the most relevant information, and generates an accurate answer based only on the retrieved documents.

This approach significantly reduces hallucinations while allowing the assistant to answer questions using private company knowledge.

---

# ⚙️ Workflow Architecture

```
Google Drive
      │
      ▼
Download PDF
      │
      ▼
Extract PDF Text
      │
      ▼
Generate Embeddings
      │
      ▼
Supabase Vector Store
      │
────────────────────────────
      │
Telegram Trigger
      │
      ▼
AI Agent
      │
      ▼
Retrieve Context (RAG)
      │
      ▼
OpenAI
      │
      ▼
Telegram Response
```

---

# 🚀 Features

- 🤖 AI-powered Telegram assistant
- 📄 Automatic PDF document processing
- 🧠 Retrieval-Augmented Generation (RAG)
- 🔍 Semantic search using vector embeddings
- 💬 Telegram Bot integration
- 📚 Private knowledge base
- ⚡ OpenAI Embeddings
- 🗂️ Supabase Vector Database
- 🧩 Conversation Memory
- 🔒 Reduces AI hallucinations
- 🚀 Fully automated n8n workflow

---

# 🛠️ Technologies Used

- n8n
- OpenAI GPT
- OpenAI Embeddings
- Supabase
- Supabase Vector Store
- PostgreSQL
- Google Drive API
- Telegram Bot API

---

# 📂 Knowledge Ingestion Pipeline

The first part of the workflow is responsible for creating the knowledge base.

It automatically:

- Downloads PDF documents from Google Drive
- Extracts text from PDF files
- Converts the text into vector embeddings
- Stores the embeddings inside Supabase Vector Store

This process only needs to run whenever new documents are added or existing documents are updated.

---

# 🧠 Retrieval-Augmented Generation (RAG)

Instead of answering directly from the language model, the AI Agent first searches the vector database.

The retrieval process is:

1. Receive the user's question.
2. Convert the question into an embedding.
3. Search Supabase Vector Store.
4. Retrieve the most relevant document chunks.
5. Send the retrieved context to OpenAI.
6. Generate the final answer.

This allows the assistant to answer using your own documents rather than relying on general model knowledge.

---

# 💬 Telegram Integration

The workflow listens for incoming Telegram messages.

For every message:

- The user sends a question.
- The AI searches the knowledge base.
- The most relevant information is retrieved.
- The final response is generated.
- The answer is automatically sent back to Telegram.

---

# 📦 Use Cases

- Customer Support
- Internal Company Assistant
- Restaurant Menu Assistant
- Product Catalog Search
- FAQ Bot
- HR Knowledge Base
- Technical Documentation
- SOP Assistant
- Employee Handbook
- Private AI Chatbot

---

# 📈 Benefits

- Accurate answers from private data
- Reduced hallucinations
- Easy document updates
- Fast semantic search
- No manual searching
- Scalable architecture
- Easy to customize
- Production-ready workflow

---

# 📸 Workflow Preview

<img width="1600" height="900" alt="rag picture workflow" src="https://github.com/user-attachments/assets/7d101c0e-d85d-4c6c-81ef-6b5e29bba048" />

---

# 🏷️ Tags

`n8n`
`OpenAI`
`RAG`
`Supabase`
`Vector Database`
`Embeddings`
`Telegram`
`AI Agent`
`Automation`
`Workflow`
`Semantic Search`
`No-Code`
`Low-Code`
`Artificial Intelligence`

---

⭐ If you found this project useful, consider giving it a star!
