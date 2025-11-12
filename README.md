# 🤖 n8n AI Agent Flow — Chat + Memory + Wikipedia

This workflow implements a conversational AI Agent inside **n8n** that can respond to user prompts using either **OpenAI Chat models** (GPT-4, GPT-4o-mini) or **Google Gemini Chat models**.  
It also integrates **memory persistence** and retrieves verified information exclusively from **Wikipedia**.

---

## 🧠 Features

- 🔹 **AI Agent Module** — enables multi-turn conversations with context retention.  
- 🔹 **Dual Model Support** — switch between OpenAI or Google Gemini seamlessly.  
- 🔹 **Memory Node** — stores previous user interactions for contextual answers.  
- 🔹 **Wikipedia Query Node** — fetches real data only from Wikipedia.  
- 🔹 **Flexible Input** — accepts text chat messages via webhook or form input.

---

## 🧩 Workflow Overview

[Webhook / Input Node]
↓
[AI Agent Module]
↓
[Memory Node (Store / Retrieve)]
↓
[Wikipedia API Node]
↓
[AI Model Node → OpenAI or Gemini]
↓
[Response Output (Discord / Webhook / Console)]

- The workflow starts when a message is received.  
- The AI Agent passes the message to the selected model.  
- The Memory Node keeps track of the ongoing conversation.  
- Before responding, the agent queries **Wikipedia** to verify factual context.  
- The reply is returned with updated memory.

---

## ⚙️ Configuration

### 1. Environment Variables
Set up your credentials in n8n:

| Variable | Description |
|-----------|--------------|
| `OPENAI_API_KEY` | OpenAI API key (if using GPT models) |
| `GOOGLE_API_KEY` | Google Gemini API key |
| `WIKI_API_URL` | Wikipedia endpoint (default: `https://en.wikipedia.org/api/rest_v1/page/summary/`) |

---

### 2. Model Selection
You can switch the active model through a variable or node parameter:
- `model_provider = "openai"` → Uses OpenAI Chat Model  
- `model_provider = "gemini"` → Uses Google Gemini Chat Model

---

### 3. Memory Configuration
The **Memory Node** should:
- Save `user_message`, `assistant_reply`, and `timestamp`.
- Retrieve the last few exchanges to maintain context (e.g. last 5 messages).

You can use a database node (PostgreSQL, SQLite) or n8n’s built-in memory module.

---

### 4. Wikipedia Node
- Input: user query or topic extracted from the chat message.
- Output: short summary text from Wikipedia API.
- Ensure it filters out any sources beyond Wikipedia for factual grounding.

---

## 🚀 Running the Flow

1. Import the `.json` workflow file into your n8n instance.  
2. Configure the model credentials under **Credentials → AI Models**.  
3. (Optional) Adjust memory persistence if using an external DB.  
4. Activate the workflow and send a message through the input channel.  

---

## 🧩 Example Query

> User: “Tell me about quantum computing.”

**Flow:**
1. Memory Node checks context.  
2. Wikipedia Node fetches verified summary.  
3. AI Model reformulates the answer conversationally.  
4. Response: “Quantum computing is a field of study that uses quantum mechanics to process information…”  

---

## ❤️ Made with love by Anselmo

