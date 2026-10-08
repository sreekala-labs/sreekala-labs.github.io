---
title: "Response Streaming"
topic: AI > Claude
summary: "Response Streaming in AI"
---

You might have noticed that when you type a prompt in the chat window, the response takes about 10-30 seconds and during this time, the user 
isn't notified or user keeps staring at the screen. 

In order to avoid this, Claude offers sonething streaming which can be set at the time of creating a message by setting stream=True. 

```python
from dotenv import load_dotenv
load_dotenv()

from anthropic import Anthropic
client= Anthropic()
model="claude-haiku-4-5"

def chat(message):
    response = client.messages.create(messages=message, max_tokens=1000, model=model, stream=True)
    
    for event in response:
        print(event)

messages=[]
messages.append({"role":"user","content":"What is the prime number after 1M?"})

response = chat(messages)
print(response)

#Displays only text.
with client.messages.stream(
    model=model,
    max_tokens=1000,
    messages=messages
) as stream:
    for text in stream.text_stream:
        print(text, end=" ")

#Displays the Complete message. 
with client.messages.stream(
    model=model,
    max_tokens=1000,
    messages=messages
) as stream:
    for text in stream.text_stream:
        pass

    final_message= stream.get_final_message()
    print(final_message)
```

---
```output
RawMessageStartEvent(message=Message(id='msg_011CfpHhvSxfWma8Tz1oSAS4', container=None, content=[], model='claude-haiku-4-5-20251001', role='assistant', stop_details=None, stop_reason=None, stop_sequence=None, type='message', usage=Usage(cache_creation=CacheCreation(ephemeral_1h_input_tokens=0, ephemeral_5m_input_tokens=0), cache_creation_input_tokens=0, cache_read_input_tokens=0, inference_geo='not_available', input_tokens=17, output_tokens=1, output_tokens_details=None, server_tool_use=None, service_tier='standard'), diagnostics=None), type='message_start')
RawContentBlockStartEvent(content_block=TextBlock(citations=None, text='', type='text'), index=0, type='content_block_start')
RawContentBlockDeltaEvent(delta=TextDelta(text='#', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text=' Prime', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text=' Number', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text=' After 1 ', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text='Million\n\nThe first', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text=' prime number after ', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text='1,', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text='000,000 ', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text='is **1', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text=',000', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text=',003', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockDeltaEvent(delta=TextDelta(text='**.', type='text_delta'), index=0, type='content_block_delta')
RawContentBlockStopEvent(index=0, type='content_block_stop')
RawMessageDeltaEvent(delta=Delta(container=None, stop_details=None, stop_reason='end_turn', stop_sequence=None), type='message_delta', usage=MessageDeltaUsage(cache_creation_input_tokens=0, cache_read_input_tokens=0, input_tokens=17, output_tokens=32, output_tokens_details=None, server_tool_use=None))
RawMessageStopEvent(type='message_stop')
```

If you look at the output, you notice the following events:
1. MessagesStart : Start of the message.
2. ContentBlockStart : Start of the chunk which includes using tool set etc.
3. ContactBlockDelta : Chunks of generated text. As you can see these are many in number(chunks).
4. ContentBlockStop : End of the chunk generation.
5. MessageDeltaEvent : Current Message is complete. You can see that the stop_reason is "end_turn".
6. MessageStopEvent : End of the message. You can see from the output above that the type is "message_stop".

