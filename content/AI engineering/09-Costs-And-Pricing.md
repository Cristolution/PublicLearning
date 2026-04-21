# Costs & Pricing 💰

*Understanding AI costs without the headache!*

---

## How AI Pricing Works

AI pricing is usually based on **tokens** (words) processed.

### The Basic Formula

```
Cost = Input Tokens × Input Price + Output Tokens × Output Price
```

### Think of It Like

```
Input: Sending a letter (you write)
Output: Receiving a response (AI writes)
```

---

## Common Pricing Models

### Per 1,000 Tokens

| Model | Input (per 1K) | Output (per 1K) |
|-------|----------------|-----------------|
| GPT-4o | $0.005 | $0.015 |
| GPT-4 | $0.03 | $0.06 |
| GPT-3.5 Turbo | $0.001 | $0.002 |
| Claude 3.5 | $0.003 | $0.015 |

### Example Costs

```
Short email (50 tokens in, 100 out):
- GPT-3.5: $0.00025 (almost free!)
- GPT-4: $0.0075 (less than a cent)

Long article (1000 tokens in, 2000 out):
- GPT-3.5: $0.005
- GPT-4: $0.12
```

---

## What Affects Cost?

### 1. Model Choice

| Model | Speed | Quality | Cost |
|-------|-------|---------|------|
| GPT-3.5 | Fast | Good | Low |
| GPT-4 | Medium | Great | Medium |
| GPT-4o | Fast | Great | Medium |

### 2. Number of Tokens

**Tips to reduce tokens:**
- Be concise in prompts
- Use short system instructions
- Don't include unnecessary context

### 3. Context Window Size

Bigger context = more expensive to process each request

### 4. Additional Features

| Feature | Extra Cost? |
|---------|-------------|
| Image input (vision) | Usually yes |
| Fine-tuning | Yes (training + usage) |
| Dedicated capacity | Yes |

---

## Free Options

### Free Tier Limits

| Provider | Free Usage |
|----------|-----------|
| OpenAI | $5 credit (new accounts) |
| Anthropic | Limited free tier |
| Google AI | Gemini free tier |
| Ollama | Completely free! |
| Hugging Face | Free inference endpoints |

### Free AI Tools

- **ChatGPT** (limited version)
- **Claude** (limited version)
- **Gemini** (limited version)
- **Ollama** (local, free)
- **LM Studio** (local, free)

---

## Hidden Costs

### 1. API Calls

Every request costs money

```
1 request = 1 cent
1,000 requests = $10
1,000,000 requests = $10,000
```

### 2. Vector Storage

Storing embeddings costs money

```
Pinecone: ~$0.08 per GB/month
Weaviate: ~$0.10 per GB/month
Chroma: Free (local)
```

### 3. Fine-tuning

Fine-tuning has setup + usage costs

```
OpenAI Fine-tuning: $3-12 per 1M tokens (training)
                   + standard API rates (usage)
```

### 4. Infrastructure

Running your own AI costs:

- Server costs
- Electricity
- Maintenance
- Dev time

---

## Cost Optimization Tips

### 1. Use the Right Model

```
Simple tasks: GPT-3.5 or Claude Haiku
Complex tasks: GPT-4 or Claude Sonnet
```

### 2. Cache Responses

```
User asks: "What is Python?"
Save response → Next time same question → Return cached response
```

### 3. Reduce Prompt Length

```
Too long: "Please, if you have time, could you maybe..."
Better: "Explain Python"
```

### 4. Use Streaming

Cancel early if needed!

### 5. Monitor Usage

Set up alerts for unexpected spending

---

## Budget Planning

### For Individuals

| Monthly Usage | Recommended | Approx Cost |
|--------------|-------------|-------------|
| Light (< 100K tokens) | Free tier | $0 |
| Medium (1M tokens) | GPT-3.5 | $5-10 |
| Heavy (10M tokens) | GPT-4 | $50-100 |

### For Small Business

| Usage | Recommended | Approx Cost |
|-------|-------------|-------------|
| Basic AI chat | Mix of free + paid | $50-200/mo |
| AI content | GPT-4 API | $200-500/mo |
| Custom AI | Fine-tuned + API | $500+/mo |

### For Enterprise

- Dedicated API endpoints
- Custom contracts
- Volume discounts
- Typically $5,000+/month

---

## Free vs. Paid Comparison

### Free Tools (ChatGPT, Claude)

| Pros | Cons |
|------|------|
| Easy to start | Limited features |
| No setup | Can't integrate |
| Good for learning | Privacy concerns |
| Free! | Rate limits |

### Paid API Access

| Pros | Cons |
|------|------|
| Full control | Technical setup needed |
| Integrations | Pay for usage |
| Custom workflows | Monitoring required |
| Scalability | Can get expensive |

---

## Making Smart Choices

### When to Pay

✅ Use paid API when:
- Building a product
- Need integrations
- High volume
- Need reliability

### When Free is Fine

✅ Use free tools when:
- Learning
- Personal use
- Low volume
- Experimenting

---

## Quick Reference 📋

| Term | Meaning |
|------|---------|
| **Token** | Unit of AI pricing (word part) |
| **Input tokens** | What you send to AI |
| **Output tokens** | What AI generates |
| **API** | Connection to AI service |
| **Free tier** | Limited free usage |
| **Fine-tuning** | Custom training (expensive) |

---

## Summary

### Cost-Saving Checklist

- [ ] Use GPT-3.5 for simple tasks
- [ ] Write concise prompts
- [ ] Cache common responses
- [ ] Monitor usage closely
- [ ] Set budget alerts
- [ ] Consider local AI (Ollama)

---

## Index: Complete Guide

➡️ **[00-Index.md](00-Index.md)** - Back to start!

---

*Understand the costs, optimize your spend! 💸*