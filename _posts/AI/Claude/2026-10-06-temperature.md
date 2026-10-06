---
title: "Temperature in AI"
topic: AI > Claude
summary: "Concept of Temperature in AI"
---

Temperature in Claude is a parameter which controls how predictable or creative claude's response will be. 
Temperature paramaters accepts value between 0 and 1. 0 being the less creative, 1 being super creative. 

Claude becomes very deterministic at near 0. Claude distributes probability more evenly across options, leading to more varied and creative options.

|Temperature Ranges| When to Use | 
|---|---|
|0.0-0.3| Support Bot, Coding assistance, data extraction, content moderation|
|0.4-0.7| Educational content, problem-solving, Summarization | 
| 0.8-1.0 | Creative writing, brainstorming, Marketing content | 

```python
from dotenv import load_dotenv
load_dotenv()
from anthropic import Anthropic
client= Anthropic()
model="claude-haiku-4-5"

def chat(messages, system=None, temperature=1.0):
    
    params={
        "model":model,
        "temperature":temperature,
        "max_tokens":1000,
        "messages":messages
        }
    
    if system:
        params["system"]=system 
        
    message = client.messages.create(**params)
    return message.content[0].text 

messages=[]
messages.append({"role":"user","content":"Movie ideas in 2 lines"})
answer= chat(messages, temperature=0.0)
print(answer)
```
