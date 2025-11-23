# n8n-ai-slack-workflow
My n8n workflow for automating Slack message handling with AI and transcription

🧠 Slack AI Assistant — n8n Workflow

This repository contains my implementation of a full n8n-based Slack AI assistant workflow.
The system processes Slack messages (both text and audio), transcribes audio, generates intelligent responses using LLMs, and replies back in the same Slack thread.

This project was built as part of an assignment opportunity, and through this I learned deeply about n8n workflow design, Slack integrations, API orchestration, AI chaining, and workflow debugging.

📌 Features Implemented
✅ Slack → n8n Communication

Slack Trigger node receives messages/events

Thread context extraction ensures replies stay in the same Slack thread

✅ Audio Detection Pipeline

Detect Audio Type node confirms whether the incoming Slack message contains an audio file

Branching using an Audio Gate (true/false)

True → Audio processing

False → Direct text-based AI response

✅ Audio Processing

Set Audio Meta node assigns MIME type & metadata

Download Slack Audio node retrieves the file binary

Transcription performed using Hugging Face Whisper / Audio models

Transcription merged into user message flow

✅ AI Message Handling

Message Model (OpenAI/HF) generates responses

Dynamic prompts based on user message and context

Error-handling improvements

Clean formatting of build-plan answers

✅ Threaded Replies

Replies posted back to Slack inside the originating thread

Uses thread_ts from Thread Context node

🚧 Work in Progress (WIP)
🔄 Conversation Memory

I am currently working on:

Implementing memory storage using Data Table (n8n)

Saving previous conversation turns per Slack thread_ts

Retrieving memory and merging it with the next user message

Building a multi-turn contextual assistant

This will be added soon.

🛠️ How to Use This Workflow
1. Import into n8n

Go to n8n → Workflows → Import

Upload n8n_workflow.json

2. Configure Credentials

You must add:

Slack API Credential

OpenAI / HuggingFace API Key

Slack Bot Signing Secret (if needed)

3. Enable Workflow

Turn on workflow activation.

4. Test from Slack

Send a message (text or audio) to your Slack bot:

Text is processed via the Message Model

Audio is transcribed → fed to the model
You will receive a response in the same thread.

📸 Workflow Structure (High-Level Diagram)

Slack Trigger
      ↓
Thread Context
      ↓
Detect Audio Type
      ↓
 ┌─────────────┐
 │   Audio?     │
 └─────┬───────┘
   Yes ↓     No ↓
 Set Audio     Direct to
   Meta        Message Model
    ↓              ↓
Download Audio   Build Plan Generation
    ↓              ↓
Transcription    Slack Send Message
    ↓
Message Model
    ↓
Slack Send Message

🌟 Key Learnings from This Project

Advanced n8n node linking & branching

Handling binary data & media files

Whisper API integration

Slack app configuration (token scopes, event triggers, thread replies)

AI agent design in workflow automation

Debugging complex flows and solving real API issues
