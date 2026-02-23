# AI-ML Engineer | YUVABE  
Jan 2024 – Aug 2025 • Auroville, Tamil Nadu

## High-Impact Architecture and Platform Work

### Architected a Production Multi-Agent AI Platform
Architected and deployed a production multi-agent AI platform serving 100,000+ users across healthcare, finance, education, and marketing domains. Designed a routing layer that dynamically directs user queries to specialized agents for health advice, policy analysis, and document processing. Implemented OpenAI function calling, RAG pipelines, and multimodal text and voice interaction through a unified FastAPI backend deployed on Azure with Docker. This architecture enabled scalable, domain-aware AI responses while reducing hallucinations through grounded retrieval and agent specialization.

### Built a Production Retrieval-Augmented Generation Platform
Developed a full production RAG system capable of handling large document collections such as insurance policies and medical reports. Implemented the complete pipeline including document parsing, semantic chunking, embedding generation using OpenAI models, vector storage in Pinecone, similarity search retrieval, and grounded response generation. Served the system through a FastAPI backend with conversation persistence via Supabase, enabling reliable document-aware question answering for thousands of users.

### Designed AI Microservices Following MACH Architecture Principles
Designed and deployed modular AI microservices using Python, FastAPI, Docker, and Azure cloud infrastructure. Followed MACH architecture principles to create independently deployable services for inference, document processing, classification, and conversational interaction. This approach improved maintainability, enabled horizontal scaling of AI workloads, and allowed new models or services to be deployed without disrupting existing production systems.

---

## Advanced LLM Systems and Agentic Workflows

### Engineered Multi-Agent LLM Workflows for Specialized Reasoning
Designed agentic LLM workflows combining Chain of Thought reasoning and ReAct prompting strategies to improve reliability in complex decision-support systems. Built intermediary routers and specialized sub-agents responsible for tasks such as policy interpretation, medical reasoning, and document analysis. Implemented tool calling and context management across agents to ensure consistent responses while minimizing hallucinations in high-stakes advisory applications.

### Built a Large-Scale Medical Reasoning Q&A System
Developed a medical reasoning system using 7,000 USMLE examination questions to simulate expert-level medical problem solving. Implemented Chain of Thought prompting and dynamic few-shot selection to generate structured reasoning traces. Stored these traces in a Pinecone and SQLite retrieval system to enable retrieval-augmented reasoning during inference, improving consistency and allowing the model to reference prior reasoning patterns.

### Implemented LLM Pipelines for Automated Knowledge Generation
Developed modular LLM pipelines that automatically generate structured outputs such as brand guidelines, identity documents, and marketing campaign drafts from structured questionnaires. Designed orchestration workflows that transform raw user input into structured knowledge artifacts, reducing manual content creation time and enabling repeatable generation pipelines.

---

## NLP, SMS Intelligence, and Predictive Machine Learning

### Built a Multi-Layer SMS Intelligence Pipeline
Developed a production SMS intelligence system that converts unstructured SMS messages into structured financial insights. Designed a multi-tier pipeline using LLaMA 3.1, BERT, SetFit, and GPT-4 models to perform binary classification, hierarchical category classification, and entity extraction. Processed over 15,000 messages during experimentation and scaled the system to handle over 100,000 financial records monthly.

### Fine-Tuned Transformer Models for Noisy Real-World Data
Fine-tuned BERT and SetFit models for SMS classification tasks involving noisy, real-world data containing informal language, abbreviations, and mixed formatting. Implemented feature engineering, training pipelines, and evaluation workflows to improve classification accuracy and robustness across different message categories.

### Developed Multimodal Predictive ML Pipelines for Brand Intelligence
Designed machine learning pipelines capable of analyzing social media data including text, images, and video. Applied NLP, computer vision, and clustering techniques to extract sentiment trends, brand perception metrics, and campaign insights. Built systems that transform raw social data into actionable intelligence for marketing and product teams.

---

## Edge AI and On-Device LLM Systems

### Researched and Implemented Fully Offline RAG Systems on Android
Designed and implemented a complete on-device RAG architecture for Android that performs document parsing, embedding generation, vector search, and language model inference entirely offline. Used ONNX Runtime to run the all-MiniLM embedding model locally, ObjectBox with HNSW indexing for vector storage, and Llama.cpp to run small language models such as LLaMA 3.2 for response generation.

### Benchmarked On-Device LLM Inference Across Mobile Hardware
Conducted extensive benchmarking experiments to evaluate the feasibility of on-device AI inference. Tested models including Qwen2.5, Phi-3 Mini, and LLaMA variants across ONNX Runtime and Llama.cpp environments. Achieved approximately 19.6 tokens per second on a 6GB RAM Android device using a 0.43GB quantized model, demonstrating practical feasibility for offline conversational AI.

### Investigated Retrieval and Hallucination Challenges in Small Language Models
Performed research into limitations of small language models operating under mobile hardware constraints. Identified failure modes related to context length limitations, hallucination patterns, and retrieval errors. Proposed improvements including metadata filtering, better chunk preprocessing, and optimized retrieval strategies to improve answer reliability in edge environments.

---

## Conversational Avatars, Voice Systems, and Interactive AI

### Engineered a Real-Time Conversational Avatar System on Android
Developed an interactive conversational avatar platform that integrates 3D avatars, speech synthesis, lip synchronization, and animation into a mobile AI experience. Implemented runtime avatar creation from user photos, integrated voice synthesis pipelines, and synchronized viseme-driven lip sync animation to create a natural conversational interface.

### Built a Unity-Based 3D Avatar System with Runtime Lip Sync
Developed an Android application in Unity featuring real-time avatar rendering, Azure-based text-to-speech synthesis, and Oculus Lip Sync for viseme-driven facial animation. Modified the Ready Player Me SDK source code to enable runtime lip sync functionality not supported by the default SDK. Implemented avatar caching and persistence mechanisms to support offline reuse after the initial download.

### Developed Dual-Avatar Dialogue Systems with Dynamic Camera Control
Designed a dialogue engine that supports conversations between two avatars driven by JSON scripts. Implemented synchronized audio generation, lip sync animation, randomized idle animations, and camera transitions that track the active speaking avatar, enabling cinematic multi-character interactions.

### Deployed Avatar Generation APIs Using Ready Player Me
Automated avatar creation from a single user photo by integrating the Ready Player Me API through a Python service. Packaged the solution as a publicly accessible REST API and deployed it on Hugging Face Spaces, enabling avatar generation without requiring a dedicated frontend interface.

---

## Backend Systems, APIs, and Infrastructure Engineering

### Built Secure Backend APIs for AI-Powered Applications
Developed RESTful APIs supporting document upload, processing, summarization, question answering, and metadata extraction across multiple client applications. Implemented secure endpoints and standardized request pipelines that allow web and mobile applications to integrate AI capabilities without tight coupling.

### Containerized and Deployed Full-Stack AI Applications
Packaged backend services, AI pipelines, and frontend applications into Docker containers and deployed them on Azure cloud infrastructure. Configured development and production environments to support scalable deployments and reproducible builds.

### Implemented Conversation Persistence and State Management
Designed database schemas in Supabase to persist conversation history across sessions. Implemented query flows and storage strategies to support multi-turn dialogue systems where context continuity is required for effective LLM interaction.

### Migrated Legacy Backend Services from Node.js to ASP.NET
Modernized backend infrastructure by migrating eight REST API endpoints from Node.js to ASP.NET using C#. Independently learned the C# language and the .NET ecosystem to complete the migration successfully while maintaining API compatibility and service reliability.

---

## LLM Evaluation, Benchmarking, and Applied Research

### Evaluated Open Source LLMs as Alternatives to Proprietary APIs
Conducted evaluation studies on open source models such as LLaMA, Qwen, and other emerging models as potential replacements for proprietary APIs. Tested their ability to perform classification, function calling, and generation tasks under complex routing conditions in multi-agent systems.

### Benchmarked Model Performance Across Hardware and Quantization Levels
Performed benchmarking experiments comparing LLaMA, Phi-3, GPT-4, and GPT-3.5 across GPU hardware including dual T4 instances and A100 80GB accelerators. Analyzed trade-offs between 4-bit and 6-bit quantization strategies to balance model quality, inference latency, and memory usage.

### Investigated Failure Modes in Function Calling and Agent Routing
Tested open source models for function calling reliability within multi-agent pipelines. Identified failure patterns including premature tool invocation, hallucinated tool outputs, and empty string responses. Documented these behaviors to guide future model selection and system design decisions.

---

## Key Highlights

• Architected and deployed a production multi-agent AI platform serving 100,000+ users across healthcare, finance, education, and marketing, implementing a routing layer that directs queries to specialized agents for health advisory, policy analysis, and document processing using OpenAI function calling, RAG pipelines, and a unified FastAPI backend deployed on Azure with Docker.

• Built a production Retrieval Augmented Generation platform for document-aware question answering across insurance policies and medical reports, implementing document parsing, semantic chunking, OpenAI embeddings, Pinecone vector search, and grounded response generation served through FastAPI with conversation persistence in Supabase.

• Engineered agentic LLM workflows using Chain of Thought and ReAct prompting to improve reasoning reliability and reduce hallucinations in high-stakes advisory systems, implementing routers and specialized sub-agents for medical reasoning, policy interpretation, and document analysis.

• Developed a large-scale medical reasoning Q&A system using 7,000 USMLE questions, generating structured reasoning traces through dynamic few-shot prompting and storing them in a Pinecone + SQLite retrieval system to enable retrieval-augmented reasoning during inference.

• Built a multi-layer SMS intelligence pipeline converting raw SMS data into structured financial insights using LLaMA 3.1, BERT, SetFit, and GPT-4, implementing binary classifiers, hierarchical label trees, and LLM-based entity extraction to process over 100,000 transaction records monthly.

• Fine-tuned transformer models including BERT and SetFit for classification and entity extraction on noisy real-world datasets, designing training pipelines and evaluation workflows to improve robustness across unstructured SMS data.

• Designed predictive ML pipelines analyzing multimodal social media data including text, images, and video to generate brand intelligence signals such as sentiment trends, campaign performance indicators, and perception metrics.

• Designed and deployed modular AI microservices using Python, FastAPI, Docker, and Azure following MACH architecture principles, enabling independently deployable inference pipelines and horizontally scalable AI workloads.

• Built secure REST APIs for file upload, document processing, summarization, question answering, and metadata extraction, enabling multiple web and mobile clients to integrate AI capabilities through standardized backend services.

• Implemented conversation state persistence for multi-turn AI systems using Supabase database schemas and retrieval flows, enabling contextual dialogue across sessions in LLM applications.

• Designed and implemented a fully offline Retrieval Augmented Generation system for Android using ONNX Runtime for embedding inference, ObjectBox HNSW vector search for retrieval, and Llama.cpp for on-device language model inference.

• Conducted benchmarking experiments on on-device AI inference across models including Qwen2.5, Phi-3 Mini, and LLaMA variants using ONNX Runtime and Llama.cpp, achieving ~19.6 tokens/sec on a 6GB RAM Android device using a 0.43GB quantized model.

• Investigated retrieval accuracy and hallucination patterns in small language models operating under mobile hardware constraints and proposed improvements including metadata filtering and optimized chunk preprocessing strategies.

• Engineered a real-time conversational avatar system on Android integrating 3D avatar rendering, text-to-speech synthesis, viseme-driven lip synchronization, and animation pipelines to create immersive conversational AI interactions.

• Built a Unity Android application featuring runtime avatar generation from user photos using the Ready Player Me SDK, Azure TTS voice synthesis, and Oculus Lip Sync for real-time facial animation, modifying SDK source code to enable runtime lip sync functionality.

• Developed a dual-avatar dialogue engine supporting JSON-driven conversations with synchronized audio synthesis, lip sync animation, randomized idle behaviors, and dynamic camera control tracking the active speaking avatar.

• Automated avatar generation from single photos by integrating the Ready Player Me API into a Python service and deploying the system as a public REST API on Hugging Face Spaces.

• Evaluated open-source LLMs including LLaMA and Qwen as potential alternatives to proprietary APIs, testing classification, generation, and function calling reliability under multi-agent routing conditions.

• Benchmarked model performance across LLaMA, Phi-3, GPT-4, and GPT-3.5 using T4 and A100 GPUs, analyzing latency, accuracy, and quantization trade-offs between 4-bit and 6-bit configurations.

• Modernized backend infrastructure by migrating eight REST API endpoints from Node.js to ASP.NET using C#, independently learning the .NET ecosystem to deliver a fully functional backend service migration.