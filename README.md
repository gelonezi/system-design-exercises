# System Design Exercises

Architecture diagrams drawn as system-design practice, in [Excalidraw](https://excalidraw.com).

## Judiciary Integration Platform

**[→ Open the board in Excalidraw](https://excalidraw.com/#json=a-eHnApUWQOO8Mw825KjP,vkUMiKu2Mo9H3pV9tt0TKg)**
· or open `judiciary-integration-architecture.excalidraw` locally

A generalized reference architecture for an integration platform that gives several
internal products a **single API contract** over dozens of heterogeneous legacy court
systems — abstracting consumers from the constant change in those external systems.

**Shape of the system**

- ~25 .NET microservices on AWS EKS (Helm-versioned packages)
- Two entry paths: synchronous via Ingress, asynchronous via RabbitMQ + an async processor
- A layered core: **Catalog** (per-system configuration) → **SDK** (protocol contracts and
  per-system corner cases) → **Connectors** (stateless adapters) → **Controllers**
  (orchestration across connectors)
- Two external protocol families: SOAP (a national interoperability standard, multiple
  versions) and REST
- DocumentDB for metadata and caching, S3 for document binaries
- Keycloak for authentication, Vault for external-system credentials
- Elasticsearch / Kibana / Elastic APM for logs, metrics and distributed traces

**Views on the board**

| View | What it shows |
|---|---|
| Operations | The five-operation public contract |
| Static Components | What the pieces are, for one operation end to end |
| System Behaviour | UML sequence — how a request flows, sync and async |
| Supporting Systems | The infrastructure inventory |
| Continuous Integration / Deployment | How it ships |

## Note

These diagrams are **generalized references**. Product names and company-specific details
have been removed; they are shared to illustrate architectural patterns, scale and design
trade-offs — not proprietary implementation.
