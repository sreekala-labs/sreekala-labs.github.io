---
title: "Multi-Turn Conversations in Claude"
topic: Claude
summary: "Multi-Turn Conversations in Claude"
---

Claude doesn't store any of your conversation history. It is important to note that each request you make is completely independent. 

**What to do?**

* Manually maintain a list of all the messages in your code.
* Send the complete message history with every request.

Looking at the below code, you will see that:
* We are adding the user message.(Define Bhagavad Gita in one sentence).
* Sending the initial user message to Claude.
* Taking the response from Claude and adding it the message list as an assistant message.
* Add a follow-up question as another user message. 
* Sending the entire history to Claude.

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

#multi conversation.
#Step1: User Message 
#Step2: Response
# Step3: Take the response and add the context to assistant message,. 

def add_user_message(messages, text):
    user_messages={"role":"user","content":text}
    messages.append(user_messages)
    
def add_assistant_message(messages, text):
    assistant_message ={"role":"assistant","content":text}
    messages.append(assistant_message)

def chat(messages):
    message = client.messages.create(
        model=model,
        max_tokens=1000,
        messages= messages
    )
    return message.content[0].text

messages=[]
add_user_message(messages,"Define Bhagavad Gita in one sentence")
answer= chat(messages)
print(answer)
add_assistant_message(messages, answer)

print("#Writing another sentence")
add_user_message(messages, "Write another sentence")
final_answer= chat(messages)
print(final_answer)



```
