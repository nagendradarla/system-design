# How to present a system design

Use this before any of the topic notes. The topic notes assume you already run the interview this way.

## What the interviewer is actually scoring

They are not scoring whether you reproduced a famous architecture. They are scoring whether you can:

- Turn a vague prompt into a bounded problem.
- Pick a design that fits the scale you just estimated, and say what you rejected.
- Go deep on the one or two components where the design can fail.
- Change your mind when they push back.

Over-engineering is a negative signal. A startup design and a billion-user design are different answers to the same prompt. Say which one you are designing.

## 45-minute clock

| Minutes | Step | You are done when |
| --- | --- | --- |
| 3 to 10 | Scope | Functional requirements, non-functional requirements, and explicit out-of-scope items are written down |
| 10 to 15 | High-level design plus estimate | They can repeat your diagram back, and the numbers justify the boxes |
| 10 to 25 | Deep dive | Two components have a chosen approach, a rejected approach, and a failure mode |
| 3 to 5 | Wrap | Bottleneck at 10x, what you would measure, one thing you did not pretend to solve |

If they steer you, follow them. The clock is a default, not a script you must finish.

## What to say in the first two minutes

Do not draw boxes yet.

1. Restate the product in one sentence.
2. Ask what is in scope. Users, the one or two core actions, and what "done" means.
3. Ask for scale, or offer an assumption and wait for a nod.
4. Ask what matters more: latency, correctness, cost, or time to ship.
5. Write the out-of-scope list so you are not graded on it later.

Questions that usually pay off:

- Web, mobile, or both?
- Read-heavy or write-heavy?
- Strongly consistent, or is slightly stale data acceptable?
- One region or many?
- What already exists that we should reuse?

If they say "you decide," write the assumption on the board. You will need it when the deep dive contradicts it.

## What to remember while estimating

Process beats precision. Round aggressively and keep units attached.

Handy anchors (order of magnitude, not lab measurements):

- L1/L2 cache and memory references are nanoseconds to about 100 ns.
- A datacenter round trip is well under 1 ms. A cross-country round trip is tens of ms. A transcontinental round trip is on the order of 150 ms.
- A disk seek is milliseconds. Sequential disk is much cheaper than random seeks. This is why logs and SSTables show up so often.
- Compress before you send bytes across a region boundary.

Availability, so you do not invent a nine:

| Target | Downtime per year |
| --- | --- |
| 99% | about 3.7 days |
| 99.9% | about 8.8 hours |
| 99.99% | about 53 minutes |
| 99.999% | about 5 minutes |

Powers of two you will actually use: 2^10 is about 10^3 (KB vs thousand), 2^20 about a million, 2^30 about a billion. For interview math, 100 million / 86400 is about 1,200 per second. 2x that is a reasonable peak unless the product is spiky (ticket drops, live events).

Always estimate: QPS, peak QPS, storage for the retention window, and bandwidth if the payload is large (video, images, crawl). Cache size and server count only if they change the design.

## How to draw the high-level design

Left to right, one user action:

```
client -> DNS -> load balancer -> stateless service -> cache -> database
                                      |
                                      +-> queue -> workers -> external system
```

Then walk one write and one read in words. Name the state each box owns. If a box owns no state, say it is stateless and why that matters (any instance can take the next request).

Get a nod before the deep dive. "The interesting part is X. I would spend the remaining time there unless you want Y."

## Deep dive rules

- Pick components where a trade-off lives: data model, partition key, consistency, fanout, ordering, hot keys.
- For each: what you chose, what you rejected, and the condition that would flip the choice.
- Do not spend the slot on a ranking formula, a UI, or a protocol you cannot operate.
- If you propose two options, you must pick one for the rest of the interview. "It depends" without a pick reads as unfinished.

## Wrap the way a staff engineer wraps

- Name the first thing that breaks at 10x, and the change you would make then, not now.
- Name the single point of failure you still have, and whether you accept it.
- Name one metric you would page on.
- Name one open question you would take back to the team. Do not invent a fake answer in the last minute.

## Do

- Ask, then assume, then proceed.
- Offer two approaches on the decision that matters.
- Design the critical path first.
- Talk while you think. Silence looks like stuck.
- Ask for a correction early: "Does this match the scale you had in mind?"

## Do not

- Start with a microservice diagram.
- Claim the design is complete.
- Hide inside one component for twenty minutes.
- Use a stronger consistency model than the product needs. It costs latency and availability.
- Confuse a building block (consistent hashing, a queue, a CDN) with the product.

## Checklist you can glance at before you speak

- Users and the core action
- QPS and the storage number, with units
- One picture, two flows
- Two rejected alternatives
- Failure of the datastore and failure of one region
- What you would not build in v1
