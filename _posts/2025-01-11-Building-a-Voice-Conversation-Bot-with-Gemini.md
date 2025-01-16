---
title: "Building a Real-Time Audio Chatbot with Twilio, FastAPI, and Google Gemini’s Multimodal Live API"
date: 2025-01-11 00:00:00 +0000
categories: [LLM, GENAI, Multimodal, RAG]
tags: [AWS, Bedrock, Twilio, FastAPI,Pipecat]
---

![Architecture Diagram ](assets/images/Realtime-voice-2025-01-16-131205.png)
In the realm of conversational AI, real-time audio bots are becoming increasingly relevant. Whether you’re building customer support systems, voice-activated services, or interactive hotlines, combining a powerful AI model with robust telephony services can provide a seamless and engaging user experience.
The challenges of the current ecosystem of audio bots are they tend to be rigidly configured, limiting their adaptability and making them less effective in dynamic scenarios. Moreover, their responses often come across as overly robotic, impacting user engagement and overall effectiveness. Additionally, they frequently fail to capture and react to a customer’s tone, compromising the quality of the interaction. For example, if a user needs the bot to slow down so they can note down important information, most existing systems are unable to adjust their response style accordingly, leading to frustration and reduced satisfaction.

With the advent of realtime speech-to-speech models and multimodals (supporting text, video along with speech) has opened up possiblities of combining these powerful GENAI models with robust telphony services to provide a seamless and engaging user experience. “Multimodal” means you can use any combination of audio, video, images, and/or text in your interactions. And “real-time” means that things are happening quickly enough that it feels conversational—a “back-and-forth” with a bot, not submitting a query and waiting for results.

In this post, we will explore how you can create a multimodal voice conversation bot leveraging Pipecat, Twilio (for telephony voice call handling), FastAPI (for the server and WebSocket connections), and Google’s Gemini (a multimodal AI system). The goal is to provide an overview of the architecture and the necessary steps—focusing on how the pieces fit together rather than diving into heavy code snippets. If you want to setup the architecture yourself check out the [repository](https://github.com/kailashsp/realtime-conversation-voice-AI-agent).

## What Is Gemini’s Multimodal Live API?

Google’s Multimodal Live API provides a bidirectional (two-way) streaming interface for natural, human-like voice conversations and interruptible responses. Leveraging Google Gemini, it supports audio and video input, plus text—and it can return either text or audio. 

Key highlights include:

1. **Multimodality:** The model can see, hear, and speak (accepting audio/video, returning text or spoken responses).  
2. **Low-Latency Real-Time Interaction:** Ideal for voice calls or video conferencing scenarios.  
3. **Session Memory:** Remembers previous interactions within a session, so you don’t have to repeat context.  
4. **Function Calling & Code Execution:** Gemini can call external APIs (like database lookups or code execution) mid-conversation, returning results to the user.  
5. **Voice Activity Detection (VAD):** Automatically detects when a user starts/stops talking, allowing for natural, interruptible conversation.

---

## Core Components

### 1. Twilio for Real-Time Audio Streaming
Twilio is a cloud communications platform offering a simple way to receive phone calls and stream real-time audio. Here’s what Twilio does in this setup:

- **Phone Number Provisioning:** Once you buy or assign a Twilio phone number, Twilio handles incoming calls to that number.  
- **Webhooks:** When a call comes in, Twilio “pings” your FastAPI application via a secure URL ( exposed using a tool like ngrok).  
- **Audio Streaming:** Twilio can send audio data to your server in real time via WebSockets, enabling immediate processing or transcription.

### 2. FastAPI for the Server and WebSocket Endpoints
FastAPI is a Python web framework known for its speed and ease of use. In our scenario:

- **Routes/Endpoints:** FastAPI defines HTTP endpoints to handle Twilio’s webhooks.  
- **WebSocket Gateway:** The audio stream from Twilio is handled by a WebSocket endpoint, where you can process or forward the audio data.  
- **Event Handling:** When audio data arrives (e.g., every time Twilio sends you a chunk of spoken audio), FastAPI can relay this data to Gemini’s speech recognition API or store it for later analysis.

### 3. Pipecat.ai for Orchestrating the Conversation Flow
Pipecat is a framework for building voice-enabled, real-time, multimodal AI applications. Pipecat is an open source Python framework that handles the complex orchestration of AI services, network transport, audio processing, and multimodal interactions.
In our case, we use pipecat's pipeline system to assemble the sequence of processors that handle different aspects of the conversation flow. Think of it like an assembly line where each station (processor) performs a specific task.

### 4. Gemini’s Multimodal Live API: Intelligent Processing
With the Multimodal Live API, you set up a session over WebSockets that transmits:

- **Audio (or optional video) from the caller.**  
- **User text if necessary** (for additional instructions).  
- **System instructions** to control tone, style, or constraints on how Gemini should respond.  
- **Function Calls** if the model needs to retrieve external data.

Gemini processes the inputs in real time, returns partial or final text/audio responses, and can be interrupted if the user speaks again. This preserves a fluid, back-and-forth conversation.

---

## End-to-End Voice Conversation

Let’s imagine a customer support scenario where a user calls a Twilio number to troubleshoot an issue:

1. **Call Initialization**  
   - User dials the Twilio number. Twilio sends a webhook request to your FastAPI endpoint.  
   - FastAPI responds with instructions (TwiML) telling Twilio to stream the audio to `wss://<your-server>/ws`.

2. **FastAPI ↔ Twilio Audio Streaming**  
   - As soon as the caller speaks, Twilio sends raw audio chunks via the WebSocket to FastAPI.  
   - FastAPI packages these chunks of messages and sends them to Gemini.

3. **Gemini Session Setup**  
   - Initially, FastAPI must open a session with Gemini’s Multimodal Live API.  
   - This includes your model (like `"gemini-2.0-flash-exp"`) and any system instructions or tools you want to declare (function calls, external APIs, etc.).

4. **Real-Time Processing & Response**  
   - Gemini converts the user’s speech to text, then processes any relevant context in the session.  
   - Gemini streams back partial or final messages. If you requested audio output, Gemini returns raw audio bytes, which you then forward to Twilio. Twilio can play it to the caller in real time.

5. **Interruptions**  
   - If the user interrupts, Gemini’s current response is canceled. Twilio sends new audio. Gemini starts a new turn.

6. **Function Calls (Optional)**  
   - If the user asks a question requiring external data (e.g., “What’s my account balance?”), Gemini may generate a function call 
   - Your server runs the function or calls an external service, then sends the result back.  
   - Gemini uses the returned data to craft the final answer for the user in the audio.
   - In our example we have integrated a knowledge base from AWS to get more context. You can set up your own RAG setup to increase the context

7. **Session Conclusion**  
   - When the call ends or times out, FastAPI closes the session. Gemini discards the conversation memory.  
   - If you want to restore context later, you’d store it yourself and send it to Gemini in a new session.

---

## Conclusion

By pairing Twilio’s real-time phone streaming capabilities with FastAPI and Pipecat for orchestrating the data flow, you can harness Google Gemini’s Multimodal Live API to build truly interactive voice bots. Users can speak naturally, ask follow-up questions, and even interrupt the bot mid-sentence—just like a human conversation. Meanwhile, the bot can leverage advanced features such as function calling, code execution, and external data lookups for highly dynamic, context-aware interactions.

As voice AI matures, the Multimodal Live API opens the door to integrating video, images, and even real-time function calls—enabling experiences that feel more personal, immediate, and human. Whether you’re building an IVR system, a customer support line, or a voice assistant, the combination of Twilio + FastAPI + Gemini can deliver a next-level conversational experience.


## References:

1. https://ai.google.dev/api/multimodal-live
2. https://www.pipecat.ai/
3. https://github.com/pipecat-ai/pipecat/tree/main/examples
4. https://www.twilio.com/docs
5. https://fastapi.tiangolo.com/