# Memory & Knowledge 🧠

*How AI remembers and learns!*

---

## The Memory Problem

AI models are like **goldfish** - they have short memories!

- They train on data from the past
- They don't know what happened after training
- They "forget" when you start a new conversation

### The Solution

**Give AI external memory!**

---

## Types of Memory

### 1. Short-Term Memory (Conversation Context)

What's currently in the chat

```
Chat: "My name is Sarah"
AI: "Hi Sarah!"
```

**Limit:** Depends on context window (usually thousands of words)

### 2. Long-Term Memory (Across Chats)

Remembering things **between sessions**

```
Chat 1: "My favorite color is blue"
Chat 2: "Remember my favorite color?" 
AI: "Blue!"
```

### 3. Entity Memory (Facts About You)

```
Name: Sarah
Role: Developer
Projects: Website, App
Preferences: Short responses
```

---

## What is RAG? 📚

**RAG** = **Retrieval Augmented Generation**

Think of it as giving AI a **reference book** before answering.

### How RAG Works

```
1. You have documents (PDFs, articles, etc.)
2. Convert to "vectors" (math representations)
3. Store in a database
4. When question asked → Find relevant info → Feed to AI
5. AI answers based on that info
```

### Simple Example

**Without RAG:**
```
You: "What does our employee handbook say about vacation?"
AI: "I don't have access to your handbook"
```

**With RAG:**
```
1. Handbook uploaded & stored
2. You ask about vacation
3. System finds handbook section about vacation
4. Feeds that to AI
5. AI answers: "According to your handbook..."
```

---

## What are Embeddings? 🔢

Embeddings are how AI **understands meaning** - converting text to numbers.

### Simple Explanation

| Text | "Meaning Numbers" |
|------|-------------------|
| "cat" | [0.1, 0.8, 0.3, ...] |
| "kitten" | [0.1, 0.79, 0.31, ...] |
| "dog" | [0.7, 0.2, 0.1, ...] |

**Cat and kitten have similar numbers!**
**Cat and dog have different numbers!**

### Why Does This Matter?

- Find **similar** concepts
- Search by **meaning**, not just keywords
- Power recommendation systems

---

## What is a Vector Database?

A vector database stores embeddings for **fast similarity search**.

### Traditional Search
```
Search: "buy phone"
Finds: Contains exact words "buy" and "phone"
```

### Vector Search
```
Search: "buy phone"
Finds: "purchase a mobile device", "get a smartphone"
(Things with similar MEANING)
```

---

## What is Fine-Tuning? 🎓

Fine-tuning is **teaching** a model your specific knowledge.

### Analogy

| Pre-trained Model | Fine-Tuning |
|-------------------|-------------|
| Knows general things | Learns your specific things |
| Like a fresh graduate | Like an employee trained by you |

### When to Fine-Tune

- Need specific format (legal documents)
- Special vocabulary (medical, technical)
- Custom tone (your brand voice)
- Prompting isn't working well enough

---

## What is Training? 📖

Training is how AI models **learn** from data.

### How It Works

```
1. Show millions of examples
2. Model learns patterns
3. Adjust internal "weights"
4. Gets better at predicting
```

### Types of Training

| Type | What It Is | When |
|------|-----------|------|
| Pre-training | Learn general knowledge | Initial model creation |
| Fine-tuning | Learn specific knowledge | Customize model |
| RLHF | Learn from human feedback | Improve responses |

---

## What is RLHF? 👥

**RLHF** = **Reinforcement Learning from Human Feedback**

It's like **teaching by showing** what's good vs. bad:

```
1. AI gives answer
2. Human rates it (good/bad)
3. AI learns from ratings
4. Gets better over time
```

This is what makes ChatGPT and Claude so good at following instructions!

---

## What is a Knowledge Base?

A knowledge base is a **central place** where information is stored.

### Types

| Type | Example |
|------|---------|
| Documents | PDFs, Word files, Notion pages |
| Database | Customer info, product data |
| Web | Wikipedia, company website |
| Q&A | FAQ, help articles |

---

## Building a Knowledge System

### Simple Flow

```
Documents → Split into chunks → Convert to vectors → Store in database
                                                        ↓
User Question → Convert to vector → Find similar → Feed to AI → Answer
```

### Tools for This

| Tool | What It Does |
|------|-------------|
| LangChain | Build the pipeline |
| Pinecone | Vector database (cloud) |
| Chroma | Vector database (local) |
| Weaviate | Open source vector DB |
| LlamaIndex | Another framework |

---

## What are System Instructions?

System instructions are **hidden rules** that shape AI behavior.

### How It Works

```
System: "You are a helpful assistant that always speaks in French"

User: "Hello"
AI: "Bonjour!"  (responds in French!)
```

### Examples

```
"You are a pirate. Speak like a pirate."
"You are a Python expert. Give code examples."
"You are concise. Keep answers under 3 sentences."
```

---

## Quick Reference 📋

| Term | Simple Meaning |
|------|----------------|
| **RAG** | Giving AI reference material |
| **Embeddings** | Converting text to numbers |
| **Vector Database** | Fast search for similar meaning |
| **Fine-tuning** | Teaching AI your specific knowledge |
| **Training** | How AI learns from data |
| **RLHF** | Learning from human ratings |
| **Knowledge Base** | Central place for information |

---

## Next Steps

➡️ **[07-Quality-And-Safety.md](07-Quality-And-Safety.md)** - Learn about AI safety!

---

*AI can now remember and learn! 📚*