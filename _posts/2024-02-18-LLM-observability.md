---
title: "Observability in LLM apps"
date: 2024-08-18 00:00:00 +0000
categories: [LLM]
tags: [OBSERVABILITY, MONITORING]
---

# Observability in LLM apps

LLM Observability enables us to monitor our LLM calls and troubleshoot issues in the LLM apps so that we can resolve issues faster. The probabilistic nature of LLM outputs can result in some unforeseen issues in our LLM pipeline. But before we can monitor, we need to decide what things need to be tracked in order to debug issues.

LLM model parameters such as temperature, TopK, and TopP could be reasons why you don't get the expected answer. However, usually, the major issues can be solved by tweaking the way you prompt the model.

LLM Observability is crucial in chatbots which use RAG to prevent hallucination and provide the most factual results. This kind of goes against the probabilistic nature of the LLMs. If you think about it, you are essentially trying to work against the default behavior of LLMs by opting for a RAG approach, but that does not mean it is not suitable. RAG chatbots are still efficient solutions that can help users with questions related to their field more easily, and it also helps that the LLMs can be more engaging for the end user.

For a RAG chatbot, in addition to the parameters of the model and prompt, it is important to log the relevant documents that you get from the retriever and their scores. This step can help you understand whether the problem is arising from the retriever or generator.

## Conclusion

The architecture of your LLM app can make you want to log different parameters that can influence outputs. But to start off, you can log:

- **Model parameters**
- **Source documents from retriever for RAG**