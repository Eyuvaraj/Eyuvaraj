# Yuvabe — AI/ML Engineer & AI/ML Intern

## Role Progression

**YUVABE**, Auroville, Tamil Nadu.
- **AI/ML Engineer** — Jul 2024 – Aug 2025
- **AI/ML Intern** — Jan 2024 – Jun 2024

## Overview
Built and shipped production AI systems at Yuvabe spanning multi-agent LLM
platforms, RAG pipelines, on-device/edge AI, SMS/NLP intelligence, and
conversational avatar systems — full backend ownership (FastAPI, Docker,
Azure) plus applied ML/LLM engineering across healthcare, finance, education,
and marketing domains.

## Technical Work

### 1. High-Impact Architecture and Platform Work
- **Architected a Production Multi-Agent AI Platform** — Architected and
  deployed a production multi-agent AI platform serving 100,000+ users across
  healthcare, finance, education, and marketing domains. Designed a routing
  layer that dynamically directs user queries to specialized agents for
  health advice, policy analysis, and document processing. Implemented
  OpenAI function calling, RAG pipelines, and multimodal text and voice
  interaction through a unified FastAPI backend deployed on Azure with
  Docker. This architecture enabled scalable, domain-aware AI responses
  while reducing hallucinations through grounded retrieval and agent
  specialization.
- **Built a Production Retrieval-Augmented Generation Platform** — Developed
  a full production RAG system capable of handling large document
  collections such as insurance policies and medical reports. Implemented
  the complete pipeline including document parsing, semantic chunking,
  embedding generation using OpenAI models, vector storage in Pinecone,
  similarity search retrieval, and grounded response generation. Served the
  system through a FastAPI backend with conversation persistence via
  Supabase, enabling reliable document-aware question answering for a
  platform serving 100,000+ users.
- **Designed AI Microservices Following MACH Architecture Principles** —
  Designed and deployed modular AI microservices using Python, FastAPI,
  Docker, and Azure cloud infrastructure. Followed MACH architecture
  principles to create independently deployable services for inference,
  document processing, classification, and conversational interaction. This
  approach improved maintainability, enabled horizontal scaling of AI
  workloads, and allowed new models or services to be deployed without
  disrupting existing production systems.

### 2. Advanced LLM Systems and Agentic Workflows
- **Engineered Multi-Agent LLM Workflows for Specialized Reasoning** —
  Designed agentic LLM workflows combining Chain of Thought reasoning and
  ReAct prompting strategies to improve reliability in complex
  decision-support systems. Built intermediary routers and specialized
  sub-agents responsible for tasks such as policy interpretation, medical
  reasoning, and document analysis. Implemented tool calling and context
  management across agents to ensure consistent responses while minimizing
  hallucinations in high-stakes advisory applications.
- **Built a Large-Scale Medical Reasoning Q&A System** — Developed a medical
  reasoning system using 7,000 USMLE examination questions to simulate
  expert-level medical problem solving. Implemented Chain of Thought
  prompting and dynamic few-shot selection to generate structured reasoning
  traces. Stored these traces in a Pinecone and SQLite retrieval system to
  enable retrieval-augmented reasoning during inference, improving
  consistency and allowing the model to reference prior reasoning patterns.
- **Implemented LLM Pipelines for Automated Knowledge Generation** —
  Developed modular LLM pipelines that automatically generate structured
  outputs such as brand guidelines, identity documents, and marketing
  campaign drafts from structured questionnaires. Designed orchestration
  workflows that transform raw user input into structured knowledge
  artifacts, reducing manual content creation time and enabling repeatable
  generation pipelines.

### 3. NLP, SMS Intelligence, and Predictive Machine Learning
- **Built a Multi-Layer SMS Intelligence Pipeline** — Developed a production
  SMS intelligence system that converts unstructured SMS messages into
  structured financial insights. Designed a multi-tier pipeline during the internship using LLaMA
  3.0, BERT, SetFit, and GPT-4 models to perform binary classification,
  hierarchical category classification, and entity extraction. Processed
  more than 100,000 SMS messages across experimentation and production use.
- **Fine-Tuned Transformer Models for Noisy Real-World Data** — Fine-tuned
  BERT and SetFit models for SMS classification tasks involving noisy,
  real-world data containing informal language, abbreviations, and mixed
  formatting. Implemented feature engineering, training pipelines, and
  evaluation workflows to improve classification accuracy and robustness
  across different message categories.
- **Developed Multimodal Predictive ML Pipelines for Brand Intelligence** —
  Designed machine learning pipelines capable of analyzing social media data
  including text, images, and video. Applied NLP, computer vision, and
  clustering techniques to extract sentiment trends, brand perception
  metrics, and campaign insights. Built systems that transform raw social
  data into actionable intelligence for marketing and product teams.

### 4. Edge AI and On-Device LLM Systems
- **Researched and Implemented Fully Offline RAG Systems on Android** —
  Designed and implemented a complete on-device RAG architecture for Android
  that performs document parsing, embedding generation, vector search, and
  language model inference entirely offline. Used ONNX Runtime to run the
  all-MiniLM embedding model locally, ObjectBox with HNSW indexing for
  vector storage, and Llama.cpp to run small language models such as LLaMA
  3.1 for response generation during the full-time engineer role.
- **Benchmarked On-Device LLM Inference Across Mobile Hardware** — Conducted
  extensive benchmarking experiments to evaluate the feasibility of
  on-device AI inference. Tested models including Qwen2.5, Phi-3 Mini, and
  LLaMA 3.1 across ONNX Runtime and Llama.cpp environments. Achieved
  approximately 19.6 tokens per second on a 6GB RAM Android device using a
  0.43GB quantized model, demonstrating practical feasibility for offline
  conversational AI.
- **Investigated Retrieval and Hallucination Challenges in Small Language
  Models** — Performed research into limitations of small language models
  operating under mobile hardware constraints. Identified failure modes
  related to context length limitations, hallucination patterns, and
  retrieval errors. Proposed improvements including metadata filtering,
  better chunk preprocessing, and optimized retrieval strategies to improve
  answer reliability in edge environments.

### 5. Conversational Avatars, Voice Systems, and Interactive AI
- **Engineered a Real-Time Conversational Avatar System on Android** —
  Developed an interactive conversational avatar platform that integrates 3D
  avatars, speech synthesis, lip synchronization, and animation into a
  mobile AI experience. Implemented runtime avatar creation from user
  photos, integrated voice synthesis pipelines, and synchronized
  viseme-driven lip sync animation to create a natural conversational
  interface.
- **Built a Unity-Based 3D Avatar System with Runtime Lip Sync** — Developed
  an Android application in Unity featuring real-time avatar rendering,
  Azure-based text-to-speech synthesis, and Oculus Lip Sync for
  viseme-driven facial animation. Modified the Ready Player Me SDK source
  code to enable runtime lip sync functionality not supported by the default
  SDK. Implemented avatar caching and persistence mechanisms to support
  offline reuse after the initial download.
- **Developed Dual-Avatar Dialogue Systems with Dynamic Camera Control** —
  Designed a dialogue engine that supports conversations between two avatars
  driven by JSON scripts. Implemented synchronized audio generation, lip
  sync animation, randomized idle animations, and camera transitions that
  track the active speaking avatar, enabling cinematic multi-character
  interactions.
- **Deployed Avatar Generation APIs Using Ready Player Me** — Automated
  avatar creation from a single user photo by integrating the Ready Player
  Me API through a Python service. Packaged the solution as a publicly
  accessible REST API and deployed it on Hugging Face Spaces, enabling
  avatar generation without requiring a dedicated frontend interface.

### 6. Backend Systems, APIs, and Infrastructure Engineering
- **Built Secure Backend APIs for AI-Powered Applications** — Developed
  RESTful APIs supporting document upload, processing, summarization,
  question answering, and metadata extraction across multiple client
  applications. Implemented secure endpoints and standardized request
  pipelines that allow web and mobile applications to integrate AI
  capabilities without tight coupling.
- **Containerized and Deployed Full-Stack AI Applications** — Packaged
  backend services, AI pipelines, and frontend applications into Docker
  containers and deployed them on Azure cloud infrastructure. Configured
  development and production environments to support scalable deployments
  and reproducible builds.
- **Implemented Conversation Persistence and State Management** — Designed
  database schemas in Supabase to persist conversation history across
  sessions. Implemented query flows and storage strategies to support
  multi-turn dialogue systems where context continuity is required for
  effective LLM interaction.
- **Migrated Legacy Backend Services from Node.js to ASP.NET** — Modernized
  backend infrastructure by migrating eight REST API endpoints from Node.js
  to ASP.NET using C#. Independently learned the C# language and the .NET
  ecosystem to complete the migration successfully while maintaining API
  compatibility and service reliability.

### 7. LLM Evaluation, Benchmarking, and Applied Research
- **Evaluated Open Source LLMs as Alternatives to Proprietary APIs** —
  Conducted evaluation studies on open source models such as LLaMA 3.1, Qwen,
  and other emerging models as potential replacements for proprietary APIs.
  Tested their ability to perform classification, function calling, and
  generation tasks under complex routing conditions in multi-agent systems.
- **Benchmarked Model Performance Across Hardware and Quantization Levels**
  — Performed benchmarking experiments comparing LLaMA 3.1, Phi-3, GPT-4, and
  GPT-3.5 across GPU hardware including dual T4 instances and A100 80GB
  accelerators. Analyzed trade-offs between 4-bit and 6-bit quantization
  strategies to balance model quality, inference latency, and memory usage.
- **Investigated Failure Modes in Function Calling and Agent Routing** —
  Tested open source models for function calling reliability within
  multi-agent pipelines. Identified failure patterns including premature
  tool invocation, hallucinated tool outputs, and empty string responses.
  Documented these behaviors to guide future model selection and system
  design decisions.

## Scale and Scope
- 100,000+ users served by the multi-agent platform.
- 7,000 USMLE questions used to build the medical reasoning Q&A system.
- More than 100,000 SMS messages processed across experimentation and production use.
- ~19.6 tokens/sec on-device inference on a 6GB RAM Android device, 0.43GB
  quantized model.
- 8 REST API endpoints migrated Node.js → ASP.NET (C#), learned independently.
- Benchmarking spanned dual T4 and A100 80GB GPUs, 4-bit vs. 6-bit
  quantization.
- Tech stack overall: Python, FastAPI, Docker, Azure, OpenAI API/function
  calling, Pinecone, Supabase, LLaMA 3.0 (internship), LLaMA 3.1 (full-time), BERT, SetFit, GPT-4/GPT-3.5,
  ONNX Runtime, ObjectBox (HNSW), Llama.cpp, Qwen2.5, Phi-3 Mini, Unity,
  Azure TTS, Oculus Lip Sync, Ready Player Me SDK, Node.js, ASP.NET/C#,
  SQLite.

## Selected Highlights
- **AI/ML Engineer** (8 bullets): multi-agent RAG platform, production RAG
  pipeline, agentic Chain-of-Thought/ReAct workflows, offline Android RAG
  (ONNX/ObjectBox/Llama.cpp, 19.6 tok/s), GPU/quantization benchmarking,
  Unity avatar system, Node.js→ASP.NET migration, MACH-principle
  microservices.
- **AI/ML Intern** (5 bullets): SMS intelligence pipeline (more than 100,000 messages),
  BERT/SetFit fine-tuning,
  medical reasoning Q&A (7,000 USMLE questions), automated LLM
  knowledge-generation pipelines.

Additional work includes a dual-avatar dialogue engine with dynamic camera
control, a Ready Player Me avatar-generation API on Hugging Face Spaces,
Supabase-backed conversation persistence, secure document-processing APIs,
multimodal social-media intelligence pipelines, and open-source LLM
function-calling evaluation.

## Ready-to-Use Highlights
- Architected a multi-agent RAG platform serving 100,000+ users, routing queries to specialized domain agents via FastAPI on Azure.
- Built a production RAG pipeline for insurance/medical documents using OpenAI embeddings, Pinecone retrieval, and Supabase persistence.
- Designed agentic Chain-of-Thought/ReAct workflows with specialized sub-agents to cut hallucinations in advisory use cases.
- Built a medical reasoning Q&A system on 7,000 USMLE questions, storing CoT traces in Pinecone/SQLite for retrieval-augmented inference.
- Engineered a fully offline Android RAG pipeline with LLaMA 3.1 (ONNX Runtime, ObjectBox HNSW, Llama.cpp), reaching 19.6 tok/sec on a 6GB-RAM device during the full-time role.
- Benchmarked LLaMA 3.1, Phi-3, GPT-4, and GPT-3.5 across T4/A100 GPUs, comparing 4-bit vs. 6-bit quantization for model selection during the full-time role.
- During the internship, engineered a multi-tier SMS intelligence pipeline (LLaMA 3.0, BERT, SetFit, GPT-4), processing more than 100,000 SMS messages across experimentation and production use.
- Fine-tuned BERT/SetFit on noisy real-world SMS text, building training and evaluation pipelines to improve robustness.
- Shipped a real-time Unity avatar system with Azure TTS and Oculus Lip Sync, patching a third-party SDK for runtime lip-sync.
- Built a dual-avatar dialogue engine with synchronized audio, lip sync, and dynamic camera control between speakers.
- Deployed a Ready Player Me avatar-generation API as a public REST service on Hugging Face Spaces.
- Migrated 8 REST API endpoints from Node.js to ASP.NET (C#), learning the .NET ecosystem independently.
- Structured modular AI microservices on Python, FastAPI, Docker, and Azure using MACH principles for independent scaling.
- Designed Supabase-backed conversation persistence to support context continuity in multi-turn LLM dialogue systems.
- Automated LLM pipelines turning structured questionnaires into brand guidelines and campaign drafts.
- Built predictive ML pipelines analyzing multimodal social data (text, image, video) for brand-intelligence signals.
- Evaluated open-source LLMs (LLaMA 3.1, Qwen) as proprietary-API alternatives for classification and function-calling reliability during the full-time role.
