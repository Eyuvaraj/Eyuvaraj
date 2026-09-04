# Projects

## QuizMaster
**Repository:** [QuizMaster](https://github.com/Eyuvaraj/QuizMaster)

Solo full-stack quiz management app: a Flask REST API (flask-restx, JWT auth) backend paired with a Vue 3 SPA frontend, with Celery/Redis background jobs handling scheduled reminders, reports, and asynchronous CSV export.

### Architecture
Two top-level folders, `Backend/` and `Frontend/`, no monorepo tooling. The backend is a Flask app using **flask-restx Namespaces/Resources** (Swagger-documented REST API), with one namespace per domain: User, Subject, Chapter, Quiz, Question, QuizLog, QuestionAnswer, Cache, Search, Task, and Export. The frontend is a Vite/Vue 3 SPA that talks to the backend purely over REST through an Axios-based service layer, with Pinia managing auth/user state.

### Key Features
- **CRUD hierarchy** Subject → Chapter → Quiz → Question, each with cascading deletes, exposed via admin-only endpoints.
- **Quiz-taking and scoring**, tracking submission state and computed scores per attempt.
- **JWT auth with decorator-enforced RBAC** (`login_required`/`admin_required`) applied across protected administrative and user routes.
- **Celery Beat crontab-scheduled background jobs** — daily quiz reminders and monthly performance reports — routed across three dedicated task queues (emails, reports, exports), backed by Redis as broker and result store.
- **Redis-backed API response caching** with automatic in-memory fallback if Redis is unreachable.
- **Asynchronous CSV export** via Celery, with progress polled through a dedicated task-status endpoint.
- A **31-component Vue 3 SPA** (Pinia, Vue Router, Chart.js) for quiz authoring, timed attempts, and performance visualization.

### Scale & Results
50 REST endpoints across 10 flask-restx namespaces, 7 SQLAlchemy models, 31 Vue single-file components, 99 commits over roughly 9 months (Jan–Oct 2025) of solo development.

**Tech Stack:**  
Flask, flask-restx, SQLAlchemy, Flask-JWT-Extended, Flask-Migrate, Celery, Redis, Vue 3, Pinia, Vue Router, Chart.js, Vite

---

## MeloVerse
**Repository:** [Meloverse](https://github.com/Eyuvaraj/Meloverse)

Solo academic Flask project (IIT Madras "MAD1" coursework) — a music streaming web app with user accounts, creator profiles, playlists, following, likes, and an admin panel with usage analytics.

### Architecture
A layered Flask structure: SQLAlchemy models in one module, three Flask **Blueprints** (`auth`, `admin`, `users`) acting as controllers, and Jinja templates as the view layer, backed by SQLite.

### Key Features
- User signup/login/logout with session-based auth.
- Playlist creation, editing, and track management.
- A **"Creator" role** letting users publish singles/albums and post announcements.
- Follow/unfollow creators and like/dislike across tracks, albums, playlists, and announcements.
- An **admin dashboard** with usage counts, top creators, and 7-day trending tracks/albums, rendered as on-demand matplotlib charts.
- One JSON API endpoint exposing song/user/creator data.

### Scale & Results
30 routes across 3 blueprints, 14 SQLAlchemy models, 59 commits over roughly 5.5 months of solo development.

**Tech Stack:**  
Flask, SQLAlchemy, Flask-Login, Jinja2, Bootstrap 5, Plyr.js, matplotlib, SQLite

---

## goboxd
**Repository:** [goboxd](https://github.com/Eyuvaraj/goboxd) *(fork)*

A Go HTTP service that sandboxes and runs untrusted code inside per-job **nsjail** sandboxes across 15 languages — a hackathon build at Paradox 2026, IIT Madras (team size up to 2 was allowed; entered and built solo).

### Architecture
A `chi` router exposes `/run` and `/v1/run` endpoints. Each submission takes a concurrency-semaphore slot, creates a per-job temp workspace, then compiles and runs test cases by shelling out to a fresh `nsjail` subprocess per step. Results (stdout/stderr, exit code, memory peak, CPU time) are read back via pipes and cgroup accounting, then mapped to a structured status (`accepted`, `wrong_output`, `time_exceeded`, `memory_exceeded`, `runtime_error`, etc.).

### Key Features
- True sandboxing via **nsjail**: a per-job PID namespace, chroot to a throwaway directory, a network namespace with no loopback, a dedicated cgroup v2 sub-tree for memory/PID accounting, and a Kafel seccomp deny-list blocking `ptrace`/`mount`/`unshare`/`chroot`/`bpf` and kernel-module syscalls.
- Resource limiting across wall time, memory (with cgroup OOM detection via `memory.events`), process count, disk, and captured output size.
- A bounded concurrency semaphore plus an optional bounded queue with 503 shedding under burst load, so the service degrades gracefully instead of failing outright.
- **15 supported languages** via declarative YAML config — adding one needs only a config entry and install script, no code changes.
- A **15-probe adversarial test harness** (fork bombs, chroot/ptrace escapes, network breakouts) verifying sandbox containment against a live instance.

### Scale & Results
101 commits, ~6,000 lines of Go, built over ~7 weeks. Load-tested to **503 req/s at 50 concurrent clients** with zero errors; a separate JVM-workload stress test found and root-caused a throughput ceiling to the concurrency semaphore size.

**Tech Stack:**  
Go, nsjail, Docker, cgroup v2, seccomp, chi

---

## IITM Infobot
Solo-built RAG chatbot: a FastAPI backend running a real retrieval-augmented generation pipeline, served through a Chainlit chat frontend. Won 1st place at the IITM BS GenAI Hackathon (Paradox, IIT Madras), ₹25,000 prize.

### Architecture
Ingests PDF/HTML source documents, chunks them, and encodes chunks with a locally loaded `nomic-embed-text-v1.5` model, upserting into a persisted ChromaDB collection. At query time, the user's message is embedded via Nomic's hosted API, the top-K nearest chunks are retrieved from Chroma, low-relevance chunks are filtered out by a similarity-score threshold, and the surviving chunks are spliced into a prompt alongside a persona-locked system prompt before going to a Groq/OpenAI-compatible chat completion.

### Key Features
- **Dual-mode LLM routing**: Groq Llama-3-70B in dev, an OpenAI-compatible Llama-3-8B endpoint in production, each with separately tuned retrieval parameters.
- **Chroma distance-thresholded retrieval** that keeps irrelevant chunks out of the prompt.
- A **persona-locked system prompt** scoping the bot to IITM BS-program queries and discouraging fabricated answers.
- A **batch embed-and-upsert ingestion pipeline** with ID-based deduplication.
- Two independently Dockerized services (backend, frontend) with Azure deployment configuration.

### Scale & Results
32 commits over a ~13-day build sprint, solo-authored. Won **1st place** at the IITM BS GenAI Hackathon (Paradox, IIT Madras) — **₹25,000 prize**.

**Tech Stack:**  
Python, FastAPI, Chainlit, ChromaDB, LangChain, Nomic Embeddings, Groq API (Llama 3), Docker
