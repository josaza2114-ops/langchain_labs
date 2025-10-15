# Gemini-Powered RAG Pipeline
Retrieval-Augmented Generation (RAG) using LangChain, Chroma, and Gemini 1.5 — built from scratch in Jupyter for transparency and education.

---

## Overview
This project is a local-first RAG setup that:
- Ingests your private documents into ChromaDB using Sentence-Transformers embeddings
- Retrieves the most relevant context for any query
- Uses Gemini 1.5 (Pro / Flash) via Google’s API to generate grounded answers
- Runs inside a Jupyter Notebook (or Streamlit UI later)
- Keeps dependencies isolated in a virtual environment (.LVenv)

Built for learning, experimentation, and extensibility — not a black box.

---

## Architecture
```mermaid
flowchart TD
    A[Documents (.txt, .md)] -->|load & split| B[LangChain Splitter]
    B -->|embed| C[Sentence Transformers MiniLM-L6-v2]
    C -->|store| D[ChromaDB]
    E[User Query] --> F[Retriever]
    D --> F
    F --> G[Gemini LLM]
    G --> H[Final Answer]
```

---

## Setup Instructions

### 1. Clone and create environment
```bash
git clone https://github.com/yourusername/gemini_rag_lab.git
cd gemini_rag_lab

python -m venv .LVenv
.LVenv\Scripts\activate  # (Windows)
# or: source .LVenv/bin/activate (macOS/Linux)
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

If you don’t have the file yet, generate it from your working env:
```bash
pip freeze > requirements.txt
```

### 3. Environment variables
Create a `.env` file (never commit it):
```
GOOGLE_API_KEY=your_api_key_here
DATA_PATH=./data
DB_PATH=./chroma_db
MODEL_NAME=gemini-1.5-pro
```

### 4. Run in Jupyter
Launch your notebook:
```bash
jupyter lab
```

Then open `gemini_rag.ipynb` (or your base notebook)  
and run cells sequentially:
1. Bootstrap + Gemini check
2. Ingest + Embedding to Chroma
3. Conversational QA Loop

---

## Example Interaction

```
Question: What is LangChain?
Answer: LangChain is a framework that helps build LLM-based applications by combining prompts, tools, retrievers, and chains for contextual reasoning.
```

---

## Tech Stack

| Layer | Tool |
|-------|------|
| LLM | Gemini 1.5 (Pro / Flash) |
| Framework | LangChain 0.2.x |
| Embeddings | Sentence-Transformers all-MiniLM-L6-v2 |
| Vector Store | ChromaDB |
| Environment | Python 3.12 / Jupyter |
| Memory | ConversationBufferMemory |
| UI (optional) | Streamlit |

---

## Folder Structure
```
.
├── data/               # Source documents
├── chroma_db/          # Persisted embeddings
├── .LVenv/             # Virtual environment
├── .env                # API key + configs (ignored)
├── requirements.txt
├── gemini_rag.ipynb    # Main notebook
└── README.md
```

---

## Roadmap
- [x] Core RAG retrieval pipeline  
- [x] Gemini integration  
- [x] Conversational context memory  
- [ ] Streamlit front-end UI  
- [ ] Add PDF ingestion  
- [ ] Add source citation + chunk highlighting  

---

## Security Notes
- Never commit `.env`
- Use `.gitignore` to exclude it
- Rotate your API key periodically
- Consider environment managers like `direnv` or `doppler` for secure automation

---

## License
MIT License © 2025 Jose A. Salas  
Educational use encouraged — attribution appreciated.
