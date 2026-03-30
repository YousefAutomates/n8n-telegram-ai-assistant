<div align="center">

<!-- HERO BANNER -->
<img src="https://img.shields.io/badge/n8n-Telegram_AI_Assistant-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n Telegram AI Assistant" />

<br/>
<br/>

# Telegram AI Personal Assistant

### Multi-Agent Orchestrator Workflow for n8n

**Transform your Telegram into a powerful AI-powered personal assistant that manages your emails, calendar, web searches, and social media — all through natural conversation.**

<br/>

[![Built with n8n](https://img.shields.io/badge/Built_with-n8n-FF6D5A?style=flat-square&logo=n8n&logoColor=white)](https://n8n.io)
[![Powered by Groq](https://img.shields.io/badge/Powered_by-Groq_AI-F55036?style=flat-square&logo=groq&logoColor=white)](https://groq.com)
[![Telegram Bot](https://img.shields.io/badge/Platform-Telegram-26A5E4?style=flat-square&logo=telegram&logoColor=white)](https://telegram.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Cost](https://img.shields.io/badge/AI_Cost-$0_FREE-brightgreen?style=flat-square)](#cost-comparison)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square)](pulls)

<br/>

[**Quick Start**](#quick-start-guide) · [**Documentation**](#architecture-deep-dive) · [**Setup**](#prerequisites-and-credentials) · [**Examples**](#usage-examples) · [**Get Help**](https://yousefautomates.pages.dev/)

<br/>

---

### Language / اللغة

> **يتوفر شرح عربي مفصل بالاسفل — Arabic documentation available below**

| [English Documentation](#english-documentation) | [التوثيق العربي](#arabic-documentation) |
|:---:|:---:|

---

</div>

<!-- ================================================================== -->
<!-- ENGLISH DOCUMENTATION -->
<!-- ================================================================== -->

<a id="english-documentation"></a>

# English Documentation

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture Deep Dive](#architecture-deep-dive)
- [Workflow Flow Diagram](#workflow-flow-diagram)
- [Node-by-Node Reference](#node-by-node-reference)
- [AI Models Used](#ai-models-used-all-free)
- [Prerequisites and Credentials](#prerequisites-and-credentials)
- [Quick Start Guide](#quick-start-guide)
- [Detailed Setup Instructions](#detailed-setup-instructions)
- [Usage Examples](#usage-examples)
- [Cost Comparison](#cost-comparison)
- [Troubleshooting](#troubleshooting)
- [Security Considerations](#security-considerations)
- [Contributing](#contributing)
- [Professional Services](#professional-automation-services)

---

## Overview

This is a **production-ready n8n workflow** that turns a Telegram bot into a fully autonomous AI personal assistant. It uses a **Multi-Agent Orchestrator Architecture** where a central AI brain intelligently routes your requests to specialized sub-agents.

### What makes this special?

| Feature | Description |
|---------|-------------|
| **100% Free AI** | All AI models run on Groq with zero cost |
| **Multi-Agent** | 4 specialized AI agents + 1 orchestrator |
| **Voice Support** | Send voice message and get voice reply |
| **Vision AI** | Send photos and AI understands them |
| **Memory** | Remembers last 50 messages per user |
| **Fast** | Groq LPU delivers sub-second inference |

---

## Key Features

### Multi-Modal Input Processing
```
Text Messages    --> Direct processing
Voice Messages   --> Groq Whisper transcription --> Processing
Photo Messages   --> Groq Vision analysis --> Processing
Photo + Caption  --> Combined understanding
```

### Intelligent Agent Routing
```
Email Agent      --> Send / reply / delete / read-unread emails (Gmail)
Calendar Agent   --> Create / update / delete / list events (Google Calendar)
Search Agent     --> Google Search / Tavily Search / Wikipedia / Hacker News
Social Media     --> Create and save Twitter-X posts (Google Sheets)
Think Tool       --> Internal reasoning before decisions
```

### Smart Output
```
Voice Input  --> Voice Reply (Groq PlayAI TTS)
Text Input   --> Text Reply (Markdown formatted)
Image Input  --> Text Reply (with image analysis)
```

---

## Architecture Deep Dive

### System Architecture

```
+------------------------------------------------------------------+
|                    TELEGRAM AI ASSISTANT                           |
|                Multi-Agent Orchestrator System                     |
+------------------------------------------------------------------+
|                                                                    |
|  TELEGRAM                                                          |
|  +----------------+                                                |
|  | User Message   |--> Authentication --> Type Detection           |
|  +----------------+       (If1)            (Switch)                |
|                                                                    |
|  +------------------------------------------------------------+   |
|  |              INPUT PROCESSING LAYER                         |   |
|  |  +---------+  +--------------+  +----------------+         |   |
|  |  |  Text   |  |    Voice     |  |     Image      |         |   |
|  |  | Extract |  |  Download    |  |  Download      |         |   |
|  |  |         |  |  Transcribe  |  |  Analyze       |         |   |
|  |  |         |  |  (Whisper)   |  |  (Llama 4)     |         |   |
|  |  +----+----+  +------+-------+  +-------+--------+         |   |
|  |       +---------------+------------------+                  |   |
|  |                       |                                     |   |
|  |              Normalized Text Field                          |   |
|  +------------------------------------------------------------+   |
|                          |                                         |
|                          v                                         |
|  +------------------------------------------------------------+   |
|  |            ORCHESTRATOR AGENT                               |   |
|  |         (Groq Llama 3.3 70B Versatile)                      |   |
|  |                                                             |   |
|  |  +---------+  +-------------------------------+             |   |
|  |  |  Think  |  |   Buffer Memory (50 msgs)     |             |   |
|  |  |  Tool   |  |   Key: Telegram chat_id       |             |   |
|  |  +---------+  +-------------------------------+             |   |
|  |                                                             |   |
|  |  Connected Sub-Agents:                                      |   |
|  |  +----------+----------+----------+--------------+          |   |
|  |  | Email    | Calendar | Search   | Social Media |          |   |
|  |  | Agent    | Agent    | Agent    | Agent        |          |   |
|  |  +----+-----+----+-----+----+-----+------+-------+          |   |
|  +-------+----------+----------+-------------+-------------+   |
|          v          v          v             v                  |
|  +----------++----------++----------++----------++-------------+  |
|  |  Gmail   ||  Google  || SerpAPI  ||  Tavily  ||Google Sheets|  |
|  |  API     || Calendar || Wikipedia||  Search  ||  + Twitter  |  |
|  |          ||   API    || Hacker   ||   API    ||    API      |  |
|  |          ||          || News     ||          ||             |  |
|  +----------++----------++----------++----------++-------------+  |
|                          |                                      |
|                          v                                      |
|  +------------------------------------------------------------+|
|  |              OUTPUT ROUTING LAYER                           ||
|  |  +----------------+    +--------------------+               ||
|  |  | Voice Input?   |--->| Groq PlayAI TTS    |               ||
|  |  | YES = Audio    |    | then Telegram Voice |               ||
|  |  +----------------+    +--------------------+               ||
|  |  | Text or Image? |--->| Telegram Text      |               ||
|  |  | NO = Text      |    | (Markdown)         |               ||
|  |  +----------------+    +--------------------+               ||
|  +------------------------------------------------------------+|
|                                                                  |
+------------------------------------------------------------------+
```

### Agent Hierarchy

```
Orchestrator Agent (Parent)
|
+-- Email Agent (Sub-Agent)
|   +-- Send Email
|   +-- Reply to Email
|   +-- Delete Email
|   +-- Get Emails
|   +-- Mark as Read
|   +-- Mark as Unread
|
+-- Calendar Agent (Sub-Agent)
|   +-- Create Event
|   +-- Delete Event
|   +-- Get Event
|   +-- Get Many Events
|   +-- Update Event
|
+-- Search Agent (Sub-Agent)
|   +-- Google Search (SerpAPI)
|   +-- Tavily Search (AI-optimized)
|   +-- Wikipedia
|   +-- Hacker News
|
+-- Social Media Agent (Sub-Agent)
|   +-- Create Tweet (disabled)
|   +-- Save to Google Sheets
|
+-- Think Tool (Internal reasoning)
```

---

## Workflow Flow Diagram

```
START
  |
  v
+--------------------+
|  WhatsApp Trigger   | <-- Telegram Bot receives message
|  (Telegram)         |
+--------+-----------+
         |
         v
+--------------------+
|       If1           | <-- Check: Is sender authorized?
|  (Authentication)   |
+---+------------+---+
    |            |
  YES           NO --> (ignored)
    |
    v
+--------------------+
|      Switch         | <-- Detect message type
|  (Type Router)      |
+--+-------+-------+-+
   |       |       |
   v       v       v
 TEXT    VOICE   IMAGE
   |       |       |
   |       v       v
   |  +-------------+  +------------------+
   |  | Download URL |  | Download Image   |
   |  | Download     |  | URL              |
   |  | Audio        |  | Download Image   |
   |  | Transcribe   |  | Analyze image    |
   |  | (Groq        |  | (Groq Vision)    |
   |  | Whisper)     |  |                  |
   |  +------+------+  +--------+---------+
   |         |                   |
   v         v                   v
+------+  +------+         +----------+
| Text |  |Voice |         |Image+Text|
| (Set)|  |(Set) |         |  (Set)   |
+--+---+  +--+---+         +----+-----+
   |         |                   |
   +---------+-------------------+
                  |
                  v
       +--------------------+
       |   Orchestrator      | <-- Main AI Brain
       |      Agent          | <-- + Memory (50 msgs)
       | (Groq Llama 3.3)   | <-- + Think Tool
       |                     | <-- + 4 Sub-Agents
       +--------+-----------+
                |
                v
       +--------------------+
       |        If           | <-- Was original message voice?
       |  (Output Router)    |
       +---+------------+---+
           |            |
         YES           NO
           |            |
           v            v
       +--------+  +----------+
       |Generate |  |  Send    |
       | audio   |  | message1 |
       |(Groq    |  | (Text)   |
       | TTS)    |  +----------+
       +---+----+
           |
           v
       +--------+
       |  Send  |
       |message |
       |(Audio) |
       +--------+
           |
           v
         END
```

---

## Node-by-Node Reference

### Input Layer

| No | Node Name | Original Type | Modified Type | Purpose |
|----|-----------|---------------|---------------|---------|
| 1 | WhatsApp Trigger | WhatsApp Trigger | **Telegram Trigger** | Receives incoming Telegram messages |
| 2 | If1 | If (WhatsApp auth) | **If (Telegram auth)** | Validates sender by chat_id |
| 3 | Switch | Switch | Switch (updated paths) | Routes message to correct path |

### Text Processing Path

| No | Node Name | Type | Purpose |
|----|-----------|------|---------|
| 4 | Text | Set | Extracts message.text and normalizes to Text field |

### Voice Processing Path

| No | Node Name | Type | Purpose |
|----|-----------|------|---------|
| 5 | Download URL | HTTP Request | Calls Telegram getFile API for voice metadata |
| 6 | Download Audio | HTTP Request | Downloads voice file binary from Telegram |
| 7 | Transcribe a recording | HTTP Request to Groq | Sends audio to Groq Whisper for STT |
| 8 | Voice | Set | Normalizes transcribed text to Text field |

### Image Processing Path

| No | Node Name | Type | Purpose |
|----|-----------|------|---------|
| 9 | Download Image URL | HTTP Request | Gets photo file info from Telegram |
| 10 | Download Image | HTTP Request | Downloads the image binary |
| 11 | Analyze image | HTTP Request to Groq | Sends image to Groq Vision for analysis |
| 12 | Image + Text | Set | Combines image description with user caption |

### AI Processing Layer

| No | Node Name | Type | Purpose |
|----|-----------|------|---------|
| 13 | Orchestrator Agent | LangChain Agent | Main AI brain routes to sub-agents |
| 14 | GPT-4.1-mini | Groq LLM | Language model for Orchestrator |
| 15 | Simple Memory | Buffer Memory | Stores last 50 messages per user |
| 16 | Think | Think Tool | Internal reasoning tool |

### Sub-Agents

| No | Node Name | Type | Sub-Tools |
|----|-----------|------|-----------|
| 17 | E-Mails Agent1 | Agent Tool | Send / Reply / Delete / Get Many / Mark Read-Unread |
| 18 | Calendar Agent | Agent Tool | Create / Delete / Get / Get Many / Update events |
| 19 | Search Agent | Agent Tool | Google Search / Tavily Search / Wikipedia / Hacker News |
| 20 | Social Media Agent | Agent Tool | Create Tweet (disabled) / Save to Sheets |

### Output Layer

| No | Node Name | Type | Purpose |
|----|-----------|------|---------|
| 21 | If | If | Checks if original message was voice |
| 22 | Generate audio | HTTP Request to Groq | Converts text to speech using PlayAI TTS |
| 23 | Send message | Telegram | Sends audio reply to user |
| 24 | Send message1 | Telegram | Sends text reply with Markdown |

---

## AI Models Used (ALL FREE)

| Purpose | Model | Provider | Cost |
|---------|-------|----------|------|
| **Chat and Reasoning** | llama-3.3-70b-versatile | Groq | **FREE** |
| **Voice Transcription (STT)** | whisper-large-v3-turbo | Groq | **FREE** |
| **Voice Generation (TTS)** | playai-tts (Arista voice) | Groq | **FREE** |
| **Image Analysis (Vision)** | llama-4-scout-17b-16e-instruct | Groq | **FREE** |

### Groq Rate Limits (Free Tier)

| Model | Requests per min | Tokens per min | Tokens per day |
|-------|-----------------|----------------|----------------|
| Llama 3.3 70B | 30 | 6000 | 100000 |
| Whisper Large V3 | 20 | N/A | 2000 audio-seconds |
| PlayAI TTS | 10 | N/A | 10000 chars |
| Llama 4 Scout | 30 | 6000 | 100000 |

> **Tip:** For higher limits Groq offers paid plans starting at very affordable rates.

---

## Prerequisites and Credentials

### Required Accounts and API Keys

| No | Service | Purpose | How to Get |
|----|---------|---------|------------|
| 1 | **Telegram Bot** | Chat interface | @BotFather on Telegram then /newbot |
| 2 | **Groq API** | AI models (FREE) | console.groq.com |
| 3 | **Google Cloud** | Calendar + Gmail | console.cloud.google.com |
| 4 | **SerpAPI** | Google Search | serpapi.com (optional) |
| 5 | **Tavily** | AI-optimized Web Search | app.tavily.com (optional, alternative to SerpAPI) |
| 6 | **Google Sheets** | Save social posts | sheets.google.com |

### n8n Credentials to Create

| Credential Name | Type | Used By |
|----------------|------|---------|
| Telegram Bot API | Telegram API | Trigger and Send nodes |
| Groq API | Groq API | All 5 LLM nodes |
| Groq Header Auth | Header Auth | Whisper and TTS and Vision HTTP nodes |
| Google Calendar | OAuth2 | All Calendar tool nodes |
| Gmail | OAuth2 | All Gmail tool nodes |
| SerpAPI | API Key | Google Search node |
| Tavily API Key | Header Auth | Tavily Search node |
| Google Sheets | OAuth2 | x post node |

> Node names kept as GPT-4.1-mini for traceability but they actually use Groq Llama 3.3

---

## Quick Start Guide

### 5-Minute Setup

```
Step 1: Import the workflow
  Download workflow.json then n8n then Workflows then Import from File

Step 2: Create Telegram Bot
  Open Telegram then @BotFather then /newbot then Copy token

Step 3: Get Groq API Key
  Go to console.groq.com then API Keys then Create then Copy

Step 4: Configure n8n credentials
  Add: Telegram API and Groq API and Header Auth (for Groq)

Step 5: Update placeholders
  If1 node: Replace YOUR_TELEGRAM_CHAT_ID
  Calendar nodes: Replace YOUR_CALENDAR_EMAIL@gmail.com

Step 6: Activate and Test
  Toggle workflow ON then Send Hello to your bot
```

---

## Detailed Setup Instructions

### Step 1: Create Telegram Bot

```
1. Open Telegram app
2. Search for @BotFather
3. Send: /newbot
4. Enter bot name: My AI Assistant
5. Enter bot username: myai_helper_bot (must end with bot)
6. Copy the Bot Token
   Example: 7123456789:AAHxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### Step 2: Get Your Telegram Chat ID

```
1. Start a conversation with your new bot
2. Send any message (for example hello)
3. Open this URL in your browser:
   https://api.telegram.org/botYOUR_TOKEN/getUpdates
4. Find: chat id number
5. Copy the number (that is your chat_id)
6. Paste it in the If1 node (replace YOUR_TELEGRAM_CHAT_ID)
```

### Step 3: Get Groq API Key

```
1. Go to https://console.groq.com
2. Sign up with Google or GitHub
3. Navigate to: API Keys
4. Click: Create API Key
5. Copy the key
   Example: gsk_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

6. In n8n create TWO credentials:

   a) Groq API credential:
      Name: Groq API
      API Key: paste your key

   b) Header Auth credential:
      Name: Groq Header Auth
      Header Name: Authorization
      Header Value: Bearer gsk_xxxxxxxx
```

### Step 4: Google Cloud Setup (Calendar + Gmail)

```
1. Go to https://console.cloud.google.com
2. Create a new project: AI Assistant
3. Enable APIs:
   - Google Calendar API
   - Gmail API
   - Google Sheets API
4. Go to: Credentials then Create OAuth 2.0 Client
5. Download client credentials JSON

6. In n8n:
   - Create Google Calendar credential (OAuth2)
   - Create Gmail credential (OAuth2)
   - Create Google Sheets credential (OAuth2)
   - Authorize each one with your Google account

7. Replace YOUR_CALENDAR_EMAIL@gmail.com in these nodes:
   - Create an event
   - Delete an event
   - Get an event
   - Get Many Events
   - Update Events
```

### Step 5: SerpAPI Setup (Optional)

```
1. Go to https://serpapi.com
2. Sign up (free tier: 100 searches per month)
3. Copy API key
4. In n8n: Create SerpAPI credential with the key
```

### Step 5b: Tavily Search Setup (Optional — Alternative to SerpAPI)

```
1. Go to https://app.tavily.com
2. Sign up (free tier: 1,000 API credits/month, no credit card required)
3. Copy your API key (starts with tvly-)
4. In n8n: Create a Header Auth credential:
   Name: Tavily API Key
   Header Name: Authorization
   Header Value: Bearer tvly-YOUR_TAVILY_API_KEY
Note: Tavily can be used alongside or instead of SerpAPI for web searches.
```

### Step 6: Google Sheets Setup

```
1. Create a new Google Spreadsheet
2. Name it: X-Posts
3. Add headers in Row 1:
   Date | Theme | Posts
4. Copy the Sheet ID from the URL:
   https://docs.google.com/spreadsheets/d/THIS_IS_THE_ID/edit
5. Replace YOUR_GOOGLE_SHEET_ID_HERE in the x post node
```

### Step 7: Connect All Credentials in n8n

```
For each node click on it and select the correct credential:

Telegram nodes:     Telegram Bot API
GPT-4.1-mini nodes: Groq API
HTTP Request nodes:  Groq Header Auth (where applicable)
Calendar nodes:      Google Calendar OAuth
Gmail nodes:         Gmail OAuth
Google Sheets:       Google Sheets OAuth
SerpAPI:             SerpAPI credential
Tavily Search:       Tavily API Key (Header Auth)
```

### Step 8: Activate and Test

```
1. Click the Activate toggle (top-right)
2. Open Telegram and go to Your bot
3. Send: Hello!
4. You should receive an AI response!

Test all features:
- Text: What is on my calendar today?
- Voice: Send a voice message asking about weather
- Image: Send a photo and ask What is in this image?
```

---

## Usage Examples

### Email Management
```
You: Send an email to john@example.com about the project update
Bot: Email sent to john@example.com
     Subject: Project Update
     The email has been delivered successfully.

You: Show me my latest emails
Bot: Your latest emails:
     1. From: Sarah - Meeting Tomorrow (2 hours ago)
     2. From: GitHub - New PR Review (5 hours ago)
     3. From: AWS - Invoice Ready (1 day ago)

You: Reply to Sarah email and confirm the meeting
Bot: Reply sent to Sarah confirming the meeting.
```

### Calendar Management
```
You: Schedule a meeting with the team tomorrow at 3 PM
Bot: Event created:
     Title: Team Meeting
     Date: Tomorrow 3:00 PM - 4:00 PM
     Calendar: your@gmail.com

You: What do I have this week?
Bot: This week events:
     Mon 10 AM - Standup
     Tue 3 PM - Team Meeting (just created)
     Thu 2 PM - Client Call
     Fri 11 AM - Sprint Review

You: Cancel the client call on Thursday
Bot: Client Call on Thursday has been deleted.
```

### Web Search
```
You: What is the latest news about AI?
Bot: Latest AI News:
     1. Google announced Gemini 2.0 with enhanced reasoning
     2. Meta released Llama 4 with vision capabilities
     3. OpenAI launched GPT-5 preview
     Source: Hacker News and Google Search

You: Tell me about quantum computing
Bot: According to Wikipedia:
     Quantum computing uses quantum-mechanical phenomena
     such as superposition and entanglement to perform
     computations...
```

### Social Media
```
You: Create a tweet about the benefits of AI automation
Bot: Tweet created and saved:
     AI automation is not replacing jobs it is
     replacing tasks. The future belongs to those who
     learn to work WITH AI not against it.
     #AI #Automation #FutureOfWork
     Saved to Google Sheets for review.
```

### Image Analysis
```
You: [Send a photo of a restaurant menu]
Bot: I can see a restaurant menu with the following items:
     - Grilled Salmon: $24.99
     - Caesar Salad: $12.99
     - Pasta Carbonara: $18.99
     Would you like me to do anything with this information?
```

### Voice Interaction
```
You: [Voice message] Hey what meetings do I have today
     and can you send an email to my boss about being
     5 minutes late?

Bot: [Voice reply] You have 3 meetings today: a standup
     at 10 AM lunch with Dave at 12:30 and a review at
     3 PM. I have sent an email to your boss letting them
     know you will be 5 minutes late to the standup.
```

---

## Cost Comparison

### Before (WhatsApp + OpenAI)

| Service | Cost |
|---------|------|
| WhatsApp Business API | $0.005 - $0.08 per message |
| GPT-4.1-mini | $0.40 per 1M input tokens |
| OpenAI Whisper | $0.006 per minute |
| OpenAI TTS | $15.00 per 1M characters |
| GPT-4o-mini Vision | $0.15 per 1K image tokens |
| **Monthly estimate** | **$15 - $50+** |

### After (Telegram + Groq)

| Service | Cost |
|---------|------|
| Telegram Bot API | **FREE** |
| Groq Llama 3.3 70B | **FREE** |
| Groq Whisper | **FREE** |
| Groq PlayAI TTS | **FREE** |
| Groq Llama 4 Vision | **FREE** |
| **Monthly estimate** | **$0.00** |

> **Total savings: approximately 100%** This workflow costs absolutely nothing to run on Groq free tier!

---

## Troubleshooting

### Bot does not respond to messages

```
1. Check if workflow is activated (toggle ON)
2. Verify your chat_id in the If1 node
3. Check n8n execution logs for errors
4. Make sure Telegram webhook is properly set (check n8n logs)
5. Verify bot token is correct in credentials
```

### Voice messages fail

```
1. Verify Groq Header Auth credential is set correctly
2. Format: Bearer gsk_xxxxx (with Bearer prefix and space)
3. Check Groq rate limits (20 audio requests per minute on free tier)
4. Ensure the voice file is under 25MB
```

### Image analysis returns errors

```
1. Groq Vision expects base64 encoded images
2. Check if image download from Telegram succeeded
3. Verify the image is not too large (Telegram compresses photos)
4. Check Groq API status at status.groq.com
```

### Calendar or Email operations fail

```
1. Re-authorize Google OAuth credentials in n8n
2. Check if Calendar and Gmail APIs are enabled in Google Cloud
3. Verify the calendar email address is correct
4. Check Google OAuth consent screen is properly configured
```

### Rate limit exceeded errors

```
1. Groq free tier has request limits per minute
2. Wait 60 seconds and try again
3. Consider upgrading Groq plan for higher limits
4. Or add a rate-limiting mechanism to the workflow
```

---

## Security Considerations

| Aspect | Current | Recommendation |
|--------|---------|----------------|
| **Authentication** | chat_id check | Good - add multiple IDs for team use |
| **API Keys** | Stored in n8n credentials | Good - never hardcode in workflow |
| **Sensitive Actions** | No confirmation | Add confirmation before delete operations |
| **Data Privacy** | Groq processes data | Review Groq privacy policy |
| **Rate Limiting** | None | Consider adding debounce logic |

---

## Contributing

Contributions are welcome! Here is how you can help:

1. **Fork** the repository
2. **Create** a feature branch: git checkout -b feature/amazing-feature
3. **Commit** your changes: git commit -m Add amazing feature
4. **Push** to the branch: git push origin feature/amazing-feature
5. **Open** a Pull Request

### Ideas for Contributions
- Add support for document and PDF messages
- Add support for video messages
- Add location-based services
- Add multi-user support with database
- Add confirmation dialogs for destructive actions
- Add error handling with user-friendly messages
- Add Notion integration
- Add Slack or Discord support
- Add CRM integration

---

## License

This project is licensed under the MIT License. Feel free to use it for personal or commercial purposes.

---

<!-- ================================================================== -->
<!-- PROFESSIONAL SERVICES SECTION -->
<!-- ================================================================== -->

<div align="center">

## Professional Automation Services

---

### Need Custom AI Automation for Your Business?

<a href="https://yousefautomates.pages.dev/">
<img src="https://img.shields.io/badge/Hire_Yousef-Professional_Automation-FF6D5A?style=for-the-badge" alt="Hire Yousef" />
</a>

<br/><br/>

| Service | Description |
|---------|-------------|
| **Custom AI Assistants** | Tailored chatbots for Telegram and WhatsApp and Slack |
| **Business Automation** | End-to-end workflow automation with n8n |
| **System Integration** | Connect your tools: CRM and ERP and APIs |
| **Email Automation** | Smart email workflows and auto-responses |
| **Schedule Management** | Automated booking and calendar systems |
| **Data Pipelines** | Automated data collection and processing |
| **Social Media Bots** | Automated posting and engagement |
| **n8n Consulting** | Expert advice on workflow architecture |

<br/>

**Website:** [yousefautomates.pages.dev](https://yousefautomates.pages.dev/)

**Built with love by Yousef — AI Automation Expert**

---

</div>

<br/>
<br/>

<!-- ================================================================== -->
<!-- ARABIC DOCUMENTATION -->
<!-- ================================================================== -->

<a id="arabic-documentation"></a>

<div dir="rtl" align="right">

# التوثيق العربي

<div align="center">

> **مرحبا بك في التوثيق العربي الشامل لمشروع المساعد الشخصي الذكي عبر تلجرام**

</div>

---

## جدول المحتويات

- [نظرة عامة](#overview-ar)
- [المميزات الرئيسية](#features-ar)
- [البنية التقنية](#architecture-ar)
- [النماذج المستخدمة](#models-ar)
- [المتطلبات الاساسية](#requirements-ar)
- [دليل التشغيل السريع](#quickstart-ar)
- [شرح مفصل للاعداد](#setup-ar)
- [امثلة الاستخدام](#examples-ar)
- [مقارنة التكلفة](#cost-ar)
- [حل المشاكل](#troubleshooting-ar)
- [خدمات الاتمتة](#services-ar)

---

<a id="overview-ar"></a>
## نظرة عامة

هذا المشروع هو **وركفلو n8n جاهز للانتاج** يحول بوت تلجرام الى مساعد شخصي ذكي يعمل بالذكاء الاصطناعي. يستخدم **بنية Multi-Agent Orchestrator** حيث يوجد عقل مركزي ذكي يوجه طلباتك تلقائيا الى وكلاء متخصصين.

### ما الذي يميز هذا المشروع؟

| الميزة | الوصف |
|--------|-------|
| **ذكاء اصطناعي مجاني 100%** | جميع النماذج تعمل على Groq مجانا |
| **نظام متعدد الوكلاء** | 4 وكلاء متخصصين + 1 منسق رئيسي |
| **دعم الصوت** | ارسل رسالة صوتية ويرد لك صوتيا |
| **رؤية بالذكاء الاصطناعي** | ارسل صورة ويفهمها ويحللها |
| **ذاكرة** | يتذكر اخر 50 رسالة لكل مستخدم |
| **سريع جدا** | محرك Groq LPU يعطي استجابة اقل من ثانية |

---

<a id="features-ar"></a>
## المميزات الرئيسية

### معالجة مدخلات متعددة الانواع

| نوع الادخال | المعالجة |
|-------------|----------|
| رسالة نصية | معالجة مباشرة |
| رسالة صوتية | تحويل لنص عبر Groq Whisper ثم معالجة |
| صورة | تحليل عبر Groq Vision ثم معالجة |
| صورة مع تعليق | فهم مدمج للصورة والنص |

### توجيه ذكي للوكلاء

| الوكيل | الوظيفة | الادوات |
|--------|---------|---------|
| وكيل الايميل | ادارة البريد الالكتروني | ارسال ورد وحذف وقراءة |
| وكيل التقويم | ادارة المواعيد | انشاء وتعديل وحذف وعرض |
| وكيل البحث | البحث في الانترنت | جوجل وTavily وويكيبيديا واخبار |
| وكيل السوشيال | ادارة المحتوى | انشاء وحفظ تغريدات |
| اداة التفكير | التحليل والتقييم | تفكير داخلي قبل القرار |

### مخرجات ذكية

| المدخل الاصلي | نوع الرد |
|---------------|----------|
| رسالة صوتية | رد صوتي عبر Groq TTS |
| رسالة نصية | رد نصي بتنسيق Markdown |
| صورة | رد نصي مع تحليل الصورة |

---

<a id="architecture-ar"></a>
## البنية التقنية

### مخطط النظام

```
رسالة تلجرام واردة
        |
        v
   +-----------+
   | Telegram   |  يستقبل اي رسالة
   | Trigger    |
   +-----+-----+
         |
         v
   +-----------+     غير مصرح
   | التحقق من |-------------------> (تجاهل)
   | الهوية    |
   +-----+-----+
         | مصرح
         v
   +-----------+
   | تصنيف نوع |
   | الرسالة   |
   +--+--+--+--+
      |  |  |
   نص | صوت| صورة
      |  |  |
      v  v  v
    [معالجة كل نوع]
         |
         v
   +----------------+
   | المنسق الذكي   | العقل المركزي
   | (Llama 3.3)    | + ذاكرة 50 رسالة
   |                | + 4 وكلاء فرعيين
   +-------+--------+
           |
           v
   +-----------+
   | توجيه     |
   | المخرجات  |
   +--+-----+--+
      |     |
   صوت|   نص|
      v     v
   [ارسال الرد عبر تلجرام]
```

### هرمية الوكلاء

```
المنسق الرئيسي (Orchestrator)
|
+-- وكيل الايميل
|   +-- ارسال ايميل
|   +-- الرد على ايميل
|   +-- حذف ايميل
|   +-- جلب الايميلات
|   +-- تعليم كمقروء
|   +-- تعليم كغير مقروء
|
+-- وكيل التقويم
|   +-- انشاء حدث
|   +-- حذف حدث
|   +-- عرض حدث
|   +-- عرض احداث متعددة
|   +-- تعديل حدث
|
+-- وكيل البحث
|   +-- بحث جوجل
|   +-- بحث Tavily
|   +-- ويكيبيديا
|   +-- اخبار هاكر نيوز
|
+-- وكيل السوشيال ميديا
|   +-- انشاء تغريدة (معطل حاليا)
|   +-- حفظ في Google Sheets
|
+-- اداة التفكير
```

---

<a id="models-ar"></a>
## النماذج المستخدمة (مجانية بالكامل)

| الوظيفة | النموذج | المزود | التكلفة |
|---------|---------|--------|---------|
| المحادثة والتفكير | llama-3.3-70b-versatile | Groq | **مجاني** |
| تحويل الصوت لنص | whisper-large-v3-turbo | Groq | **مجاني** |
| تحويل النص لصوت | playai-tts | Groq | **مجاني** |
| تحليل الصور | llama-4-scout-17b-16e-instruct | Groq | **مجاني** |

---

<a id="requirements-ar"></a>
## المتطلبات الاساسية

### الحسابات المطلوبة

| الرقم | الخدمة | الغرض | كيفية الحصول |
|-------|--------|-------|-------------|
| 1 | **بوت تلجرام** | واجهة المحادثة | BotFather في تلجرام |
| 2 | **مفتاح Groq** | نماذج الذكاء الاصطناعي | console.groq.com مجاني |
| 3 | **Google Cloud** | التقويم والايميل | console.cloud.google.com |
| 4 | **SerpAPI** | بحث جوجل | serpapi.com اختياري |
| 5 | **Tavily** | بحث ويب محسن بالذكاء الاصطناعي | app.tavily.com اختياري بديل ل SerpAPI |
| 6 | **Google Sheets** | حفظ البوستات | sheets.google.com |

---

<a id="quickstart-ar"></a>
## دليل التشغيل السريع

### الاعداد في 5 دقائق

```
الخطوة 1: استيراد الوركفلو
   حمل ملف workflow.json
   في n8n: Workflows ثم Import from File

الخطوة 2: انشاء بوت تلجرام
   افتح تلجرام ثم ابحث عن BotFather
   ارسل /newbot ثم اختر اسم ثم انسخ التوكن

الخطوة 3: الحصول على مفتاح Groq
   اذهب ل console.groq.com
   سجل دخول ثم API Keys ثم انشاء مفتاح

الخطوة 4: اعداد بيانات الاعتماد في n8n
   اضف: Telegram API و Groq API و Header Auth

الخطوة 5: تحديث القيم
   If1: ضع chat_id الخاص بك
   Calendar: ضع بريدك الالكتروني

الخطوة 6: التفعيل والاختبار
   فعل الوركفلو ثم ارسل مرحبا للبوت
```

---

<a id="setup-ar"></a>
## شرح مفصل للاعداد

### الخطوة 1: انشاء بوت تلجرام

```
1. افتح تطبيق تلجرام
2. ابحث عن BotFather
3. ارسل: /newbot
4. ادخل اسم البوت: مساعدي الذكي
5. ادخل اسم المستخدم: my_ai_helper_bot
   (لازم ينتهي بكلمة bot)
6. انسخ التوكن
   مثال: 7123456789:AAHxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### الخطوة 2: الحصول على Chat ID

```
1. افتح محادثة مع البوت الجديد
2. ارسل اي رسالة مثلا: اهلا
3. افتح هذا الرابط في المتصفح:
   https://api.telegram.org/botالتوكن/getUpdates
4. ابحث عن: chat id ثم الرقم
5. انسخ الرقم هذا هو chat_id
6. ضعه في نود If1 بدل YOUR_TELEGRAM_CHAT_ID
```

### الخطوة 3: الحصول على مفتاح Groq

```
1. اذهب ل https://console.groq.com
2. سجل بحساب Google او GitHub
3. اذهب ل: API Keys
4. اضغط: Create API Key
5. انسخ المفتاح
   مثال: gsk_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

6. في n8n انشئ بيانات اعتماد:

   ا) Groq API:
      الاسم: Groq API
      المفتاح: الصق المفتاح

   ب) Header Auth:
      الاسم: Groq Header Auth
      اسم ال Header: Authorization
      القيمة: Bearer gsk_xxxxxxxx
```

### الخطوة 4: اعداد Google Cloud

```
1. اذهب ل https://console.cloud.google.com
2. انشئ مشروع جديد: AI Assistant
3. فعل ال APIs:
   - Google Calendar API
   - Gmail API
   - Google Sheets API
4. انشئ OAuth 2.0 credentials
5. في n8n: انشئ بيانات اعتماد لكل خدمة
6. استبدل YOUR_CALENDAR_EMAIL@gmail.com ببريدك
```

### الخطوة 5: التفعيل والاختبار

```
1. اضغط زر Activate اعلى اليمين
2. افتح تلجرام ثم البوت الخاص بك
3. ارسل: مرحبا!
4. المفروض تستلم رد ذكي!

اختبر كل الميزات:
- نص: ايه المواعيد اللي عندي بكرة؟
- صوت: ارسل رسالة صوتية
- صورة: ارسل صورة واسال ايه اللي في الصورة دي؟
```

---

<a id="examples-ar"></a>
## امثلة الاستخدام

### ادارة الايميلات
```
انت: ابعت ايميل لاحمد عن اجتماع بكرة
البوت: تم ارسال الايميل لاحمد
       الموضوع: اجتماع الغد
       تم التسليم بنجاح.

انت: وريني اخر الايميلات
البوت: اخر ايميلاتك:
       1. من: سارة - اجتماع الغد (قبل ساعتين)
       2. من: GitHub - مراجعة PR (قبل 5 ساعات)
       3. من: AWS - الفاتورة جاهزة (امبارح)
```

### ادارة المواعيد
```
انت: حدد ميتنج مع الفريق بكرة الساعة 3
البوت: تم انشاء الحدث:
       العنوان: اجتماع الفريق
       الموعد: بكرة 3:00 م - 4:00 م

انت: ايه المواعيد اللي عندي الاسبوع ده؟
البوت: احداث هذا الاسبوع:
       الاثنين 10 ص - Standup
       الثلاثاء 3 م - اجتماع الفريق
       الخميس 2 م - مكالمة عميل
       الجمعة 11 ص - مراجعة Sprint
```

### البحث في الانترنت
```
انت: ابحث عن اخر اخبار الذكاء الاصطناعي
البوت: اخر اخبار ال AI:
       1. جوجل اعلنت عن Gemini 2.0
       2. Meta اصدرت Llama 4
       المصدر: Hacker News وبحث جوجل
```

### التفاعل الصوتي
```
انت: [رسالة صوتية] ايه المواعيد اللي عندي النهاردة؟
البوت: [رد صوتي] عندك 3 مواعيد النهاردة: ستاند اب
       الساعة 10 الصبح وغدا مع احمد الساعة 12:30
       ومراجعة الساعة 3 بعد الظهر.
```

---

<a id="cost-ar"></a>
## مقارنة التكلفة

### قبل (WhatsApp + OpenAI)

| الخدمة | التكلفة |
|--------|---------|
| WhatsApp Business API | $0.005 - $0.08 لكل رسالة |
| GPT-4.1-mini | $0.40 لكل مليون توكن |
| OpenAI Whisper | $0.006 لكل دقيقة |
| OpenAI TTS | $15.00 لكل مليون حرف |
| **التقدير الشهري** | **$15 - $50+** |

### بعد (Telegram + Groq)

| الخدمة | التكلفة |
|--------|---------|
| Telegram Bot API | **مجاني** |
| Groq Llama 3.3 70B | **مجاني** |
| Groq Whisper | **مجاني** |
| Groq PlayAI TTS | **مجاني** |
| Groq Vision | **مجاني** |
| **التقدير الشهري** | **$0.00** |

> **التوفير: حوالي 100%** هذا الوركفلو ما بيكلفش حاجة خالص على Groq المجاني!

---

<a id="troubleshooting-ar"></a>
## حل المشاكل

| المشكلة | الحل |
|---------|------|
| البوت مش بيرد | تاكد ان الوركفلو مفعل وان chat_id صحيح |
| الرسائل الصوتية فاشلة | تاكد من Header Auth يبدا ب Bearer gsk |
| تحليل الصور مش شغال | تاكد ان الصورة مش كبيرة اوي |
| التقويم او الايميل مش شغال | اعد تفعيل Google OAuth |
| خطا Rate Limit | استنى دقيقة وحاول تاني |

---

<a id="services-ar"></a>

</div>

<!-- ================================================================== -->
<!-- FINAL SECTION - SHARED -->
<!-- ================================================================== -->

<div align="center">

---

## خدمات الاتمتة الاحترافية | Professional Automation Services

---

<a href="https://yousefautomates.pages.dev/">
<img src="https://img.shields.io/badge/Yousef_Automates-Professional_AI_and_Automation_Services-FF6D5A?style=for-the-badge" alt="Yousef Automates" />
</a>

<br/><br/>

### هل تحتاج اتمتة مخصصة لعملك؟ | Need Custom Automation?

<table>
<tr>
<td align="center" width="50%">

**English Services**

| Service | Description |
|---------|-------------|
| Custom AI Assistants | Telegram and WhatsApp and Slack |
| Business Automation | End-to-end n8n workflows |
| System Integration | CRM and ERP and APIs |
| Email Automation | Smart workflows |
| Schedule Management | Booking systems |
| Data Pipelines | Collection and processing |
| Social Media Bots | Auto posting |
| n8n Consulting | Architecture advice |

</td>
<td align="center" width="50%">

**الخدمات العربية**

| الخدمة | الوصف |
|--------|-------|
| مساعدين ذكيين مخصصين | تلجرام وواتساب وسلاك |
| اتمتة الاعمال | وركفلو n8n شاملة |
| ربط الانظمة | CRM و ERP و APIs |
| اتمتة الايميلات | وركفلو ذكية |
| ادارة المواعيد | انظمة حجز |
| معالجة البيانات | جمع ومعالجة |
| بوتات سوشيال ميديا | نشر تلقائي |
| استشارات n8n | تصميم البنية |

</td>
</tr>
</table>

<br/>

### [yousefautomates.pages.dev](https://yousefautomates.pages.dev/)

<br/>

---

### Star this repo if you found it useful!

**Built with love by Yousef — Senior AI Automation Expert**

<br/>

*Keywords: n8n workflow, telegram bot, ai assistant, groq, llama, whisper, multi-agent, orchestrator, automation, free ai, voice assistant, chatbot, personal assistant, email automation, calendar automation, langchain, no-code, low-code*

</div>
