---
title: "AI and LLM Fundamentals"
topic: AI
summary: "Some basic questions on AI and LLM fundamentals with Brief Answers"
---

1. **What is a Large Language Model?**
   
   A neural network(transformer) trained on huge amounts of text to predict the next token. Everything it does, from chat
   to tool calls, comes from that one skill applied repeatedly. 
2. **What is a token?**
   
   A token is a chunk of text, roughly 3-4 characters in English. Pricing, context limits, and latency all scale with tokens, so a bloated
   prompt costs money and adds delay. 
3. **What is a context window?**

   The maximum number of tokens the model can see at once: system prompt, conversation history, tool results and its own output. When a long call exceeds,
   older content gets dropped or truncated, and the agent "forgets" earlier details.
4. **What does temperature control?**

   How random the output is. Low(0.0-0.3) gives consistent, predictable answers, which suits support and booking agents. High gives more varied creative
   answers but more drift. 
5. **What is a system prompt?**

   The standing instructions that define the agent's role, rules, tone and boundaries. It is sent with every turn, so its length directly affects
   latency and cost. 
6. **What is prompt engineering? Name a few techniques:**

   Designing instructions so the model behaves reliably. 
   Few Techniques: 
   * Clear Role and Goal
   * Explicit Rules
  
   Examples(few-shot):
   * Step-by-step structure
   * Output format constraints
   * Telling the model what to do when unsure. 
7. **Zero-shot vs Few-shot prompting?**

   Zero-shot prompting gives only instructions. 
   
   Few-shot adds a handful of input and output examples, which is useful when you want a specific format or tone.
   
8. **What is hallucination and how do you reduce it?**

    The model states something false with confidence. 
    
    Reduce it by
    
    * Grounding answers in Retreived Data(RAG) or tool results,
    * Lowering temperature
    * Telling the model to say "I don't know," and
    * Constraining its scope. 
9. **What is RAG(retrieval-augmented generation)?**

    Before answering, the system searches a knowledge base for relevant passages and adds them to the prompt. The model answers from the real data
    instead of memory. 
10. **What are embeddings?**
    
    Numeric vectors that represent meaning. Similar texts have nearby vectors, which is how RAG finds relevant documents via similarity search. 

    ![Support Vector](/embeddings.gif)
    
11. **What is a vector database?**

    A store optimized for similarity search over embeddings, such as pinecone, pgvector or Weaviate. 
12. **What is function calling(tool use)?**
    
    The model outputs a structured request, such as a function name plus JSON arguments, instead of plain text. Your code runs the function and        returns the result and the model uses it in its reply. 

13. **What makes a tool definition work well?**

    * A clear name
    * A description that says when to use it
    * A tight JSON schema with required fields and examples in the Prompt.
    * Vague descriptions are the top reason tools don't fire. 
14. **What are structured outputs?**

    Forcing the model to return JSON that matches a schema. This is useful for extracting data after a call, such as name, intent and outcome, and
    it prevents parsing failures.
15. **What is an AI Agent?"**
   
    An LLM that runs in a loop: It decides an action, calls a tool, reads the result, and decides again until the goal is met. A voice assistant       with tools is an agent.
16. **What is Model Context Protocol(MCP)?**

    An open standard for connecting AI models to tools and data sources through a common interface, so tools can be reused across clients. 
17. **Fune-tuning vs prompting vs RAG: when do you use each?**

    Prompting first, since it is cheap and fast to iterate.

    RAG when the model needs specific or changing facts. 

    Fine-tuning when you need a consistent style or behavior that prompts can't reliably produce. 
18. **What is Time to First Token(TTFT)?**

    The delay before the model streams its first word. In voice, Text-to-speech(TTS) can start speaking as soon as tokens arrive, so TTFT drives       how fast the agent *feels*.
19. **What is streaming?**
    
    Returning tokens as they are generated instead of waiting for the whole answer. Without it, callers would wait in silence for the full response.
20. **How do you choose between a larger and a smaller model?**

    Bigger Models reason better but are slower and cost more. Voice agents usually favor fast models, and escalate to larger ones only for complex reasoning steps.
21. **What is prompt injection?** 

    User input that tries to override the system instructions, like "Ignore your rules and ...". Defend with clear boundaries in the prompt, validating tool arguments on your server and never trusting the model for authorization. 
22. **What are guardrails?**  

    Rules or checks that keep the agent in scope, such as topic restrictions, content filters, output validation, and requiring confirmation before actions like      payments or cancellations. 
   
23. **How do you evaluate an AI agent's quality**

    Define test scenarios, run them repeatedly and score outcomes: task success, correct tool calls, latency and tone. Review call transcripts for failures, then     turn those into new test cases. 
24. **Why might the same prompt gives different results each time?**

    * Sampling randomness(Temperature above 0)
    * Model version changes.
    * Different conversation history
    * Different tool results. 

    Best practice is to Lower Temperature and pin model versions for consistency. 
   
25. **What is multimodal AI?**

    Models that handle more than text such as audio, video, or images. Speech-to-Speech models process audio directly instead of chaining 
    STT, LLM and TTS, which can reduce latency. 
