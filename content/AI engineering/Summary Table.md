| Concept                          | What It Is                                       | Role                     | Scope           | Example                                               |
| -------------------------------- | ------------------------------------------------ | ------------------------ | --------------- | ----------------------------------------------------- |
| **Agent**                        | An AI system that can act, decide, and use tools | The “brain + executor”   | High-level      | A coding assistant that writes, debugs, and runs code |
| **Sub-agent**                    | A smaller agent inside a bigger one              | Delegation               | Medium          | “Research agent” inside a main AI system              |
| **Skills**                       | Predefined capabilities an agent can perform     | Execution ability        | Medium          | Summarizing text, writing code, analyzing data        |
| **Agent Skills**                 | Skills specifically assigned to an agent         | Specialization           | Medium          | A “debugging skill” only for dev agent                |
| **Tools**                        | External functions/APIs the agent can use        | Action layer             | External        | Calculator, database query, web search                |
| **Plugins**                      | Packaged external integrations                   | Extended tools           | External        | Notion plugin, Google Drive plugin                    |
| **MCP (Model Context Protocol)** | Standard for connecting models to tools/data     | Infrastructure           | System-level    | Lets AI access files, APIs in structured way          |
| **Rules**                        | Constraints the agent must follow                | Control                  | Global or local | “Never expose API keys”                               |
| **Context**                      | All information the agent sees right now         | Memory (short-term)      | Dynamic         | Chat history, documents, instructions                 |
| **Prompt**                       | Input given to the model                         | Immediate instruction    | Local           | “Write a Python function”                             |
| **System Prompt**                | Hidden top-level instructions shaping behavior   | Personality + boundaries | Global          | “You are a precise coding assistant”                  |
| **Prompt Engineering**           | Crafting better prompts                          | Optimization             | Input-level     | Structuring tasks clearly                             |
| **Context Engineering**          | Designing what info the model receives           | Optimization             | System-level    | Injecting docs, memory, constraints                   |
