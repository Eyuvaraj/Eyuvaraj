# My Professional Experience

## Aneeras LLP

### Founding AI Engineer

- **Period:** March 2026 – Present
- **Location:** Pondicherry, India · Hybrid
- **Product:** [TripKnot](https://tripknot.in/)

#### Company & Product Overview

[Aneeras LLP](https://aneeras.com/) is a product-first technology startup founded in 2026 around TripKnot as its core idea and first product. Aneeras focuses on building practical digital products around real-world experiences, with TripKnot establishing the company's initial direction in travel technology.

[TripKnot](https://tripknot.in/) is an AI-assisted travel platform that brings personalized day-by-day itinerary planning, destination and hidden-gem discovery, curated escapes, map-based exploration, and group travel into one connected experience. Its broader product ecosystem includes the traveler mobile application, a partner-facing business portal, an internal admin console, the public website, backend services, and the underlying destination-data platform.

#### Founding Team & Delivery Context

I am one of five founding team members and one of three full-stack engineers. The founding team consists of three full-stack engineers, one UI/UX developer, and one frontend developer. We formed Aneeras around the TripKnot idea, coordinated product and engineering decisions closely, and built the product from the ground up rather than inheriting an existing platform.

Within five months of beginning the build, we took TripKnot from the initial idea and raw destination data to a public production release. The team delivered the data foundation, backend, traveler mobile application, business portal, admin console, public website, and the supporting deployment and operational systems required to run them.

#### Role & Product Context

As a Founding AI Engineer, I work closely with the other members of the founding team across product definition, architecture, implementation, release, and iteration. My own engineering work spans AI-assisted itinerary generation, ranking and personalization, backend and admin systems, React Native mobile features, data pipelines, cloud deployment, observability, engineering infrastructure, and limited support for identity-verification work. The product is a shared founding-team effort; the details below describe my own work and clearly identify areas where responsibility was shared.

#### AI Itinerary Generation Engine

- **Multi-Provider AI Itinerary Engine:** Within the founding team, I helped build TripKnot's core multi-provider LLM itinerary engine. I configured Gemini as the primary provider with a Pydantic-derived JSON schema and strict response validation. I configured Groq/Llama-3 as the automatic fallback, passing the schema directly in its prompt before downstream normalization, and instrumented token cost and latency for every generation.
- **Place-Scoring & Diversity Algorithm:** I designed a place-scoring and diversity algorithm that blends log-scaled popularity with rating counts and landmark, trending, and hidden-gem signals. I added per-request seed jitter to prevent repeated requests from producing identical itineraries, an anchor mechanism that guarantees top landmarks appear, round-robin category-diversity filling, and budget-tier filtering with graceful relaxation when strict filters return too few results.
- **Proof of Concept:** I built the Streamlit proof of concept that preceded and informed the production rewrite, including geo-clustering, greedy traveling-salesperson-problem (TSP) day ordering, and LLM-based scheduling.

#### Trust, Safety & Identity Verification

- **KYC/Aadhaar Implementation Support:** I provided limited engineering support for TripKnot's Aadhaar/KYC identity-verification workflow. The system was led and built by another founding engineer and covered strangers trips in which participants may join people they do not already know, along with the related trip and user data models, backend validation, traveler-facing flow, and admin review interface.
- **Storage Authentication & Token Handling:** I resolved a production Google Cloud Storage upload-authentication problem by switching to Firebase service-account-key authentication after Uniform Bucket-Level Access caused the earlier `make_public` approach to fail. I also built profile-image upload handling and user-token verification endpoints.

#### Admin Backend & Console

- **Full-Stack Admin Platform:** I built the backend and admin console end to end for destination, place, and state CRUD operations; CSV import and export; and an analytics dashboard with real-time data visualizations.
- **Trip Moderation & Compliance:** I implemented trip moderation with a two-step host-verification approval flow. I also redesigned trip cancellation from hard deletion to a soft-cancel model with status, reason, and audit fields, preserving a compliance-oriented audit trail.

#### Analytics & Gamification

- **Non-Blocking Event Tracking:** I implemented fire-and-forget event tracking so analytics work runs asynchronously and is not awaited in the user-facing request path.
- **Counters, Rankings & Gamification:** I built atomic counters, a background trending-and-popularity recalculation job, public leaderboard endpoints, and user badge systems.

#### Background Ranking & Scoring Service

- **Standalone Scoring Pipeline:** I designed a standalone, dependency-ordered scoring pipeline that calculates scores in the sequence places → destinations → states. The trending model uses time-decay and Reddit-style hot-ranking mathematics with a 48-hour half-life over a rolling window.
- **Multi-Factor Popularity Model:** I calculated popularity through a weighted combination of review quality, normalized importance, engagement, and recent momentum, with seasonal boosts for in-season entities. I implemented percentile-based normalization, a dynamic top-K-percent trending cutoff, and configurable thresholds rather than hardcoded values so the approach can behave sensibly from pre-launch traffic through much larger scale.

#### Mobile App Features

- **Location-Aware Personalization:** I shipped a location and personalization pipeline for the Expo/React Native application so the home feed and discovery results respond to the user's actual location. I also fixed the distinction between a GPS-sourced city and a manually selected city so background location synchronization does not overwrite the user's explicit choice.
- **Explore India & Discovery:** I built the Explore India states experience, including region-filterable browsing, state detail pages, hero content, and best-time-to-visit information. I also implemented notification preferences, search, and category filtering.
- **Native Media Uploads:** I fixed Android and iOS photo-picker uploads by routing files through Expo's native upload API.

#### Data Platform & R&D

- **Image-Quality Vetting:** I worked jointly on an image-quality vetting pipeline for destination photographs. The approach evolved from a heavier OCR-plus-frequency-analysis watermark detector to a fine-tuned vision classifier after tuning against real false positives, including food photography.
- **Asset Migration:** I developed a companion asset-migration tool that converts images to WebP, re-hosts them on Google Cloud Storage, and produces structured audit logs.
- **Destination Ingestion ETL:** I built an ETL tool that ingests destination data from spreadsheets and CSV files into the production data model, including slug generation, geocoding, and tag and image parsing. It pushes data through the authenticated backend API, rather than writing directly to the database, and supports dry runs and duplicate detection.

#### DevOps & Cloud Infrastructure

- **CI/CD:** I configured GitHub Actions continuous integration for testing and Docker builds, automatic staging deployment, and manually gated production promotion.
- **Cloud Deployment:** I deployed the backend to Google Cloud Run in `asia-south1`.
- **Workload Identity:** I configured GCP Workload Identity Federation so the CI environment does not hold a long-lived cloud credential.
- **Observability:** I integrated Sentry error and performance monitoring into both the backend and mobile applications.

#### Technology Stack

- **Languages & Frameworks:** Python, Node.js, React Native, Expo, Streamlit, Pydantic, FastAPI
- **AI & LLMs:** Gemini, Groq, LLaMA-3, vision classifiers, Pydantic schema validation
- **Databases & Cloud:** PostgreSQL, Supabase, Google Cloud Run, Google Cloud Storage, Firebase, Docker
- **DevOps & Infrastructure:** GitHub Actions, GCP Workload Identity Federation, Sentry

#### Key Highlights

- Helped take TripKnot from its founding idea and raw destination data to a complete production ecosystem within five months, including the backend, traveler mobile app, business portal, admin console, and public website.
- Developed TripKnot's multi-provider itinerary workflow with Gemini schema validation, Groq/Llama fallback handling, and per-generation token-cost and latency tracking.
- Designed place-scoring and diversity logic using popularity, ratings, landmark and hidden-gem signals, seed jitter, category balancing, landmark anchors, and budget-aware filtering.
- Designed the standalone ranking service that calculates configurable, time-decayed trending and multi-factor popularity scores across places, destinations, and states.
- Built the full-stack admin platform for destination data, CSV operations, analytics, host verification, and audit-logged trip moderation.
- Implemented asynchronous analytics, atomic counters, popularity recalculation, public leaderboards, and user badges without blocking user-facing requests.
- Shipped location-aware discovery, manual-city preservation, Explore India, notification preferences, search, filtering, and native media uploads in React Native and Expo.
- Built authenticated destination-ingestion and asset-migration tooling with geocoding, duplicate detection, dry runs, WebP conversion, Google Cloud Storage, and audit logs.
- Established Docker-based CI/CD on Google Cloud Run with automatic staging, gated production promotion, keyless Workload Identity Federation, and Sentry monitoring.

---

## [YUVABE](https://yuvabe.com/)

### Organization Context

YUVABE is an Auroville-based organization operating under the Auroville Foundation. It follows a Work, Serve, Evolve model and combines higher-order skilling with multidisciplinary project delivery. [Yuvabe Studios](https://www.yuvabestudios.com/) brings together AI, engineering, design, product, and marketing capabilities for client engagements. I progressed from a six-month AI Engineer internship into a full-time AI Engineer role without a gap between the two positions.

### Client Context: [TVAM](https://www.tvam.co/)

TVAM was already an established Bengaluru-based health-and-fintech company before it became a YUVABE client. Its health-and-wealth platform brought together health insurance, doctor consultations and telemedicine, AI-assisted health experiences, UPI and bill payments, loans, investments, banking-related services, and personal-finance features. TVAM's public materials describe operations across 22 Indian states and a community or platform population of more than 200,000 people; the platform population during my work was documented as more than 100,000 users. [Yuvabe Studios' TVAM case study](https://www.yuvabestudios.com/case-studies/tvam) dates the engagement to 2024 and documents RAG, vector search, cloud-native AI, and product work for the iOS and Android platform.

I was involved from the beginning of TVAM's client engagement with YUVABE and worked predominantly on this client across both my internship and full-time role. Unlike a greenfield product built entirely at YUVABE, TVAM already had a substantial company, product, services, users, and partner ecosystem. My scope was TVAM's AI-related R&D and engineering: I researched approaches, built and evaluated prototypes, developed AI and backend services, and deployed selected systems for the client. Other YUVABE teams worked on areas such as brand, UI/UX, and broader product delivery. The specific work recorded below, including the SMS/NLP systems, edge RAG research, Minions evaluation, avatar pipelines, and associated AI experiments, was performed for TVAM as part of this client engagement.

### AI Engineer

- **Period:** July 2024 – August 2025
- **Location:** Auroville, Tamil Nadu, India
- **Primary Client:** TVAM

#### Role Overview

As a full-time AI Engineer, my primary operational focus was TVAM's AI/ML architecture and R&D. I architected, built, evaluated, and deployed generative-AI platforms, multi-agent microservice networks, NLP systems, edge language-model pipelines, on-device document intelligence, conversational 3D avatars, and supporting backend infrastructure for the client. My work covered the development lifecycle from low-level C++ and Python R&D and model fine-tuning to FastAPI microservices, Azure and GCP deployment, and native Android integration. I also mentored incoming YUVABE AI interns.

#### 1. Multi-Agent Production AI Platform & Agentic Architecture

##### Production Multi-Agent Platform Architecture

- **System Design:** I architected and deployed a multi-agent AI system for TVAM's platform, which served more than 100,000 users across healthcare, health insurance, wealth management, and personal financial management during this work.
- **Dynamic Agent Routing:** I designed a routing layer using OpenAI function calling and domain-specific intermediary router agents. It analyzes each incoming query, dialogue state, and intent before directing the message to a specialized sub-agent:
  - **Health Advisor:** Handles medical symptoms, triage guidance, lifestyle wellness, and preliminary advice.
  - **Policy Advisor:** Analyzes health-insurance terms, coverage limits, riders, and claim rules.
  - **Doctor Router:** Evaluates medical necessity and triggers specialist-consultation popups.
  - **File Processor:** Processes uploaded medical reports, lab tests, and policy PDFs.
- **Context Continuity & State Synchronization:** I solved context loss during agent handoffs by designing shared session-state wrappers in FastAPI. The wrappers maintain conversational context, user-profile parameters, and file metadata across exchanges between sub-agents.
- **Multimodal Voice & Text:** I unified text and voice interaction by integrating speech-to-text (STT) and text-to-speech (TTS) models through backend endpoints, enabling accessible voice-driven advisory interactions.
- **Reliability:** I used grounded retrieval, agent specialization, tool calling, context management, output handling, and documented model-failure analysis to make domain-aware responses more dependable and reduce hallucination risk.

##### Cloud-Native Microservices & Infrastructure

- **MACH Architecture:** I built modular, cloud-native microservices following MACH principles: Microservices, API-first, Cloud-native, and Headless. I standardized interfaces across inference services, vector databases, document-processing nodes, and client-facing SDKs so individual workloads could scale independently and new models or services could be introduced without disrupting the rest of the platform.
- **API Development & Containerization:** I built high-throughput backend services with Python and FastAPI and containerized the microservices with Docker to create reproducible staging and production environments.
- **Cloud Deployment:** I deployed containerized services to Azure and Google Cloud Platform, including Cloud Run, and configured horizontal autoscaling, health-check probes, and zero-downtime model deployments.
- **Database & Session Storage:** I designed Supabase/PostgreSQL relational schemas for multi-turn conversation logs, agent-routing decisions, user preferences, and chat history. I used Google Cloud Storage (GCS) for secure document and generated-artifact retention.
- **Reusable AI APIs:** I built secure REST APIs for document upload, processing, summarization, question answering, and metadata extraction so multiple web and mobile applications could integrate AI capabilities through standardized services without tight coupling.

#### 2. Enterprise NLP, SMS Intelligence & Transaction Analytics

##### Four-Tier SMS Processing Hierarchy

I designed and built an end-to-end SMS intelligence pipeline for TVAM's AI-Powered Decision Board. Across experimentation and product work, the pipeline processed datasets ranging from more than 15,000 to more than 100,000 unstructured SMS messages and converted noisy transactional text into structured, queryable financial data through four tiers:

1. **Preprocessing & Binary Classification:** I cleaned raw SMS logs by filtering exact duplicates, non-English messages, promotional spam, and embedded URLs, then classified messages as Transaction or Offer.
2. **LLM Quality-Filtering Agent:** I implemented an LLM-based agent that scores usefulness from 1 to 5. It drops ratings 1 and 2, representing promotional noise and junk notifications, while retaining ratings 3, 4, and 5 for downstream financial analysis.
3. **Primary Category Classification:** I categorized retained financial messages into Credit, Debit, Info, and Balance.
4. **Granular Subcategory Labeling:** I prompted LLMs to produce 8–10 granular labels below each primary category, such as salary credit, UPI debit, utility payment, mutual-fund investment, and account-balance update. I enforced mandatory label assignment to create a complete staged label tree for business-use-case exploration.

##### Transformer Fine-Tuning & Model Benchmarking

- **BERT:** I researched encoder-only transformer architectures and fine-tuned custom BERT models for multiclass classification over noisy financial data containing abbreviations and informal syntax.
- **SetFit:** I fine-tuned SetFit sentence-transformer models for high-speed SMS classification, rating prediction, and Category 1 prediction, and deployed the resulting endpoints to Hugging Face Spaces for real-time inference.
- **LLaMA 3.1 70B & Clustering:** I used LLaMA 3.1 70B for zero-shot discovery of new categories in financial logs and ran K-Means clustering over sentence embeddings to identify unlabeled transaction patterns.
- **Benchmarking Matrix:** I measured classification accuracy, throughput, and latency across Phi-3, LLaMA 3-8B, LLaMA 3-70B in 4-bit and 6-bit quantization, GPT-4, and GPT-3.5 on two NVIDIA T4 GPUs with 16 GB VRAM each and one NVIDIA A100 GPU with 80 GB VRAM.

##### Entity Extraction & Decision Board

- **Financial Entity Extraction:** I developed system prompts that extract transaction amounts, dates, account numbers, and sender entities from unstructured messages and write those attributes into structured production-database columns.
- **RAG-Based Entity Standardization:** I implemented retrieval-augmented normalization for inconsistent bank sender codes such as `JX-UNIONB`, `AX-NSESMS`, and `JK-UNIONB`, mapping them to standardized financial-institution entities.
- **AI-Powered Decision Board:** I designed and prototyped a unified dashboard that aggregates processed SMS insights, categorizes spending behavior, tracks balance trends, and visualizes financial-health metrics for product managers and users.

#### 3. Open-Source LLM Evaluation & Specialist Doctor Routing

##### Specialist Doctor Routing

- **Business Workflow:** After a user interacts with TVAM's AI assistant, Tvamev, the system evaluates whether specialist medical intervention may be needed. When appropriate, it selects a medical specialty and triggers an in-app consultation popup through function calling.
- **Baseline Implementation:** I worked with the baseline OpenAI function-calling workflow, which uses conversation history to select the appropriate specialist and raise the popup flag.

##### Open-Source Replacement Experiments & Failure Analysis

I evaluated open-source replacements to reduce reliance on proprietary APIs and documented their behavior under the more complex doctor-routing workflow.

- **Broader Model Evaluation:** I evaluated LLaMA 3.1, Qwen, and other open-source models as possible alternatives to proprietary APIs for classification, generation, and function calling under multi-agent routing conditions.

- **Alibaba QWQ:** QWQ handled simple single-tool tasks such as weather lookup but failed under complex medical routing. It invoked the tool in only 4 of 10 trials, frequently exposed internal function names and parameter descriptions, and generated hallucinated doctor advice.
- **Two-Stage Workaround:** I split the process into two stages: the tool invocation first raises the application flag, then the complete chat context goes to a second LLM that generates dynamic popup content.
- **LLaMA 3.3-70B through Groq:** The Groq-hosted model handled conversation and function calls effectively but repeatedly called the same tool more than once in a session.
- **LLaMA 3.3-70B on a Local VM:** The `q6_k` GGUF model sometimes called the doctor-routing function immediately at session start and frequently returned empty strings for complex conversational prompts.
- **Failure-Mode Record:** Across these tests, I documented premature tool invocation, repeated invocation, hallucinated tool outputs or advice, leaked internal tool metadata, and empty-string responses to guide model selection and workflow design.

#### 4. Edge AI, On-Device SLM Systems & Mobile Benchmarks

##### On-Device Inference Engine Survey

I conducted R&D on running small language models and embedding models directly on Android hardware without cloud connectivity. I tested models including Qwen2.5, Phi-3 Mini, and LLaMA 3.1 across ONNX Runtime and Llama.cpp environments, then evaluated six major mobile inference options:

1. **Llama.cpp:** I selected it as the primary engine for local GGUF model execution.
2. **ONNX Runtime:** I used it for local embedding generation and quantized SLM inference.
3. **MediaPipe/TensorFlow Lite:** I evaluated it for on-device visual and text processing.
4. **MLC LLM/Apache TVM:** I tested it for compiler-optimized mobile LLM execution.
5. **MLLM:** I evaluated it as a lightweight mobile inference framework.
6. **Picovoice:** I evaluated it for on-device voice processing.

##### Empirical Android Benchmarks

I ran the mobile benchmarks with Llama.cpp on a Xiaomi device using HyperOS and Android 14, a Snapdragon 4 Gen 2 octa-core CPU up to 2.2 GHz, 6 GB RAM, and 2 GB virtual swap.

| Model | Quantization | Size | Throughput | Practical Result |
|---|---:|---:|---:|---|
| `qwen2.5-0.5b-instruct` | `q4_0` | 0.429 GB | 19.69 tokens/s | Fastest; practical for real-time mobile conversation |
| `qwen2.5-0.5b-instruct` | `q6_k` | 0.650 GB | 14.34 tokens/s | Strong accuracy-speed tradeoff on a mobile CPU |
| `qwen2.5-0.5b-instruct` | `q8_0` | 0.676 GB | 16.36 tokens/s | Stable throughput at higher precision |
| `qwen2.5-1.5b-instruct` | `q4_0` | 1.070 GB | 8.87 tokens/s | Viable for more complex instruction following |
| `qwen2.5-1.5b-instruct` | `q6_k` | 1.460 GB | 6.43 tokens/s | Moderate generation latency |
| `qwen2.5-1.5b-instruct` | `q8_0` | 1.890 GB | 6.47 tokens/s | Higher memory footprint on CPU |
| `qwen2.5-3.0b-instruct` | `q4_0` | 2.000 GB | 4.55 tokens/s | Acceptable for non-real-time background work |
| `qwen2.5-3.0b-instruct` | `q6_k` | 2.790 GB | 2.24 tokens/s | Slow generation |
| `qwen2.5-3.0b-instruct` | `q8_0` | 3.620 GB | 0.20 tokens/s | Unusable because memory pressure caused severe system lag |
| `phi3-mini` (3.8B) | `q4_0` | 2.390 GB | 2.90 tokens/s | High memory use and slow response |
| `phi3-mini` (3.8B) | `q8_0` | 3.780 GB | 0.00 tokens/s | The application froze and the operating system crashed |

##### Memory & Runtime Findings

- **4 GB RAM Limitation:** I documented that Android devices with 4 GB RAM or less could not run even the 0.429 GB `qwen2.5-0.5b-instruct_q4_0` model reliably because of operating-system background-memory pressure and process-killer limits.
- **ONNX Runtime vs. Llama.cpp:** On an Intel Core i5 11th-generation computer with 16 GB RAM running the 2.53 GB `phi3-mini-q4` model, ONNX Runtime produced 9.54 tokens per second and Llama.cpp produced 8.65 tokens per second.
- **Android ONNX Validation:** I converted small language models to ONNX, validated them on Android devices with 8 GB RAM, and documented approximately one-token-per-second degradation on 4 GB devices.
- **Small-Model Reliability Analysis:** I investigated limited context windows, hallucination patterns, and retrieval errors under mobile constraints. I proposed better chunk preprocessing, metadata-aware filtering, and retrieval-strategy changes to improve answer reliability.

#### 5. Edge RAG: Fully Offline Document Q&A on Android

##### Architecture & Technical Stack

I designed and implemented a fully offline retrieval-augmented generation system that performs document parsing, embedding generation, vector retrieval, and language-model inference on an Android device without a cloud dependency.

- **Document Parsing:** I integrated `iTextPDF` for PDF parsing and Apache POI for DOCX parsing directly into Java/Android projects.
- **Semantic Chunking:** I split text into 1,200-character chunks with 400-character overlap.
- **Local Embeddings:** I ran `all-MiniLM-L6-v2` locally through ONNX Runtime, producing 384-dimensional vectors.
- **On-Device Vector Search:** I integrated ObjectBox Vector Database with a Hierarchical Navigable Small World index for local similarity retrieval.
- **Local Generation:** I ran Llama.cpp through Termux on Android and served LLaMA 3.2-1B `Q8_0` and LLaMA 3.2-3B `Q4_0` GGUF models from a localhost API consumed by the Android application.

##### Financial SMS Benchmark

I evaluated the Edge RAG system on 201 real financial SMS messages containing bank balances, fund statements, and transaction notifications.

- **Retrieval Competition:** Top-K retrieval at 12, 20, and 40 chunks often returned competing financial transactions and confused the on-device model.
- **Arithmetic Failures:** The LLaMA 3.2-1B and 3.3-3B models struggled with operations such as summing debits and calculating net balances across multiple messages.
- **Currency Hallucination:** Models frequently returned dollars or euros even when the context used Indian rupees (`₹` or `Rs.`).
- **Latency:** Longer retrieved contexts materially reduced generation speed on the mobile CPU.

##### Proposed Improvements

1. **Metadata Filtering:** I proposed applying date, sender, and transaction-type filters in SQL or ObjectBox before vector similarity search.
2. **Streaming Generation:** I proposed streaming tokens to the interface to reduce the perceived wait during initial context processing.
3. **Current-Date Injection:** I proposed injecting the device's current date and time into system prompts to ground temporal queries.
4. **Native C++ JNI Integration:** I proposed replacing the Termux local server with direct C++ JNI bindings for Llama.cpp inside the Android application.

#### 6. Distributed Edge-and-Cloud Collaboration: Minions Evaluation

##### Architecture Review

I reviewed the research paper *Minions: Cost-efficient Collaboration Between On-device and Cloud Language Models*. The approach uses a large cloud model to decompose a request into subtasks, local small language models from roughly 1B to 8B parameters to process those subtasks in parallel, and the cloud model again to synthesize the local outputs.

##### Empirical Benchmark

I tested the Minions framework on a sample medical question-answering context and measured cost, token consumption, latency, and output quality across three execution modes.

| Execution Mode | Model Configuration | Prompt Tokens | Completion Tokens | Total Time | Output Quality |
|---|---|---:|---:|---:|---|
| Remote only | `gpt-4o-mini` | 866 | 349 | 4.9 seconds | Accurate |
| Edge only | `qwen2.5-0.5b-instruct_q8_0` | 957 | 335 | 27.3 seconds | Mostly right |
| Minions hybrid | Local: `qwen2.5-0.5b`; remote: `gpt-4o-mini` | Local: 2,082; remote: 4,581 | Local: 334; remote: 573 | 3 minutes 28.4 seconds | Accurate |

- **Cost and Quality:** The hybrid approach reduced cloud API cost by 5.7× while retaining 97.9% of the remote model's accuracy.
- **Practical Viability:** I documented that the architecture was effective for server-side or desktop edge deployments but was not practical on mobile phones in this setup because of memory use, thermal throttling, and end-to-end execution exceeding three minutes.

#### 7. Conversational 3D Avatars, Speech & Mobile SDK Pipeline (`ReadyplayerOculusUnity`)

##### Avatar Ecosystem Evaluation

I evaluated 3D avatar creation, runtime loading, and facial-animation technologies including VRoid, Avaturn, Reallusion Character Creator 4 and iClone, UniVRM, uLipSync, Meta Avatar SDK, and Meta XR Plugin.

- **Meta Ecosystem Limitation:** I documented that Meta Avatars were restricted to Meta's ecosystem, including Instagram stickers, WhatsApp, and Meta Quest/Horizon OS, without public export formats or an external runtime-animation SDK suitable for this work.
- **Ready Player Me Selection:** I selected Ready Player Me for full-body avatar creation, cross-platform runtime loading, and customizable GLB assets.

##### Photo-to-Avatar REST API

- **API Development:** I analyzed the Ready Player Me SDK's C# source and reverse-engineered its REST calls. I then wrote a Python service that converts one uploaded photograph into a fully rigged Ready Player Me avatar and returns its `.glb` URL.
- **Deployment:** I deployed the service publicly on Hugging Face Spaces at `eyuvaraj-avatarcreator.hf.space`, allowing photo-based avatar generation without a separate frontend or Unity Editor workflow.

##### Moving the Complete Pipeline to Android Runtime

The default Ready Player Me workflow required avatars to be configured in the Unity Editor before compiling the APK. I moved the complete setup into the Android runtime:

1. **Dynamic Loading:** I allowed users to enter an image URL or upload a photograph in the application, then downloaded the resulting `.glb` model dynamically on Android.
2. **Persistence & Caching:** I saved the downloaded `.glb` file in local Android storage so later launches could load it from disk and run text-to-speech, animation, and lip synchronization offline after the initial download.
3. **SDK Modification:** I modified the Ready Player Me Unity SDK's C# source to bind Oculus Lip Sync and map mesh targets dynamically at runtime on Android.
4. **Visual Quality:** I increased `baseColor` and normal-map texture resolution from 1024 px to 2048 px and added Ready Player Me's looping `Standing_idle` body animation to maintain a natural posture.

##### TTS Evaluation & Technical Constraints

- **OpenAI TTS:** It produced high-quality audio but required internet access and incurred a per-turn API cost.
- **Android Native TTS:** I tested it as a free offline option. `TextToSpeech.synthesizeToFile()` failed silently, without error logs, when input exceeded roughly 150–400 characters depending on the device. `TextToSpeech.speak()` could stream to the speakers but did not expose raw PCM buffers to Unity's `AudioSource`, so Oculus Lip Sync could not use the audio to drive facial blendshapes.
- **Azure TTS:** I selected Azure TTS for the production path because it provided real-time playback together with exact viseme IDs and timestamps for precise lip synchronization.

##### Dual-Avatar Dialogue & Dynamic Camera

- **JSON Dialogue Engine:** I built a turn-based engine that reads structured JSON scripts containing two-character conversations.
- **Audio & Viseme Synchronization:** I generated audio line by line, passed PCM audio to Unity's `AudioSource`, and activated the matching Oculus Lip Sync viseme blendshapes on the speaking avatar.
- **Listening Behavior:** I programmed the non-speaking avatar to use randomized idle gestures, subtle head nods, and listening poses while the other avatar spoke.
- **Camera Control:** I implemented automated camera movement that focuses on the active speaker and returns to a wide two-avatar view during pauses.

##### Reusable Android Library

I exported the Unity project, including the avatars, Oculus Lip Sync, Azure TTS, and dynamic camera system, as an Android `.aar` library. I built Java, Kotlin, and Flutter wrappers so native mobile applications could embed the conversational-avatar experience.

#### 8. 2D & Web 3D Avatar Lip-Sync Experiments

##### 2D Avatar R&D

I ran five approaches to create talking avatars from static two-dimensional photographs without cloud-rendering fees:

1. **Azure TTS Viseme-Clip Concatenation:** I extracted individual audio and video clips from Azure TTS viseme IDs and joined them locally, then documented motion artifacts and abrupt jaw transitions.
2. **Cartoonized Viseme Frames:** I cartoonized portrait photographs, removed their original mouth regions, and overlaid 21 cartoon viseme frames for smoother transitions, documenting facial-hair difficulties on male avatars.
3. **Manual Warp Editing:** I manually produced 21 viseme frames by warping the jaw, teeth, and tongue positions to improve realism.
4. **HeyGen & MediaPipe Masking:** I generated a base avatar video in HeyGen, masked its mouth using MediaPipe landmarks, and overlaid viseme mouth images dynamically at runtime.
5. **Rule-Based Number Video:** I pre-rendered 32 number clips covering 0–19, 100, and 1000, plus an introduction clip, then concatenated them dynamically to speak any number up to 99 million.

##### Web-Based 3D Viseme Lip Sync

- **Avatar Pipeline:** I created a 3D avatar with facial blendshapes using Avaturn.
- **Local Phonetic Visemes:** I integrated `TalkingHead.js`, based on 1976 letter-to-sound rules, to calculate English visemes locally, including support for romanized Indic text.
- **Three.js Rendering:** I combined Google and Azure TTS SSML word-timestamp metadata with Three.js to animate facial blendshapes in the browser. I hosted live demonstrations at `eyuvaraj.github.io/VisemeAvatar_GoogleTTS/` and `eyuvaraj.github.io/VisemeAvatar_Azure/`.

##### Third-Party Service Evaluation

- **Vidnoz:** I tested template avatars in eight Indian languages: Hindi, Tamil, Telugu, Kannada, Marathi, Gujarati, Bengali, and Urdu.
- **NVIDIA Audio2Face 2D:** I benchmarked the preview lip-sync model and documented inaccurate lip alignment on its default audio.
- **HeyGen:** I evaluated photo-to-video generation, Hindi and Tamil video translation with voice cloning, and LiveKit streaming integrations.
- **Speech & Lip-Sync Systems:** I evaluated ElevenLabs, LMNT, Play.ht, Cartesia, ChatterBox TTS with local PCM streaming, fish.audio, Wav2Lip, and MuseTalk.

#### 9. Infrastructure Modernization, Text-to-Video R&D & Mentoring

##### ASP.NET Microservice Migration

- **Migration:** I led the migration of legacy LoadDashboard REST microservices from Node.js to ASP.NET with C#.
- **Execution:** I learned C# and the .NET framework independently within two weeks and converted eight production REST endpoints while preserving their schemas, database performance, service uptime, compatibility, and reliability.

##### Open-Source Text-to-Video Survey

I surveyed open-source text-to-video models on Hugging Face for possible enterprise use:

- **Tencent HunyuanVideo:** 13B parameters, approximately 40 GB, requiring roughly 45–60 GB VRAM
- **Genmo Mochi-1:** Approximately 42 GB
- **THUDM CogVideoX-5b:** Approximately 12 GB
- **ByteDance AnimateDiff-Lightning:** Approximately 10 GB
- **Lumina-Video:** Approximately 8 GB
- **ModelScopeT2V:** Approximately 8 GB
- **Evaluation Framework:** I evaluated text-video alignment, visual quality, motion smoothness, temporal consistency between frames, and facial preservation.

##### Technical Enablement & Intern Mentoring

- **Technical Evaluation:** I prepared two complete Python programming question papers and technical problem sets for incoming YUVABE AI interns.
- **Onboarding & Mentoring:** I conducted technical onboarding, code reviews, and weekly mentoring sessions covering Python, FastAPI, Docker, and machine-learning fundamentals.

#### 10. Additional TVAM AI Pipelines

- **Automated Knowledge Generation:** I built modular LLM pipelines that turn structured questionnaires into outputs such as brand guidelines, identity documents, and marketing-campaign drafts. I designed orchestration flows that transform raw answers into reusable knowledge artifacts and repeatable content-generation pipelines.
- **Multimodal Brand Intelligence:** I designed predictive ML pipelines for social-media text, image, and video data. I used NLP, computer vision, and clustering to derive sentiment trends, brand-perception signals, campaign indicators, and other insights for marketing and product teams.

#### Full-Time Technology Matrix

- **Programming Languages:** Python 3.x, C#/.NET and Unity, Java, Kotlin, C++ for Llama.cpp/JNI, SQL, JavaScript ES6+ and Three.js
- **Large Language Models & APIs:** OpenAI API with GPT-4, GPT-3.5, Assistant API, function calling, and embeddings; LLaMA 3, 3.1, 3.2, and 3.3 in 8B and 70B variants; Qwen2.5 0.5B, 1.5B, 3B, and 72B; Phi-3 Mini and Medium; Alibaba QWQ
- **ML & Fine-Tuning:** SetFit, BERT, Unsloth/QLoRA, Scikit-Learn, K-Means, PyTorch, Transformers, Hugging Face Transformers
- **Prompting & Agent Systems:** Chain-of-Thought, ReAct, dynamic few-shot prompting, multi-agent routing, system-prompt optimization
- **On-Device AI:** Llama.cpp/GGUF, ONNX Runtime, MediaPipe/TFLite, MLC LLM/Apache TVM, MLLM, Picovoice, Edge RAG, ObjectBox/HNSW, Termux, `all-MiniLM-L6-v2`
- **3D Engines & SDKs:** Unity 2021.3.45f1 LTS, Ready Player Me SDK, Oculus Lip Sync, Three.js, TalkingHead.js, UniVRM, URP Shader, uLipSync
- **3D & Avatar Tools:** Avaturn, VRoid, Reallusion Character Creator 4 and iClone, Meta XR SDK, Meta Avatar SDK, Ready Player Me Studio, Blender
- **Lip Sync & Visemes:** Oculus Lip Sync, Azure TTS visemes, MediaPipe mouth masking, NVIDIA Audio2Face 2D, Wav2Lip, MuseTalk, HeyGen
- **Backend & APIs:** FastAPI, ASP.NET Core/C#, Node.js, REST API design
- **Databases & Storage:** Pinecone, Supabase/PostgreSQL, ObjectBox, SQLite3, Google Cloud Storage
- **Cloud & DevOps:** Docker, Azure, Google Cloud Platform and Cloud Run, Hugging Face Spaces, GitHub Actions
- **Speech & Audio:** Azure TTS, OpenAI TTS, Android native TTS, Google TTS, ElevenLabs, LMNT, Play.ht, Cartesia, ChatterBox TTS, fish.audio

#### Key Highlights

- Architected TVAM's multi-agent AI platform for a product serving more than 100,000 users, routing health, insurance, doctor-consultation, and document requests to specialized agents while preserving context across handoffs.
- Built modular FastAPI microservices with Docker, Supabase/PostgreSQL, Pinecone, and Google Cloud Storage, deploying scalable AI workloads across Azure and Google Cloud Platform.
- Designed a four-tier SMS intelligence pipeline that processed datasets ranging from more than 15,000 to more than 100,000 messages for classification, quality filtering, category discovery, and financial-entity extraction.
- Evaluated and fine-tuned BERT, SetFit, Phi-3, LLaMA, Qwen, and other models across classification, generation, routing, quantization, and function-calling workloads.
- Built a fully offline Android RAG system using ONNX embeddings, ObjectBox HNSW retrieval, and Llama.cpp generation, with direct PDF and DOCX parsing on the device.
- Benchmarked quantized mobile models and achieved 19.69 tokens per second with a 0.429 GB Qwen2.5 0.5B `q4_0` model on a 6 GB Android device.
- Evaluated the Minions edge-and-cloud architecture, measuring a 5.7× cloud-cost reduction with 97.9% of remote-model accuracy while documenting why the tested setup was impractical on mobile.
- Engineered a runtime Android avatar pipeline with photo-to-avatar generation, Azure TTS visemes, Oculus lip synchronization, offline caching, dynamic camera control, and reusable Java, Kotlin, and Flutter wrappers.
- Led the migration of eight production LoadDashboard REST endpoints from Node.js to ASP.NET with C#, preserving schemas, database performance, compatibility, and service uptime.
- Prepared Python technical assessments and mentored incoming AI interns through onboarding, code reviews, and weekly sessions on Python, FastAPI, Docker, and machine-learning fundamentals.

---

### AI Engineer Intern

- **Period:** January 2024 – June 2024
- **Location:** Auroville, Tamil Nadu, India
- **Primary Client:** TVAM

#### Internship Overview

During my six-month AI Engineering internship at YUVABE, I designed, built, benchmarked, and deployed generative-AI pipelines, retrieval-augmented generation systems, multi-agent microservices, and NLP classification models for TVAM. Most of my internship centered on this client, whose platform served more than 100,000 users across 22 Indian states during the period. My major systems included a medical-reasoning engine over 7,000 USMLE questions, a health-insurance policy-advisor RAG system deployed to Azure, fine-tuned Phi-3 and SetFit models, and quantized-model benchmarks on T4 and A100 GPUs.

#### 1. TVAM Health Assistant & Document-Analysis Microservice

- **Period:** February 2024 – June 2024
- **Stack:** Python, OpenAI Chat API with GPT-3.5 and GPT-4, OpenAI Assistant API, FastAPI, Streamlit, Docker, Google Cloud Storage, GCP/Cloud Run

- **Conversational Health Advisor:** I developed TVAM's core Health Advisor chatbot with OpenAI chat models for real-time health questions.
- **Document Upload & Analysis:** I integrated the OpenAI Assistant API's file-handling capabilities into the backend so users could upload medical reports and other health documents for analysis, summarization, and direct question answering.
- **Cloud Storage & Persistence:** I used Google Cloud Storage buckets to persist chat-session history, uploaded files, and generated artifacts securely.
- **Microservice APIs:** I designed and built FastAPI REST microservices with structured request and response schemas for conversation and file-processing endpoints.
- **Prototype Interface:** I built a Streamlit frontend for internal testing, prompt evaluation, and demonstrations to client stakeholders.
- **Containerization & Deployment:** I learned and applied Docker, wrote optimized Dockerfiles for the FastAPI and Streamlit services, built their images, and deployed the production application to Google Cloud Run.
- **Prompt & Flow Refinement:** In June, I updated system prompts so the assistant could redirect users to TVAM's mobile application and support doctor-appointment booking flows.

#### 2. TVAM Policy Advisor & Health-Insurance RAG System

- **Period:** April 2024 – May 2024
- **Stack:** Python, OpenAI Chat API, OpenAI `text-embedding-3-small`, Pinecone, Supabase/PostgreSQL, FastAPI, Streamlit, Docker, Azure

- **Insurance Knowledge Base:** I gathered, structured, and preprocessed TVAM health-insurance documents covering policy terms, limits, coverage rules, exclusions, and claim-submission procedures.
- **Embedding & Indexing:** I split the policy material into chunks, converted them into 1,536-dimensional vectors with `text-embedding-3-small`, and indexed them in Pinecone.
- **Semantic Retrieval:** I built the retrieval pipeline that embeds a user's query, searches Pinecone with cosine similarity, returns the highest-matching policy chunks, and assembles grounded context for LLM response generation.
- **Personal Policy Analysis:** I integrated OpenAI Assistant API uploads so users could submit their own insurance documents for clause extraction, coverage comparison, and direct questions.
- **Full-Stack Service:** I built a FastAPI backend and Streamlit interface for policy discovery and document comparison.
- **Conversation Persistence:** I designed Supabase/PostgreSQL schemas to preserve multi-turn conversation history and vector-retrieval metadata across sessions.
- **Azure Deployment:** I packaged the backend, frontend, and database configuration in Docker and deployed the end-to-end RAG system to Azure.

#### 3. USMLE Medical Reasoning & Prompt Evaluation

- **Period:** March 2024 – April 2024
- **Stack:** Python, OpenAI API, Chain-of-Thought prompting, Pinecone, SQLite3, RAG

- **7,000-Question Reasoning Engine:** I built a clinical-reasoning system over 7,000 United States Medical Licensing Examination questions to evaluate and benchmark LLM diagnostic reasoning.
- **Chain-of-Thought Prompting:** I designed system prompts that required detailed step-by-step reasoning, differential-diagnosis logic, and medical justification before the final answer selection.
- **Hybrid Storage:** I indexed vector embeddings of questions and their explanation text in Pinecone while storing relational metadata, answer choices, answer keys, and complete reasoning traces in SQLite. Pinecone held the searchable explanation embeddings; SQLite held the underlying metadata and traces.
- **Prompting Benchmarks:** I evaluated zero-shot, few-shot, and five-shot configurations on clinical-question datasets, including the August dataset.
- **Dynamic Five-Shot Retrieval:** I searched Pinecone for the five most semantically relevant example questions for each new query and used those retrieved exemplars to guide reasoning.
- **Option-Shuffle Robustness:** I ran Dynamic Five-Shot plus five-way answer-option-shuffle experiments on the August and USMLE-Test datasets. I permuted A, B, C, and D ordering five times per question to measure position bias and test whether the model's answer reflected medical reasoning rather than option placement.

#### 4. SMS Classification, Fine-Tuning & Quantization

- **Period:** June 2024
- **Stack:** Python, LLaMA 3 8B and 70B, Phi-3 Mini and Medium, SetFit, BERT, Unsloth/QLoRA, GPT-4, GPT-3.5, FastAPI, Hugging Face Spaces, NVIDIA T4 and A100 GPUs

- **GPU Benchmarking:** I benchmarked LLaMA 3-8B, LLaMA 3-70B with 4-bit quantization, and LLaMA 3-70B with 6-bit quantization. I measured latency and token-generation speed on two 16 GB NVIDIA T4 GPUs and one 80 GB NVIDIA A100 GPU, and compared multiclass SMS-classification accuracy across Phi-3, LLaMA 3-70B, GPT-4, and GPT-3.5.
- **Phi-3 Fine-Tuning:** I curated 200 real transaction and promotional SMS messages, labeled them with GPT-4, and split them into 160 training and 40 test examples. I fine-tuned Phi-3 Mini and Medium with Unsloth's memory-efficient QLoRA approach and measured accuracy by entity type, transaction-versus-offer classification, and detailed subcategory.
- **SetFit Fine-Tuning & Deployment:** I fine-tuned SetFit for fast SMS classification, created text-normalization and noise-reduction preprocessing, integrated the model into a real-time FastAPI inference endpoint, and deployed it to Hugging Face Spaces.

#### Internship Technology Stack

- **Programming:** Python 3.x, SQL
- **AI/ML & LLMs:** OpenAI Chat, Embeddings, and Assistant APIs; LLaMA 3 8B and 70B; Phi-3 Mini and Medium; SetFit; BERT; Unsloth/QLoRA; Chain-of-Thought prompting; RAG
- **Databases & Vector Search:** Pinecone, Supabase/PostgreSQL, SQLite3
- **Backend & APIs:** FastAPI, REST APIs, Pydantic
- **Frontend:** Streamlit
- **Cloud & Deployment:** Docker, Google Cloud Platform, Cloud Run, Google Cloud Storage, Azure, Hugging Face Spaces
- **Hardware:** NVIDIA T4 16 GB and NVIDIA A100 80 GB GPUs

#### Key Highlights

- Built TVAM's conversational Health Advisor and medical-document analysis APIs with OpenAI models, FastAPI, Streamlit, Docker, Google Cloud Storage, and Cloud Run.
- Developed and deployed a health-insurance RAG system on Azure using OpenAI embeddings, Pinecone retrieval, Supabase conversation persistence, FastAPI, and Streamlit.
- Built a medical-reasoning evaluation system over 7,000 USMLE questions using dynamic five-shot retrieval, Pinecone explanation embeddings, SQLite metadata, and five-way answer-option shuffling.
- Benchmarked LLaMA 3, Phi-3, GPT-4, and GPT-3.5 classification performance and quantization tradeoffs across dual NVIDIA T4 and 80 GB A100 GPU environments.
- Fine-tuned Phi-3 Mini and Medium with Unsloth QLoRA on a curated 200-message SMS dataset, measuring performance across classification, entity, and subcategory tasks.
- Fine-tuned and deployed a SetFit SMS classifier as a real-time FastAPI endpoint on Hugging Face Spaces with text-normalization and noise-reduction preprocessing.
