Act as a Staff/Principal Software Engineer producing a system design document for [TOPIC / SYSTEM NAME, e.g. "a URL shortener at 1B requests/day"].

Context:
- Scale: [expected users/QPS/data volume, or ask me to help estimate if I don't provide it]
- Constraints: [latency targets, budget, team size, existing infra, compliance needs — list what applies]
- Audience: this doc is for [interview practice / a real design review / onboarding docs] — adjust depth and jargon accordingly

Structure the document as:

1. Problem Statement & Requirements
   - Functional requirements
   - Non-functional requirements (scale, latency, availability, consistency)
   - Explicit out-of-scope items

2. Back-of-envelope Estimation
   - Traffic, storage, bandwidth estimates with the math shown

3. High-Level Architecture
   - Major components and how they interact
   - A description of the data flow (describe it in words/ASCII — I'll ask for a diagram separately if needed)

4. Deep Dive on 2-3 Critical Components
   - Pick the components where the interesting trade-offs live (e.g. database choice, caching strategy, partitioning scheme)
   - For each: what you chose, what you rejected, and why

5. Trade-offs & Alternatives
   - At least 2 major design decisions presented as "Option A vs Option B" with pros/cons, not just the chosen path

6. Bottlenecks, Failure Modes & Mitigations
   - Single points of failure
   - What breaks first at 10x scale, and how you'd address it

7. Open Questions / What I'd Validate With the Team
   - Things a real senior engineer would flag as unresolved rather than pretend to have solved

Constraints on style:
- Prioritize reasoning and trade-off articulation over exhaustive detail — I want to see the "why," not just the "what"
- Where multiple valid approaches exist, say so explicitly rather than presenting one as obviously correct
- Flag any assumption you're making so I can correct it