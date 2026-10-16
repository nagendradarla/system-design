# Architectures from the interview repos

Notes written from the interview repos. Each file is a revision guide: what the design is, why the main choice was made, and how to draw it. The scaled URL shortener in [chapter 8](../08-url-shortener.md) is a different document from the in-memory service these repos actually implement.

| Note | What it is |
| --- | --- |
| [Agentic SDLC orchestrator](agentic-sdlc-orchestrator.md) | LangGraph4j state graph around a URL shortener |
| [In-memory URL shortener](url-shortener-in-memory.md) | The Java service in `url-shortener` and the langgraph product package |
| [Supply-chain risk platform](supply-chain-risk-platform.md) | Ingest, entity resolution, scores, search, graph tiers, onboarding |
| [Multi-tenant API platform](multi-tenant-api-platform.md) | Auth, per-tenant token bucket, versions, bulkheads |
| [Risk signal pipeline](risk-signal-pipeline.md) | Kafka stages from raw signal to index and alerts |
| [Platform observability](platform-observability.md) | SLIs, error budgets, tenant labels |
| [DEHub data operators](dehub-data-operator-platform.md) | Operator contract, aspects, Iceberg Write-Audit-Publish |
| [News aggregator](news-aggregator.md) | Provider ingest, canonical store, feed, search |
| [TurboTax refund status](turbotax-refund-status.md) | Latest-status read path as implemented |
| [Identity and Datahub](identity-and-datahub.md) | Keycloak access layer and the Spark/Delta platform from the staff pitch |
| [Enterprise AI SDLC platform](enterprise-ai-sdlc-platform.md) | Spec service, orchestrator, sandboxed tools, audit log |
| [Spec-to-PR agent](spec-to-pr-agent.md) | Ticket to tested draft pull request, three retries, no merge |
| [AI code review gate](ai-code-review-gate.md) | Scanner plus review comment; critical blocks; humans still approve |
| [Legacy migration](legacy-migration-strangler.md) | Strangler fig, one slice at a time, parity and a feature flag |
| [Test generation agent](test-generation-agent.md) | Coverage gaps to tests; CI is the judge |
| [Bank dispute intake](bank-dispute-intake.md) | Case in a database, documents in object storage, async enrichment |
| [Multi-AZ, region loss, and DR](aws-ha-and-dr.md) | Zone failover first; 15 minute RPO and under an hour RTO |
| [Regulatory lakehouse and document Q&A](regulatory-lakehouse-and-doc-qa.md) | Delta on object storage; retrieve, cite, human accepts |

Not included, because the trees are placeholders and do not describe a running design:

- `fullstack_employee_management`: Java, `package.json`, Kubernetes, and Prometheus files contain the text "Placeholder content".
- `turbotax-refund-status-with-ui`: `pom.xml` is an empty `<project>` element and there is no UI source.
