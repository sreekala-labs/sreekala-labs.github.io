---
title: "Fixed Window vs. Sliding Window: Where Rate Limiters Actually Break"
topic: System Design
summary: "The bug isn't in the algorithm, it's at the boundary."
---

Rate limiting always sounds simple until you draw the boundary between two
windows and ask what happens to a client sitting right on top of it.

## Fixed window counter

Simplest to implement: count requests in a bucket keyed by
`floor(timestamp / window_size)`, reject once the count exceeds the limit,
reset the bucket when the window rolls over.

The problem is the edge. A client can burst right at the end of one window
and again right at the start of the next, doubling the effective limit for
a short stretch around the boundary. For a limit of 100/minute, that's up
to 200 requests in a much shorter span than a minute — which defeats the
point of the limiter.

## Sliding window log

Store a timestamp per request, count how many fall inside the trailing
window on every check. Accurate, no boundary problem — but it costs memory
proportional to request volume, and pruning old timestamps adds work on
the hot path.

## Sliding window counter

The practical middle ground: keep counts for the current and previous
fixed windows, then weight the previous window's count by how much of it
still overlaps the trailing window.

```
estimated_count = current_window_count
                 + previous_window_count * overlap_fraction
```

Cheap like the fixed window, close enough to accurate like the log. Most
production limiters (including the token-bucket variants API gateways
ship with) are some flavor of this.

**What I'd actually reach for:** token bucket for smoothing bursts while
allowing short spikes, sliding window counter when I need a hard,
predictable ceiling per client.
