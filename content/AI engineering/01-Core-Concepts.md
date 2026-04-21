# AI Core Concepts 🧠

*Simple explanations for fundamental AI terms - no tech jargon!*

---

## What is an LLM? (Large Language Model)

Think of an LLM as a **super smart parrot** that has read millions of books 📚

It doesn't truly "think" like a human. Instead, it:

- **Reads** tons of text from the internet
- **Learns** patterns in how words fit together
- **Predicts** what word comes next

### Simple Example
When you type: *"The sky is..."*

The LLM predicts: *"blue"* because it's seen that pattern millions of times.

---

## What is a Model?

A "model" is just the **software program** that does the AI thinking.

It's like different versions of a person:

| Model | Personality | Best At |
|-------|-------------|---------|
| GPT-4 (OpenAI) | Professional & smart | Writing, coding, analysis |
| Claude (Anthropic) | Helpful & ethical | Long conversations, nuanced topics |
| Gemini (Google) | Research-focused | Multi-modal, images & video |
| Llama (Meta) | Open & free | Running on your own computer |

---

## What is a Token? 🪙

A token is the **smallest piece of text** the AI can read.

Think of tokens like LEGO blocks:

```
"Hello world" = 2-3 tokens (roughly)
```

### Why Should You Care?

- **AI pricing is based on tokens** (like paying per word)
- More tokens = more expensive
- Token limit = how much the AI can "remember" in one conversation

### Quick Numbers
- 1 token ≈ 1 word (in English)
- 1,000 tokens ≈ 750 words
- A typical email = 50-100 tokens

---

## What is an API? 🔌

API stands for **Application Programming Interface** - but just think of it as:

> **A connector that lets two programs talk to each other**

### Simple Analogy
Your phone charger has a specific plug (USB-C, Lightning, etc.)

An API is like that plug - it's the **standard way** for your app to connect to AI.

### In Practice
When you use an AI tool, here's what happens:

```
Your App → API → AI Model → Response → Your App
```

You don't need to code - the tool handles the connection!

---

## What is a Prompt?

A prompt is simply **what you say to the AI** - your question or instruction.

### Types of Prompts

**1. Simple Prompt**
```
"What is Python?"
```

**2. Instructional Prompt**
```
"Explain like I'm 5 years old what Python is"
```

**3. Role-Playing Prompt**
```
"You are a grumpy pirate. Explain what Python is."
```

**4. Detailed Prompt**
```
"Write a 2-minute YouTube script about Python for beginners. 
Include: 
- A funny hook
- 3 key points
- A call to action"
```

---

## What is Temperature? 🌡️

Temperature controls **how creative vs. predictable** the AI is.

Think of it like a dial:

| Temperature | What It Does | Best For |
|-------------|--------------|----------|
| 0.0 (Cold) | Always picks most likely word | Facts, code, math |
| 0.5 (Cool) | Mostly predictable,偶尔创意 | General writing |
| 0.7 (Warm) | Balanced | Creative writing |
| 1.0 (Hot) | Random & crazy | Art, brainstorming |

### Example
```
Cold (0.0): "The capital of France is Paris"
Warm (0.7): "Paris - the romantic capital of France..."
Hot (1.0): "Paris! The city of love, lights, croissants... [goes off rails]"
```

---

## What is Context Window?

The context window is **how much the AI can "see" at once**.

It's like short-term memory:

- GPT-4: Can see ~8,000 to 128,000 words at once
- Claude: Can see up to 200,000 words
- Gemini: Can see up to 1 million words!

### Why It Matters
If your conversation gets too long, the AI "forgets" earlier parts.

**Solution:** Start a new chat when needed!

---

## Quick Reference Card 📋

| Term | Simple Definition |
|------|-------------------|
| **LLM** | Super smart text predictor |
| **Model** | The AI program version |
| **Token** | A word/piece of text |
| **API** | Connection between apps |
| **Prompt** | Your question to AI |
| **Temperature** | Creativity level |
| **Context** | What AI remembers |

---

## Next Steps

➡️ **[02-Prompting-Basics.md](02-Prompting-Basics.md)** - Learn how to write better prompts!

---

*Super simple. No jargon. Just learning! 🚀*
