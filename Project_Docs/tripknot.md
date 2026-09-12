# TripKnot — Aneeras LLP

## Company and Product Context

[Aneeras LLP](https://aneeras.com/) is a product-first technology startup founded in 2026 around TripKnot as its core idea and first product. [TripKnot](https://tripknot.in/) is an AI-assisted travel platform for personalized day-by-day itineraries, destination and hidden-gem discovery, curated escapes, map-based exploration, and group travel.

The complete TripKnot ecosystem includes a traveler mobile application, partner-facing business portal, internal admin console, public website, backend services, and a destination-data platform. Its technical foundation combines a FastAPI monolith, an LLM-driven itinerary generator, an identity-verification workflow for group travel, one purpose-specific scoring microservice, Next.js web interfaces, and an Expo/React Native mobile application.

## Founding Team and Delivery Context

I am one of five founding team members and one of three full-stack engineers. The team consists of three full-stack engineers, one UI/UX developer, and one frontend developer. We formed Aneeras around the TripKnot idea and coordinated the product, design, data, engineering, and release work as one founding team.

We built TripKnot from the ground up and released the product within five months of beginning development. The work started with product definition and destination data and progressed through the backend, consumer mobile application, business portal, admin console, public website, deployment pipeline, and production operations.

## System Overview
- **`backend`** — FastAPI (Python 3.12), MongoDB via Beanie ODM, ~21,000 lines of application code, 185 API endpoints across 23 domain routers (auth, itineraries, trips, users, destinations, places, states, admin, analytics, notifications, badges/gamification, reviews, promos, claims, storage, search, discover, home, saved, categories, business, ingestion). Firebase for identity; a custom email-OTP flow; Gemini (primary) + Groq/Llama (fallback) for LLM calls with structured JSON output; Inngest for background/event-driven jobs; Google Cloud Storage for media; Sentry for error tracking/tracing.
- **`tripknot-admin`** — Next.js 16 / React 19 internal ops console: destination/place/state content management, CSV import/export, trip moderation, KYC/identity review, analytics dashboards (React Query, Zustand, shadcn/Radix UI, Recharts).
- **`tripknot-app`** — Expo 54 / React Native 0.81 consumer mobile app (~27,000 lines): Expo Router, NativeWind, Zustand + TanStack Query, Firebase auth (Google/Apple sign-in), maps with clustering, push notifications, Sentry.
- **Purpose-specific microservice and supporting tools**: one standalone background scoring microservice (`tripknot-scorer` — trending/popularity ranking with time-decay math, percentile normalization, dependency-ordered score cascades across places→destinations→states); plus supporting ETL, image-quality, and itinerary-prototyping tools rather than additional production microservices.
- **Deployment/infra**: Docker, Google Cloud Run (`asia-south1`), GitHub Actions CI (tests + Docker build) and CD (staging → manual-promote-to-production), GCP Workload Identity Federation for keyless CI auth, Sentry across both backend and mobile.

## Collaboration and Ownership Boundary
The backend totals—approximately 21,000 lines of application code, 185 endpoints, and 23 domain routers—represent the collective work of the three full-stack engineers. The complete product and five-month release were shared founding-team outcomes. The technical sections below describe the systems I worked on while preserving narrower ownership boundaries where another founding engineer led the implementation.

## Technical Work

### AI itinerary generation engine (backend)
The product's core differentiator. Multi-provider LLM routing: Gemini uses a Pydantic-derived JSON schema and response validation, while Groq/Llama-3 is the automatic fallback with the schema embedded in the prompt and downstream normalization. Token cost and latency are instrumented per generation. A hand-rolled place-scoring and diversity algorithm: log-scaled popularity blended with rating-count and landmark/trending/hidden-gem signals, per-request seed jitter (±12–18%) so repeated requests don't return identical results, an "anchor" mechanism guaranteeing top landmarks always appear, round-robin category-diversity fill, and budget-tier filtering with graceful relaxation when strict filters return too few results. Predecessor prototyping happened in a Streamlit proof-of-concept (geo-clustering + greedy TSP day-ordering + LLM-based scheduling) before the production rewrite.

### Trust & safety / identity verification (backend + admin)
I provided limited engineering support for the Aadhaar/KYC identity-verification workflow, which was led and built by another founding engineer. The broader system includes a "strangers trip" flow for participants joining people they do not already know, trip and user data models, backend validation, a traveler-facing submission flow, and an admin review interface for approval or rejection. My direct production authentication work included resolving a Google Cloud Storage upload issue by switching to Firebase service-account-key authentication after a Uniform Bucket-Level Access/`make_public` failure, along with profile-image upload handling and user-token verification endpoints.

### Admin backend + console (backend + tripknot-admin, full-stack)
CSV import/export for destinations and places, destination/place/state CRUD, an analytics dashboard with real visualizations, trip moderation including a two-step host-verification approval flow and a soft-cancel-with-audit-trail redesign (replacing hard deletes with status/reason/audit fields for compliance). Built full-stack — matching backend endpoints and admin frontend UI shipped together.

### Analytics & gamification (backend)
Fire-and-forget event tracking that does not await completion in the user-facing request path, atomic counters, a trending/popularity recalculation job, public leaderboard endpoints, badges.

### Background ranking/scoring service (standalone)
A dependency-ordered scoring pipeline (places → destinations → states) computing trending scores (time-decay, Reddit-style hot-ranking math, 48h half-life over a rolling window) and popularity scores (weighted blend of review quality, normalized importance, engagement, and recent momentum, with a seasonal boost for in-season entities). Every threshold is a tunable config value rather than a hardcoded constant, and the normalization approach (percentile-based, dynamic top-K% trending cutoff) is explicitly designed to behave sensibly from pre-launch traffic through much larger scale.

### Mobile app features (tripknot-app)
A location/personalization pipeline (home feed and discover results respond to the user's real location, with a fix distinguishing GPS-sourced vs. manually-picked city so background sync stops overwriting a manual choice), a full "Explore India" states feature (region-filterable browsing, state detail pages with hero content and best-time-to-visit info), a notification-preferences screen (master + per-category toggles), search/category filtering, and a native file-upload fix (routing Android/iOS photo picker uploads through Expo's native upload API instead of a form-data approach that failed on certain URI types).

### Data platform / R&D
An image-quality vetting pipeline for destination photos — iterated from a heavier OCR+frequency-analysis watermark detector to a fine-tuned vision classifier after tuning against real false positives on food photography; a companion asset-migration tool converting and re-hosting images to WebP on GCS with structured audit logging. An ETL tool for ingesting destination data from spreadsheets/CSVs into the production data model (slug generation, geocoding, tag/image parsing), pushing through the authenticated backend API with dry-run and duplicate-detection support rather than writing to the database directly.

### DevOps / cloud infrastructure
GitHub Actions CI (test + Docker build) and CD (automatic staging deploy, manual-gated production promotion) for the backend, Google Cloud Run deployment in `asia-south1`, GCP Workload Identity Federation so CI never holds a long-lived cloud credential, and Sentry error/performance monitoring wired into both the backend and the mobile app.

## Scale signals (whole product, for context — not for a single bullet)
- Backend (collective work of three contributors): ~21,000 LOC, 185 endpoints, 23 domain modules, real production deploy pipeline (Cloud Run + CI/CD + Sentry).
- Mobile app: ~27,000 LOC, Expo/React Native, EAS Build CI for Android + iOS store submission.
- Admin console: ~17,000 LOC, Next.js 16 / React 19.
- One purpose-specific scoring microservice, plus ETL and image-processing supporting tools, beyond the three main repositories.
- Development has been continuous since March 2026.

## Key Highlights
- Helped take TripKnot from its founding idea and raw destination data to a complete production ecosystem within five months, spanning the backend, traveler mobile app, business portal, admin console, and public website.
- Developed the AI itinerary engine through multi-provider LLM routing with Gemini and Groq fallback plus custom place-scoring and diversity logic for budget-aware itineraries.
- Built the admin console and backend endpoints for content moderation and analytics, including a two-step host-verification flow and an audit-logged cancellation system.
- Designed a standalone scoring service computing trending/popularity rankings via time-decay, multi-factor models, tuned to stay stable from launch through scale.
- Shipped mobile features spanning location-aware personalization, a region-browsable "Explore India" feature, and notification preferences, in React Native/Expo.
- Set up CI/CD and cloud deployment for the backend (GitHub Actions, Docker, Cloud Run, Workload Identity Federation), with Sentry monitoring across backend and mobile.
- Built an image-quality vetting pipeline and ETL tooling to ingest and maintain destination content at scale.
