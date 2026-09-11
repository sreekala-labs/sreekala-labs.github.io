---
title: "Context window and Boundary"
topic: AI
summary: "What is a context window and what happens at the boundary?"
---

**Context Window:**

A context window is a maximum amount of information(words, sentences, characters etc), a LLM can process, process memory for and pay attention to any single moment.

Think of it as a short-term memory, anything outside the window does not exists to the model during generation. 

**What happens at the boundary?** 

When an input conversation, document or prompt exceeds the context window limits, the system hits a hard boundary. Depending on how the API, system, or application is engineered, 
one of three main behaviors occurs: 

* Truncation (Sliding Window): The most common default. Older tokens from the beginning of the conversation are silently dropped to make room for new inputs.
  The model loses historical context, leading to "forgetting" earlier instructions, facts, or constraints set at the start of the chat.
* Hard Refusal / API Error: Many raw LLM APIs will throw a context limit error (e.g., 400 InvalidRequestError: Maximum context length exceeded)
  and refuse to generate a response until tokens are removed or reduced. 
  
  Example, in Claude : If the input alone already exceeds the model's context window, the API returns a
  400 invalid_request_error ("prompt is too long") on every model. On Claude 4.5 models and newer, if input tokens plus max_tokens exceeds the context window size,
  the API accepts the request. If generation then reaches the context window limit, it stops with stop_reason: "model_context_window_exceeded".
* Performance Degradation ("Lost in the Middle"):
  Even when text stays just inside a very large context window (e.g., 128k+ tokens), the attention mechanism struggles to give equal weight to every token.
  Information buried deep in the middle of a massive context window is significantly harder for the model to retrieve accurately compared to text at the very
  beginning or very end.


**How Attention Works Within the Boundary** 

* Quadratic Attention Complexity (O(N^2)): Standard self-attention calculates how every token relates to every other token.
  Doubling the context window quadruples the memory and computational load needed to calculate attention scores.

* Positional Encodings: Models use positional embeddings to keep track of word order. When inputs exceed the range of position indexes the model was trained on,
  its ability to maintain logical ordering and syntax rapidly degrades.
