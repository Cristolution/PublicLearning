# Prompting Basics ✍️

*The art of talking to AI so it actually helps you!*

---

## What is Prompting?

Prompting is just **asking the AI questions** in a way that gets you great results.

Think of it like asking a human assistant:

| Bad Way | Good Way |
|--------|---------|
| "Help" | "Write a professional email to my boss asking for vacation" |
| "Code" | "Write a Python function that calculates age from birth year" |
| "Explain" | "Explain blockchain to a 10-year-old using pizza as an example" |

---

## The Basic Formula

Every great prompt follows this pattern:

```
ROLE + TASK + FORMAT + EXTRAS
```

### Breaking It Down

**1. ROLE** - Who should the AI be?
```
"You are a professional resume writer"
"You are a friendly math teacher"
"You are a grumpy pirate"
```

**2. TASK** - What do you want?
```
"Write a resume summary"
"Explain fractions"
"Write me an adventure story"
```

**3. FORMAT** - How should it look?
```
"in bullet points"
"in 3 paragraphs"
"as a poem"
"in JSON format"
```

**4. EXTRAS** - Any special instructions?
```
"Include examples"
"Keep it under 200 words"
"Use simple words"
```

### Example Combined
```
"You are an experienced career counselor (ROLE)
Write a 3-sentence resume summary (TASK)
in bullet points with action verbs (FORMAT)
focusing on leadership and problem-solving (EXTRAS)"
```

---

## 7 Rules of Great Prompts

### Rule 1: Be Specific 🪲

❌ **Vague:** "Fix my code"
✅ **Specific:** "Find and fix the bug in my login function - it crashes when password is empty"

### Rule 2: Give Examples 📝

❌ **No examples:** "Write a product description"
✅ **With examples:** "Write a product description like this: 'Our product is like [example] but for [benefit]'"

### Rule 3: Set the Tone 🎨

❌ **No tone:** "Write a tweet about our launch"
✅ **With tone:** "Write a casual, excited tweet announcing our launch to developers"

### Rule 4: Mention Your Audience 👥

❌ **No audience:** "Explain this technology"
✅ **With audience:** "Explain this technology to non-technical managers who care about budget"

### Rule 5: Define the Output 📄

❌ **Open-ended:** "What should I do?"
✅ **Defined output:** "Give me 3 options ranked by cost and speed"

### Rule 6: Add Constraints 🚧

❌ **No limits:** "Write a presentation"
✅ **With limits:** "Write a 5-slide presentation under 10 minutes"

### Rule 7: Chain Your Requests 🔗

❌ **Single request:** "Write me a business plan"
✅ **Chain:** "Write me a business plan. Then give me 3 pitch deck headlines based on it."

---

## Prompt Templates Library 📚

### Email Template
```
Write a [type] email to [recipient]
about [topic].

Tone: [formal/casual/friendly]
Length: [short/medium/long]
Include: [specific request]
```

### Code Template
```
Write a [language] function that:
- Input: [what goes in]
- Output: [what comes out]
- Include comments explaining each step
```

### Content Template
```
Create a [type] about [topic]
for [audience]
that includes:
1. [element 1]
2. [element 2]
3. [element 3]

Tone: [desired tone]
Length: [word count]
```

### Explanation Template
```
Explain [concept] to [audience]
using [analogy/metaphor]
in [simple/detailed] terms.
```

---

## Common Prompt Mistakes ❌

### Mistake 1: Too Short
❌ "python"
✅ "Python is a programming language. Explain what it's used for and why beginners like it"

### Mistake 2: Too Many Questions
❌ "What's AI, how does it work, who invented it, is it dangerous, and should I learn it?"
✅ Break into separate prompts!

### Mistake 3: No Context
❌ "Continue"
✅ "Continue the story about [character name], who just discovered [event] in [location]"

### Mistake 4: Assuming AI Remembers
❌ "Fix it" (in a new chat)
✅ "Here's my code [paste code]. Fix the error that says [error message]"

---

## Chain of Thought (CoT) 🪜

When you want the AI to think step by step:

```
"Think step by step, then give me the answer."
```

This helps with:

- Math problems
- Logic puzzles
- Planning tasks
- Debugging

### Example
```
Question: If I have 12 apples and give 3 to Sarah and 2 to John, how many do I have left?

Let's think step by step:
1. Start with 12 apples
2. Give 3 to Sarah: 12 - 3 = 9
3. Give 2 to John: 9 - 2 = 7
Answer: 7 apples
```

---

## Few-Shot Prompting 📌

Give examples, then ask for similar output:

```
Translate to Spanish:
Hello → Hola
Goodbye → Adiós
Thank you →

[AI responds: Gracias]
```

---

## Quick Reference 📋

| Do | Don't |
|----|-------|
| Be specific | Be vague |
| Give examples | Assume understanding |
| One task at a time | Multiple questions |
| Define output format | Open-ended responses |
| Mention your audience | Skip context |

---

## Practice Exercises 🏋️

**Easy:** "Write a tweet about learning Python"

**Medium:** "Write a 280-character tweet announcing a Python workshop for beginners, including date and sign-up link"

**Hard:** "Write 5 different tweet variations for our Python workshop announcement. Each should be under 280 characters, appeal to a different audience (student, career changer, manager, hobbyist, professional), and include a call to action"

---

## Next Steps

➡️ **[03-Tools-And-Frameworks.md](03-Tools-And-Frameworks.md)** - Learn about AI tools!

---

*Simple prompts = Great results! ✨*