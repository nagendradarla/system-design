# System design study set

Revision notes for the design problems in *System Design Interview: An Insider's Guide* (Alex Xu), chapters 4 through 15. These are original prep docs: the decisions, the math, and how to say them out loud. They are not a transcript of the book.

Audience assumed throughout: a 45-minute interview practice session. If you are using a note for a real design review, drop the "say this" lines and keep the trade-offs.

## How to use a note

1. Read **How to present** and **What to remember** the day before.
2. Close the note and talk through sections 1 to 3 in under 15 minutes.
3. Open **Deep dive** only for the two components you would actually defend. Section 3 of each note has an architecture diagram, a flow chart, and a short whiteboard sketch.
4. End on **Open questions**. Leaving something unresolved on purpose is a senior signal.

The method that applies to every topic is in [How to present](00-how-to-present.md).

## Designs

| Chapter | Topic | The decision to defend | Note |
| --- | --- | --- | --- |
| 4 | Rate limiter | Token bucket in a shared store, in front of the API | [rate limiter](04-rate-limiter.md) |
| 5 | Consistent hashing | Ring plus virtual nodes, so a membership change moves about 1/n of the keys | [consistent hashing](05-consistent-hashing.md) |
| 6 | Key-value store | AP store: quorum reads/writes, vector clocks, LSM on disk | [key-value store](06-key-value-store.md) |
| 7 | Unique ID generator | Snowflake-style 64-bit IDs, not a single ticket database | [unique ID generator](07-unique-id-generator.md) |
| 8 | URL shortener | ID generator, then base62; cache the redirect path | [URL shortener](08-url-shortener.md) |
| 9 | Web crawler | Polite, prioritized URL frontier; dedupe before fetch | [web crawler](09-web-crawler.md) |
| 10 | Notification system | One pipeline, a queue per channel, idempotent sends | [notification system](10-notification-system.md) |
| 11 | News feed | Fanout on write for normal users, fanout on read for celebrities | [news feed](11-news-feed.md) |
| 12 | Chat system | WebSocket for delivery, ordered IDs for history, heartbeat for presence | [chat system](12-chat-system.md) |
| 13 | Search autocomplete | Trie with top-k cached on each node, rebuilt from logs | [search autocomplete](13-search-autocomplete.md) |
| 14 | YouTube | Separate upload from playback; transcode offline; serve from CDN | [YouTube](14-youtube.md) |
| 15 | Google Drive | Metadata in a database, file bytes in block storage, sync by cursor | [Google Drive](15-google-drive.md) |

## Designs taken from the interview repos

These notes are the architectures found under `github/interviews`, written in the same revision format. They are not copies of those files.

Index: [from-interviews/README.md](from-interviews/README.md).

| Source | Design | Note |
| --- | --- | --- |
| langgraph4j-url-shortener | SDLC graph as the control plane, URL shortener as the data plane | [agentic SDLC](from-interviews/agentic-sdlc-orchestrator.md) |
| url-shortener and langgraph4j product code | In-memory shortener: idempotent create, 302, click counts | [in-memory URL shortener](from-interviews/url-shortener-in-memory.md) |
| Principal Architect - Platform | Supply-chain risk SaaS: ingest, graph, scores, search | [supply-chain risk](from-interviews/supply-chain-risk-platform.md) |
| Principal Architect - Platform | Tenant API gateway, token bucket, versioning, bulkheads | [multi-tenant API platform](from-interviews/multi-tenant-api-platform.md) |
| Principal Architect - Platform | Kafka signal, score, index, and alert pipeline | [risk signal pipeline](from-interviews/risk-signal-pipeline.md) |
| Principal Architect - Platform | Per-tenant SLOs, traces, and noisy-neighbor limits | [platform observability](from-interviews/platform-observability.md) |
| WEX DesignInterview | Data operators, Iceberg Write-Audit-Publish, open lake | [DEHub](from-interviews/dehub-data-operator-platform.md) |
| WEX DesignInterview | Ingest, canonical articles, feed, and search | [news aggregator](from-interviews/news-aggregator.md) |
| turbotax-refund-status | Latest refund read, optional live refresh, prediction stub | [refund status](from-interviews/turbotax-refund-status.md) |
| Service staff pitch | Keycloak access control and a Spark/Delta data platform | [identity and Datahub](from-interviews/identity-and-datahub.md) |
| AI Augmented Lead | SDLC platform: spec, sandbox, draft PR, audit | [enterprise AI SDLC](from-interviews/enterprise-ai-sdlc-platform.md) |
| AI Augmented Lead | Jira spec to a tested draft pull request | [spec-to-PR](from-interviews/spec-to-pr-agent.md) |
| AI Augmented Lead | CI review gate; critical findings block merge | [review gate](from-interviews/ai-code-review-gate.md) |
| AI Augmented Lead | Strangler migration of a monolith module | [legacy migration](from-interviews/legacy-migration-strangler.md) |
| AI Augmented Lead | Coverage-gap tests with CI as the judge | [test generation](from-interviews/test-generation-agent.md) |
| AWS Solutions Architect | Dispute case, documents, async analyst queue | [dispute intake](from-interviews/bank-dispute-intake.md) |
| AWS Solutions Architect | Multi-AZ, then region recovery | [HA and DR](from-interviews/aws-ha-and-dr.md) |
| AWS Solutions Architect | Lakehouse plus cited document Q&A | [lakehouse and Q&A](from-interviews/regulatory-lakehouse-and-doc-qa.md) |

`fullstack_employee_management` and `turbotax-refund-status-with-ui` are placeholder trees. There is no architecture in them to record.

## Assumptions that apply unless a note says otherwise

- One region first. Multi-region is a wrap-up topic, not the opening diagram.
- Interviewer is a teammate. State the assumption, then proceed.
- Round the math. Label every unit.
- There is no single correct design. Each note names at least two real options.
