# ============================================================
# 🚀 SETUP GUIDE - Telegram AI Personal Assistant
# ============================================================
# Built by Yousef | https://yousefautomates.pages.dev/
# ============================================================

## STEP 1: Create Telegram Bot
# ---------------------------------------------------------------
# 1. Open Telegram and search for @BotFather
# 2. Send /newbot
# 3. Choose a name (e.g., "My AI Assistant")
# 4. Choose a username (e.g., "myai_assistant_bot")
# 5. Copy the Bot Token (looks like: 123456789:ABCdefGHIjklMNOpqrsTUVwxyz)
# 6. In n8n: Create "Telegram API" credential with this token

## STEP 2: Get Your Telegram Chat ID
# ---------------------------------------------------------------
# 1. Start a chat with your new bot
# 2. Send any message (e.g., "hello")
# 3. Open: https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates
# 4. Find "chat":{"id": YOUR_CHAT_ID}
# 5. Replace YOUR_TELEGRAM_CHAT_ID in the If1 node with this number

## STEP 3: Get Groq API Key (FREE)
# ---------------------------------------------------------------
# 1. Go to https://console.groq.com
# 2. Sign up / Sign in
# 3. Go to API Keys → Create API Key
# 4. Copy the key
# 5. In n8n: Create "Groq API" credential with this key
# 6. In n8n: Create "Header Auth" credential:
#    - Header Name: Authorization
#    - Header Value: Bearer YOUR_GROQ_API_KEY

## STEP 4: Google Calendar & Gmail
# ---------------------------------------------------------------
# 1. Go to Google Cloud Console → Create Project
# 2. Enable Calendar API and Gmail API
# 3. Create OAuth 2.0 credentials
# 4. In n8n: Create Google Calendar and Gmail credentials
# 5. Replace YOUR_CALENDAR_EMAIL@gmail.com in all Calendar nodes

## STEP 5: SerpAPI (for Google Search - Optional)
# ---------------------------------------------------------------
# 1. Go to https://serpapi.com
# 2. Sign up (free tier available)
# 3. Copy API key
# 4. In n8n: Create SerpAPI credential

## STEP 5b: Tavily Search (Alternative/Fallback Search - Optional)
# ---------------------------------------------------------------
# 1. Go to https://app.tavily.com
# 2. Sign up (free tier: 1,000 API credits/month, no credit card required)
# 3. Copy your API key (starts with tvly-)
# 4. In n8n: Create "Header Auth" credential:
#    - Name: Tavily API Key
#    - Header Name: Authorization
#    - Header Value: Bearer tvly-YOUR_TAVILY_API_KEY
# Note: Tavily provides AI-optimized search results and can be used
#       alongside or as a fallback to SerpAPI.

## STEP 6: Google Sheets (for Social Media posts)
# ---------------------------------------------------------------
# 1. Create a new Google Sheet named "X-Posts"
# 2. Add columns: Date | Theme | Posts
# 3. Copy the Sheet ID from the URL
# 4. Replace YOUR_GOOGLE_SHEET_ID_HERE in the "x post" node

## STEP 7: Import & Activate
# ---------------------------------------------------------------
# 1. In n8n: Go to Workflows → Import from File
# 2. Select the workflow.json file
# 3. Connect all credentials to their respective nodes
# 4. Click "Activate" toggle
# 5. Send a message to your Telegram bot!

# ============================================================
# 📊 FREE Models Used (via Groq):
# ============================================================
# - Chat/Reasoning: llama-3.3-70b-versatile
# - Voice STT:      whisper-large-v3-turbo
# - Voice TTS:      playai-tts (Arista-PlayAI voice)
# - Vision:         meta-llama/llama-4-scout-17b-16e-instruct
#
# All models are FREE on Groq with generous rate limits!
# ============================================================

# ============================================================
# 🔗 Need Professional Automation Services?
# Contact: https://yousefautomates.pages.dev/
# ============================================================
