---
title: "AWS re:Invent 2024 GENAI Updates"
date: 2024-12-06 00:00:00 +0000
categories: [LLM, GENAI]
tags: [AWS, Bedrock, Responsible AI, Anthropic, nova]
---

![Flowchart](assets/images/AWS reinvent updates.png)
## 1.  Generative AI & Bedrock Enchancements


### Automated Reasoning Checks:
 Ensures factual accuracy by verifying model outputs mathematically—critical for high-stakes use cases like insurance claims.

### Bedrock Agents with Multi-Agent Collaboration:
 This new feature allows agents to work together on complex workflows, sharing insights and coordinating tasks seamlessly.

### Supervisor Agents:
 Enables Management of dozens (or possibly hundreds) of task-specific agents, deciding if tasks run sequentially or in parallel and resolving conflicts. For example: A global coffee chain analyzing new store locations. One agent analyzes economic factors, another local market dynamics, and a third financial projections. The supervisor agent ties everything together, ensuring optimal collaboration.

### Intelligent Prompt Routing:
 Optimizes model selection within a family of models based on the complexity of the prompt for quality and cost, potentially reducing costs by up to 30% without compromising accuracy. 

### Prompt Caching: 
 Allows reuse of frequent contexts, reducing costs by up to 90% and latency by up to 85% for supported models.

### New API data ingestion 
 Introduces support for reranking models, custom connectors, and streaming data ingestion and , direct API for efficient data ingestion improving efficiency and real-time data availability.

### RAG evaluation 
 Enables automatic assessment based on LLM-as-a-judge and optimization of Retrieval Augmented Generation applications using Amazon Bedrock Knowledge Bases.


## 2. Nova
AWS unveiled Nova, a new family of multimodal generative AI models designed for diverse applications in text, image, and video generation. Here's what's new:
### a. Nova Text-Generating Models
Four Models:
- Micro: Text-only, low latency, fast response.
- Lite: Handles text, images, and video; reasonably quick.
- Pro: Balances speed, accuracy, and cost for multi-modal tasks.
- Premier(in training): Most advanced; ideal for complex workloads and custom model training.
Capabilities:
 Context windows of up to 300,000 tokens (225,000 words); expanding to 2 million tokens in early 2025.
 Fine-tunable on AWS Bedrock for enterprise-specific needs.
Use Cases:
 Summarizing documents, analyzing charts, and generating insights across text, image, and video.


### b. Generative Media Models
Nova Canvas:
 Creates and edits images using text prompts.
 Offers control over styles, color schemes, and layouts.

Nova Reel:
 Generates six-second videos from prompts or reference images, with customizable camera motions like pans and 360° rotations.
 A two-minute video generation feature is coming soon.

## 3. Upcoming Features
Speech-to-Speech Model (Q1 2025):
 - Transforms speech with natural human-like voice outputs.
 - Interprets verbal and nonverbal cues like tone and cadence.


### Any-to-Any Model (Mid-2025):
 - Processes text, speech, images, or video inputs and generates outputs in any of these formats.
 - Applications include translation, content editing, and AI assistants.




## References
- [New API data ingestion](https://aws.amazon.com/blogs/aws/new-apis-in-amazon-bedrock-to-enhance-rag-applications-now-available/)
- [Guardrails ARC](https://aws.amazon.com/blogs/aws/prevent-factual-errors-from-llm-hallucinations-with-mathematically-sound-automated-reasoning-checks-preview/)
- [RAG evaluation](https://aws.amazon.com/blogs/aws/new-rag-evaluation-and-llm-as-a-judge-capabilities-in-amazon-bedrock/)
- [AWS Nova](https://aws.amazon.com/blogs/aws/introducing-amazon-nova-frontier-intelligence-and-industry-leading-price-performance/)
- [Technical report](https://assets.amazon.science/9f/a3/ae41627f4ab2bde091f1ebc6b830/the-amazon-nova-family-of-models-technical-report-and-model-card.pdf) 
- [AWS subreddit](https://www.reddit.com/r/aws/comments/1h5uo48/aws_reinvent_2024_keynote_highlights/)

