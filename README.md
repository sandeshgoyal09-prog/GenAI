# DebuggersGPT: AI-Powered Chat & Knowledge Assistant

## Project Overview

DebuggersGPT is an intelligent assistant platform designed to help users troubleshoot, search, and retrieve information across multiple sources—such as web, documents, logs, and emails—using advanced AI and retrieval techniques. The application provides a seamless chat interface where users can ask questions, get contextual answers, and interact with a system that combines large language models (LLMs), semantic search, and retrieval-augmented generation (RAG).

**Key Purpose:**

- Empower users (developers, support teams, SREs, etc.) to quickly find answers, root causes, and documentation by chatting with an AI that understands context and can search across web, help docs, logs, and emails.
- Streamline troubleshooting, knowledge discovery, and information retrieval in complex environments.
- Integrate authentication, chat history, and extensible agent workflows for a robust, enterprise-ready solution.

---

## Overview

DebuggersGPT is a full-stack application that combines a React-based frontend with a Python Flask backend to deliver an AI-powered chat assistant. The system leverages advanced LLMs (Gemini, LangChain, etc.), semantic search (FAISS, ElasticSearch), and RAG (Retrieval-Augmented Generation) pipelines to answer user queries using web, document, log, and email data. It supports user authentication, chat history, and multi-source knowledge retrieval.

---

## Features

- **Conversational AI Chatbot**: React frontend for real-time chat with an AI assistant.
- **User Authentication**: JWT-based login, registration, and session management.
- **Chat History**: Persistent, user-specific chat history stored in MongoDB.
- **Multi-Source Knowledge Retrieval**:
  - Web search (via SerpAPI)
  - Help documents (PDF, PPT, etc.)
  - Logs and alert emails (ElasticSearch, FAISS)
- **RAG Pipelines**: Contextual answers using document and log retrieval.
- **Blob Storage Integration**: Upload/download documents via Azure Blob Storage.
- **Extensible Agentic Workflow**: Modular agent design for routing queries to specialized agents/tools.

---

## Architecture

```
Frontend (React + Redux + Tailwind)
	 |
	 | REST API (JWT Auth)
	 v
Backend (Flask, LangChain, LLMs)
	 |
	 |-- MongoDB (User, Chat History)
	 |-- ElasticSearch (Logs)
	 |-- FAISS (Docs/Emails)
	 |-- Azure Blob Storage
```

---

## Frontend

- **Stack**: React, Redux Toolkit, TailwindCSS, Axios
- **Key Components**:
  - `Login`, `Register`: User authentication
  - `Chat`, `Messages`, `Conversation`: Chat UI, message rendering, chat selection
  - `CustomPopup`, `Header`: UI utilities
- **State Management**: Redux store for user, chat, and app state
- **API Integration**: Axios services for chat, login, and registration

---

## Backend

- **Stack**: Python, Flask, Flask-JWT-Extended, MongoDB, LangChain, FAISS, ElasticSearch, Azure SDK
- **Key Modules**:
  - `app.py`: Flask app, CORS, JWT setup, blueprint registration
  - `routes/`: Auth, assistant (AI query), chat history endpoints
  - `service/`: Business logic for chat, authentication, RAG, blob storage
  - `database/`: MongoDB connection, user and chat history repositories
  - `mail_bot/`: Scripts for ingesting and indexing emails (FAISS)
  - `help_doc_rag/`, `logs_emails_rag/`: RAG pipelines for docs/logs
- **Agentic Workflow**:
  - Modular agents route queries to web, docs, or logs/email search tools
  - Prompts and tools are extensible for new data sources
- **RAG Pipelines**:
  - PDF/PPT ingestion, chunking, embedding (Gemini, FAISS)
  - Log/email ingestion, embedding (ElasticSearch, FAISS)
  - Conversational retrieval with context/history

---

## Data Flow

1. **User logs in/registers** (JWT issued)
2. **User sends a chat message**
3. **Frontend calls backend `/query` endpoint**
4. **Agentic workflow routes query** to web/doc/log/email agent/tool
5. **Relevant data retrieved** (web, docs, logs, emails)
6. **LLM generates answer** (RAG pipeline)
7. **Answer and chat history saved** in MongoDB
8. **Frontend updates chat UI**

---

## Setup & Installation

### Prerequisites

- Node.js, npm (for frontend)
- Python 3.10+, pip, virtualenv/pyenv (for backend)
- MongoDB, ElasticSearch, Azure Blob Storage credentials

### Frontend

```bash
cd HackAthon18Frontend-main
npm install
npm start
```

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py
```

- Configure `.env` with MongoDB, ElasticSearch, Azure, and API keys as needed.

---

## Key Environment Variables

- `DB_URI`: MongoDB connection string
- `JWT_SECRET_KEY`: Secret for JWT
- `ELASTIC_SEARCH_*`: ElasticSearch config
- `AZURE_STORAGE_CONNECTION_STRING`, `AZURE_STORAGE_CONTAINER_NAME`: Azure Blob Storage
- `GOOGLE_API_KEY`: Gemini/Google GenAI

---

## Extending & Customizing

- **Add new agents/tools** in `service/agentic_workflow/agents/`
- **Add new RAG pipelines** in `service/help_doc_rag/` or `service/logs_emails_rag/`
- **Integrate new data sources** by extending prompts and tool definitions

---

## License

MIT License

---

## Authors

- [Your Name/Team]

---

## Acknowledgements

- LangChain, Gemini, Flask, React, MongoDB, ElasticSearch, Azure

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
