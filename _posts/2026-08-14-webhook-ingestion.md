---
title: "Webhook Ingestion: Kafka vs. a Simple Queue"
topic: Architecture
summary: "Reaching for Kafka before you've outgrown SQS is a tell, not a strength."
---

Every "design a webhook ingestion system" prompt eventually asks the same
question: do you need Kafka, or do you need a queue?

## What the webhook actually needs

A webhook receiver has one job under pressure: accept the request fast and
acknowledge it, before doing any real work. The sender (Stripe, GitHub,
whoever) has its own retry policy and will back off or disable the
endpoint if you're slow or unreliable. So the architecture splits into two
concerns — durable intake, and processing — on purpose.

```
sender --> receiver (validate, ack fast) --> queue --> worker(s) --> side effects
```

## Simple queue (SQS, Cloud Tasks, Redis-backed)

- Good default. Durable, ordered-enough, dead-letter queues built in.
- Scales horizontally by adding workers.
- Right choice when you have one or a handful of consumers and don't need
  replay or multiple independent consumers reading the same stream.

## Kafka

- Buys you replay (consumers can re-read history), multiple independent
  consumer groups off the same topic, and much higher sustained throughput.
- Costs you operational complexity — partitioning strategy, consumer
  group rebalancing, retention tuning — that a simple queue doesn't have.

**The actual answer in an interview:** start with the simple queue and
name the specific pressure that would force a move to Kafka — multiple
teams needing independent reads of the same event stream, or a replay
requirement for reprocessing after a bug. Reaching for Kafka without one
of those pressures reads as cargo-culting the tool, not solving the
problem.

## Idempotency, either way

Whatever sits behind the queue needs to assume at-least-once delivery.
Dedupe on the sender's event ID before applying side effects — payment
webhooks especially will retry, and "processed twice" is usually worse
than "processed late."
