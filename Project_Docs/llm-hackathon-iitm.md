# LLM Hackathon (IITM Paradox 2024) — RAG Chatbot

**Repository:** [LLM-Hackathon-IITM](https://github.com/Eyuvaraj/LLM-Hackathon-IITM)

## One-line summary
Solo-built "IITM Infobot" during a 32-hour IITM BS GenAI Hackathon: a FastAPI backend running a retrieval-augmented pipeline (PDF/HTML ingestion → Nomic embeddings → persisted ChromaDB store → score-filtered similarity search → Groq/Llama-3 generation), served through a Chainlit chat frontend, both independently Dockerized.

## Technology Stack
- **LLM**: Groq API, `llama3-70b-8192` (`dev` mode) or an OpenAI-compatible endpoint serving `meta-llama/Meta-Llama-3-8B-Instruct` (production mode) — `backend/api.py`, `backend/utils.py`.
- **Embeddings**: `nomic-embed-text-v1.5` (768-dim) — loaded locally via `sentence-transformers` for ingestion (`backend/embeddings.py`), and via Nomic's hosted API (`langchain_nomic.NomicEmbeddings`) for query-time embedding (`backend/api.py`).
- **Vector store**: ChromaDB, `PersistentClient` writing to `backend/chroma_db/` (binary index files are committed), wrapped with `langchain_chroma.Chroma`.
- **Retrieval**: `similarity_search_with_score(query, k=top_K)` with a score-threshold filter dropping low-relevance chunks (`rag_vectors()` in `api.py`).
- **Ingestion**: `PyMuPDFLoader` for PDFs, `BeautifulSoup` + `html2text` for crawled HTML pages, `RecursiveCharacterTextSplitter` (chunk_size=1024, overlap=128) — `backend/embeddings.py`. Source docs live in a gitignored `data/` folder (not committed).
- **Backend**: FastAPI, single `POST /chat` endpoint.
- **Frontend**: Chainlit chat UI (`frontend/app.py`), a thin HTTP client posting conversation history to the backend.
- **Deployment**: separate Dockerfiles for backend (`tiangolo/uvicorn-gunicorn-fastapi:python3.11`) and frontend (`python:3.11-slim`); `.deployment` files present (Azure App Service format).

## Architecture
`embeddings.py` crawls local PDF/HTML source docs, chunks them, encodes chunks with the local `nomic-embed-text-v1.5` SentenceTransformer, and upserts into a Chroma collection `IITM-BS-Data` (batched, with duplicate-ID handling). At query time, `api.py` embeds the user's message via Nomic's hosted embedding API, retrieves the top-K nearest chunks from Chroma, filters candidates using the committed Chroma distance threshold (`SCORE=0.9`), and splices the surviving chunks into a prompt template alongside a persona-locked system prompt ("IITM Infobot," restricted to IITM BS program questions, instructed not to fabricate). The augmented prompt goes to Groq/OpenAI-compatible chat completion. The Chainlit frontend is a stateless HTTP relay with no logic of its own beyond session history.

## Key Features
- Dual-mode model routing (Groq Llama-3-70B in dev vs. an OpenAI-compatible Llama-3-8B endpoint in production) with separately tuned top_K/score-threshold per mode.
- Distance-thresholded retrieval to keep irrelevant chunks out of the prompt (`rag_vectors()`).
- Persona-locked system prompt scoping the bot to IITM BS-program queries and discouraging fabricated answers.
- Batch embed-and-upsert pipeline with ID-based dedup (`vec-{type}_{i}`, `DuplicateIDError` handling).
- Two independently containerized services (backend :5000, frontend :8000).

## Outcome
Built IITM Infobot as a solo participant during a 32-hour hackathon and won first place at the IITM BS GenAI Hackathon during Paradox 2024. The competition included more than 30 teams, with up to five members per team; the project received a ₹25,000 prize.

## Key Highlights

- Engineered a retrieval-augmented chatbot that chunks IITM program PDFs and HTML, embedding content with `nomic-embed-text-v1.5` into a persisted ChromaDB store.
- Built a Chroma distance-thresholded retrieval layer in FastAPI to filter low-relevance chunks before generation.
- Implemented dual-mode LLM routing with Groq Llama 3 in development and an OpenAI-compatible Llama 3 endpoint in production.
- Containerized the FastAPI backend and Chainlit frontend as independent Docker services.
- Won first place at the IITM BS GenAI Hackathon during Paradox 2024, competing solo against 30+ teams and receiving a ₹25,000 prize.
