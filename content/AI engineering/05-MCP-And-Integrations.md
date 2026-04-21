# MCP & Integrations 

*How AI connects to the outside world!*

---

## What is MCP? (Model Context Protocol)

**MCP** is a new standard that lets AI connect to **anything** - files, tools, databases, APIs.

### Simple Analogy

Think of AI as a **smart assistant** who can now use **any tool** in the world:

| Before MCP | After MCP |
|-----------|-----------|
| AI can only do what it's programmed to do | AI can use ANY tool you connect |
| Separate integration for each tool | One protocol connects everything |
| Hard to build | Easy to build |

---

## Why MCP Matters

### The Problem Before MCP

Before MCP, connecting AI to tools was like:

```
Each tool needed a custom translator:
AI ←→ Google Search (custom code)
AI ←→ Your Files (custom code)
AI ←→ Slack (custom code)
AI ←→ Database (custom code)

Too much custom work! 😫
```

### The MCP Solution

```
AI ←→ MCP ←→ Any Tool!

Google Search ←→ MCP
Your Files ←→ MCP
Slack ←→ MCP
Database ←→ MCP

One connection! 🎉
```

---

## How MCP Works

### Architecture

```
┌─────────────────────────────────────────┐
│              Your AI App                │
│              (Client)                    │
└──────────────────┬──────────────────────┘
                   │
                   │ MCP Protocol
                   │
┌──────────────────┴──────────────────────┐
│            MCP Server                    │
│    (The Bridge / Connection Manager)    │
└──────────────────┬──────────────────────┘
                   │
     ┌─────────────┼─────────────┐
     ↓             ↓             ↓
┌────────┐   ┌────────┐   ┌────────┐
│ Google  │   │ Files  │   │ Slack  │
│  Search │   │  System│   │        │
└────────┘   └────────┘   └────────┘
```

### What's a Server?

In this context, a server is a **connection hub** that:

- Holds the tools/resources
- Handles the communication
- Manages permissions

---

## What Can MCP Connect?

### 1. File Systems 📁
- Read/write files on your computer
- Search through documents
- Access code repositories

### 2. Web & APIs 🌐
- Search the internet
- Access APIs (weather, stocks, etc.)
- Fetch data from websites

### 3. Developer Tools 💻
- Git repositories
- Code execution
- Database queries

### 4. Communication 📱
- Email
- Slack
- Discord

### 5. Data & Databases 📊
- SQL databases
- Spreadsheets
- Knowledge bases

---

## What is an Integration?

An **integration** connects two services so they can **work together**.

### Examples of Integrations

| Services | What It Does |
|----------|-------------|
| Slack + AI | Chat with AI in Slack |
| Gmail + AI | AI writes your emails |
| Notion + AI | AI edits your notes |
| Figma + AI | AI generates designs |
| YouTube + AI | AI writes descriptions |

---

## Popular Integrations

### AI + Communication

**Slack AI**
- AI summarizes conversations
- Answers questions about past messages

**Discord AI**
- AI moderator
- Chat with AI in channels

### AI + Productivity

**Notion AI**
- Write & edit notes
- Auto-complete

**Google Workspace AI**
- Smart compose in Gmail
- AI in Google Docs

### AI + Content

**Adobe Firefly**
- AI image generation
- AI text effects

**Canva AI**
- AI design suggestions
- Magic resize

---

## What is an API Key? 🔑

An API key is like a **password** that lets your app connect to a service.

### Why Do You Need One?

- Identifies who is using the service
- Tracks usage (and charges if paid)
- Keeps bad actors out

### How to Get One

```
1. Go to service website (e.g., OpenAI)
2. Create account
3. Go to API section
4. Generate new key
5. Copy and use in your app
```

### ⚠️ Important Rules
- **Never share** your API key
- **Never put** it in public code
- **Keep it safe** (use .env files)

---

## Webhooks

A webhook is when one app **automatically tells** another app something happened.

### Simple Example

```
GitHub webhook:
When I push code → Tell my CI/CD system → Auto-deploy!

Slack webhook:
When someone fills form → Send message to Slack channel
```

### With AI

```
User asks question → AI webhook → Gets answer → Replies!
```

---

## What is a Function Call?

A function call is when AI **uses a tool** to get something done.

### How It Works

```
1. You ask: "What's the weather in Tokyo?"
2. AI thinks: "I need to call a weather function"
3. AI calls: weather_function(location="Tokyo")
4. Result: "72°F, sunny"
5. AI answers: "It's sunny and 72°F in Tokyo!"
```

### Why Use It?

- Get **real-time** information
- Do **accurate** calculations
- Access **external** data

---

## What is an SDK? 🛠️

SDK = **Software Development Kit**

Think of it as a **kit** with all the tools to build something.

### What's in an SDK?

- Code libraries
- Documentation
- Examples
- Testing tools

### Example

**OpenAI SDK** for Python:
```python
from openai import OpenAI

client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Hello!"}]
)
```

---

## Quick Reference 📋

| Term | Simple Meaning |
|------|----------------|
| **MCP** | Standard way for AI to connect to tools |
| **Integration** | Connection between two services |
| **API Key** | Password for connecting to services |
| **Webhook** | Auto-notification when something happens |
| **Function Call** | AI using a specific tool |
| **SDK** | Toolkit for building with a service |

---

## Next Steps

➡️ **[06-Memory-And-Knowledge.md](06-Memory-And-Knowledge.md)** - Learn how AI stores knowledge!

---

*MCP makes AI infinitely more powerful! 🔌*