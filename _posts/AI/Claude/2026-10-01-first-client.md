---
title: "Making a request"
topic: AI > Claude
summary: "Making a request"
---



This is the first python code which is client side. The .env has the ANTHROPIC_API_KEY. The API Key can be obtained from platform.claude.com. 

In order to call Claude from the API, the most important and the core method call is : client.messages.create() function. 
This function accepts 3 parameters(required):
 * model
 * max_tokens
 * messages

Messages are split into 2:
  * User Messages: The one which the human provides.(Content you want to send to Claude). 
  * Assistant Messages: The response that Claude has generated.

Every message is a dictionary with a role(user or assistant) and the content as shown in the code below. 

```python
from dotenv import load_dotenv
load_dotenv()

from anthropic import Anthropic
client= Anthropic()
model="claude-haiku-4-5"

#Core : client.messages.create() function
# 3 parameters
# 1. model 
# 2. max_tokens 
# 3. messages 

message= client.messages.create(
    model="claude-haiku-4-5",
    max_tokens=1000,
    messages=[
        {
        "role":"user",
        "content":"What is Bhagavad Githa? Answer in one sentence."
        }
    ]
)

print(message.content[0].text)
```

```
Output:
The Bhagavad Gita is a 700-verse Hindu scripture embedded in the epic Mahabharata
that presents a philosophical dialogue between Lord Krishna and the warrior
prince Arjuna about duty, righteousness, and the nature of life.
```
