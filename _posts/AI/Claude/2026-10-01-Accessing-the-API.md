---
title: "Accessing the API"
topic: Claude
summary: "Accessing the API(Claude)"
---

I was reading the Claude Academy Course and I found that they had 67 Lessons that you can just read along with. Course is called "Building with Claude API". 

My key takeaway from the first topic, Accessing the API are: 

1. There is a Five-Step Request Flow.
   * Request to Server
   * Request to Anthropic API
   * Model Processing
   * Response to Server
   * Response to Client.
2. The main reason we need a server and recommendation not to call Anthropic API directly from the client-code is
   * API request requires a secret API key for authentication.
   * Exposing this key in the client-code creates a serious security vulnerability. 
3.  When you are sending a request, they must include these essential fields:
    * API key
    * Model
    * Messages
    * Max Tokens. 
4.  Model Processing
    * Tokenization
    * Embedding
    * Contextualization
    * Generation
5.  When Claude stops Generating:
    * Max tokens reached
    * EOS - Natural ending.
    * Stop Sequence
6. What does the API response contain?
    * Message
    * Usage
    * Stop Reason






  
