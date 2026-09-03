# QuizMaster

## One-line summary
Solo full-stack quiz management app: Flask REST API (flask-restx, JWT auth) backend + Vue 3 SPA frontend, with Celery/Redis background jobs for scheduled reminders, reports, and async CSV export.

## Technology Stack
- **Backend**: Flask 3.1.0, flask-restx 1.3.0 (Swagger/OpenAPI at `/docs`), Flask-SQLAlchemy 3.1.1, SQLAlchemy 2.0.37, Flask-JWT-Extended 4.7.1, Flask-Migrate 4.1.0 (Alembic), Flask-Caching 2.3.0, Flask-Mail 0.10.0, flask-cors 5.0.1, Celery 5.4.0, Redis (`redis` 5.2.1 client), Flower 2.0.1 (Celery monitoring), SQLite (dev DB, `instance/QuizMaster-Dev.db`).
- **Frontend**: Vue 3.5.13 (Composition API), Vue Router 4.5, Pinia 3.0 (state store), Bootstrap 5.3.7, Chart.js 4.5 (+ chartjs-adapter-date-fns), Axios, jwt-decode, Vite 6.2 build tool, Sass.

## Architecture
Two top-level folders, `Backend/` and `Frontend/`, no monorepo tooling. Backend is a Flask app using **flask-restx Namespaces/Resources** (Swagger-documented REST API) registered in `Backend/app.py` — one namespace per domain: User, Subject, Chapter, Quiz, Question, QuizLog, QuestionAnswer, Cache, Search, Task, Export. Models live in `Backend/models/Models.py` (SQLAlchemy ORM, UUID primary keys). Frontend is a Vite/Vue 3 SPA under `Frontend/src`, talking to the backend purely over REST via an Axios-based `apiClient.js`/service-layer (`services/*.js`), with Pinia for auth/user state. No server-rendered templates for the UI (Jinja2 present only as Flask's default engine, unused for pages).

## Key Features
- **CRUD hierarchy** Subject → Chapter → Quiz → Question, each with cascading deletes (`Backend/models/Models.py`), exposed via admin-only endpoints in `ChapterController.py`, `QuizController.py`, `QuestionController.py`.
- **Quiz taking + scoring**: `QuizLogController.py` and `QuestionAnswerController.py` track `UserQuizLog`/`QuestionAnswer` records, submission state, and computed score (`total_scored`).
- **JWT auth + RBAC**: `Backend/application/utils.py` defines `login_required`/`admin_required` decorators wrapping `flask_jwt_extended.jwt_required()`, applied per-route (50 `@api.route` endpoints total; decorator applied on ~35 of them per grep).
- **Search**: `SearchController.py` — separate admin vs. user search endpoints.
- **Redis-backed API caching**: `application/cache_decorators.py` initializes a real `redis.Redis` client with a graceful fallback if Redis is unreachable; `CacheController.py` (admin-only) manages cache invalidation.
- **Async CSV export**: `ExportController.py` + `tasks/export_tasks.py` — Celery tasks generate CSV of quiz history/performance, status polled via `TaskController.py`.
- **Frontend**: 31 `.vue` files (9 views, 22 components split into `admin/`, `user/`, `common/`), admin dashboard with CRUD panels, user dashboard with quiz attempt flow, Chart.js-based performance charts.

## Scheduling/background jobs
**Real and precise: Celery 5.4.0 with Celery Beat**, not plain cron or a naive scheduler. `Backend/application/celery_app.py` defines a `beat_schedule` with two `crontab`-based periodic tasks: `daily-quiz-reminders` (runs daily at a configurable hour) and `monthly-performance-reports` (runs monthly on a configurable day). Task routing splits work across three named queues (`emails`, `reports`, `exports`), backed by Redis as both broker and result backend. Actual task bodies live in `Backend/tasks/{email_tasks,report_tasks,export_tasks}.py`, each building its own Flask app context to run outside the request cycle. This is a genuine "scheduled job" system, not a misnomer — but it is Celery Beat crontab scheduling, not a custom scheduler, and quiz start/deadline "locking" itself is just a datetime comparison in the quiz-attempt endpoint, not a scheduled job.

## Auth / RBAC implementation
JWT-based (Flask-JWT-Extended), enforced via two stacked Python decorators in `application/utils.py`: `base_required` (validates JWT, loads `User` by username, returns 403 if missing) → `login_required` (any authenticated user) and `admin_required` (additionally checks `user.is_admin` boolean column, 403 otherwise). This is real decorator-based middleware, consistently applied at the route level across controllers — not ad hoc if-checks scattered in view logic (though one manual ownership check exists in `QuizLogController.py:225`: `if str(current_user.id) != user_id and not current_user.is_admin`). Only two roles: admin (single predefined account, no registration flow) and regular user.

## Scale signals
- **Endpoints**: 50 `@api.route` declarations across 10 flask-restx namespaces.
- **DB models**: 7 (User, Subject, Chapter, Quiz, Question, UserQuizLog, QuestionAnswer).
- **Frontend**: 31 Vue SFCs (9 views + 22 components).
## Key Highlights
1. Architected a Flask REST API (flask-restx, 50+ endpoints) with JWT-based role decorators enforcing admin/user permissions across protected administrative and user routes.
2. Built a Celery/Redis job pipeline with crontab-scheduled Beat tasks for daily quiz reminders and monthly performance reports.
3. Added asynchronous CSV export via Celery, polled through a dedicated task-status endpoint for progress tracking.
4. Implemented Redis-backed API caching with automatic in-memory fallback for repeated admin and search requests.
5. Developed a 31-component Vue 3 SPA (Pinia, Vue Router, Chart.js) consuming the Flask API for quiz authoring and timed quiz attempts.
6. Visualized quiz performance history in the SPA via Chart.js, sourced from the backend's scoring endpoints.
