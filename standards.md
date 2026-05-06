# Standards & API Reference

> Project: Developer Documentation Search · Generated: 2026-05-03

## Industry Standards & Specifications

### ISO Standards

No ISO standards have been identified as directly governing developer documentation search engines or full-text search indexing protocols. ISO standards become relevant at the storage and interoperability layer (ISO 8601 for date-time in index records, ISO 639 for language codes used in multi-language search). If the product expands into enterprise compliance, ISO/IEC 27001 (information security management) and ISO/IEC 25010 (software quality) become applicable to the deployment architecture.

### W3C & IETF Standards

| Standard | URL | Relevance |
|----------|-----|-----------|
| RFC 7230–7235 — HTTP/1.1 | https://www.ietf.org/rfc/rfc2616.txt | All search query and result APIs are delivered over HTTP; TLS upgrade to HTTPS is mandatory for API keys in transit |
| RFC 9110 — HTTP Semantics (current) | https://www.rfc-editor.org/rfc/rfc9110 | Supersedes HTTP/1.1 RFCs; defines caching, content negotiation, and status codes used by search REST APIs |
| RFC 8288 — Web Linking | https://www.rfc-editor.org/rfc/rfc8288 | Link relations used in paginated search results (`rel=next`, `rel=prev`) and cross-resource citation links |
| RFC 6902 — JSON Patch | https://www.rfc-editor.org/rfc/rfc6902 | Partial updates to search index configurations and settings objects |
| RFC 6570 — URI Templates | https://www.rfc-editor.org/rfc/rfc6570 | Parameterised search endpoint URLs (e.g. `/indexes/{index}/search`) |
| Sitemaps Protocol (sitemaps.org) | https://www.sitemaps.org/protocol.html | Standard XML format consumed by documentation crawlers to discover and prioritise URLs for indexing; supported by Algolia DocSearch and Meilisearch crawlers |
| Robots Exclusion Protocol (RFC 9309) | https://www.rfc-editor.org/rfc/rfc9309 | `robots.txt` directives govern what a crawler may index; must be respected to avoid ingesting restricted documentation pages |
| W3C JSON-LD 1.1 | https://www.w3.org/TR/json-ld11/ | Structured metadata embedded in documentation pages; improves semantic understanding of page hierarchy and relationships during indexing |
| Schema.org TechArticle / SoftwareSourceCode | https://schema.org/TechArticle | Vocabulary for annotating API reference pages, tutorials, and code samples; enables richer snippet extraction during corpus ingestion |
| W3C WCAG 2.2 | https://www.w3.org/TR/WCAG22/ | Search UI components (autocomplete widgets, results lists) must meet accessibility requirements for keyboard navigation and screen-reader support |

### Data Model & API Specifications

| Standard | URL | Relevance |
|----------|-----|-----------|
| OpenAPI Specification 3.1.0 | https://spec.openapis.org/oas/3.1/schema-base/2025-08-31.html | The canonical format for describing search REST APIs; Typesense publishes its full API as an OpenAPI YAML file; Algolia and Meilisearch expose OpenAPI-compatible interfaces |
| JSON Schema (Draft 2020-12) | https://json-schema.org/ | Used for validating search query payloads, index configuration objects, and webhook event schemas; OpenAPI 3.1 adopts JSON Schema 2020-12 natively |
| GraphQL | https://spec.graphql.org/ | Alternative query interface adopted by some documentation platforms (e.g. GitHub Docs) to enable flexible field-level queries on search results |
| Atom Syndication Format (RFC 4287) | https://www.rfc-editor.org/rfc/rfc4287 | RSS/Atom feeds used to ingest changelog, release notes, and blog content into the documentation corpus on a continuous basis |
| NDJSON / JSON Lines | https://jsonlines.org/ | Bulk import/export format for search index snapshots and batch indexing operations; used by Elasticsearch and OpenSearch `_bulk` API |

### Security & Authentication Standards

| Standard | URL | Relevance |
|----------|-----|-----------|
| OAuth 2.0 (RFC 6749) | https://oauth.net/2/ | Delegated authorisation for permission-aware search: access tokens carry user scopes that restrict which index segments or source documents a query can return |
| OpenID Connect 1.0 | https://openid.net/connect/ | Identity layer over OAuth 2.0; provides authenticated user claims (email, groups, roles) consumed by the search engine to filter results by entitlement |
| API Key authentication | — | Simple bearer-token model used by Algolia, Typesense, and Meilisearch for non-user-facing server-to-server indexing calls; scoped by ACL (search-only vs. admin) |
| OWASP API Security Top 10 | https://owasp.org/www-project-api-security/ | Baseline security checklist for search API implementations: broken object-level authorisation is the primary risk when search crosses permission boundaries |
| TLS 1.3 (RFC 8446) | https://www.rfc-editor.org/rfc/rfc8446 | All API traffic must be encrypted in transit; required by Algolia, Meilisearch, and Typesense cloud endpoints |
| GDPR (EU 2016/679) | https://gdpr-info.eu/ | Personal data appearing in indexed documentation (e.g. names in commit messages or support threads) requires data-subject deletion propagation to the search index |

### MCP Server Specifications

The Model Context Protocol (MCP) — current specification 2025-11-25 — is directly applicable to developer documentation search. An MCP server wrapping a documentation search index allows AI agents and LLM assistants to issue natural-language queries and receive cited source passages as structured tool results.

| Resource | URL |
|----------|-----|
| MCP Specification 2025-11-25 | https://modelcontextprotocol.io/specification/2025-11-25 |
| MCP GitHub Organisation | https://github.com/modelcontextprotocol |
| 2026 MCP Roadmap | https://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/ |

MCP relevance: A documentation search product should expose an MCP server so that AI coding assistants (Claude, Copilot, Cursor) can call `search_docs(query)` as a tool. The tool result includes ranked passages with source URLs, enabling the LLM to cite documentation inline. Kapa.ai already ships a hosted MCP server endpoint for this use case.

---

## Similar Products — Developer Documentation & APIs

### Algolia Search

- **Description:** Hosted search-as-a-service with typo tolerance, faceting, and InstantSearch UI libraries. The de-facto standard for public documentation search (used by React, Vue, Stripe, and many others via DocSearch).
- **API Documentation:** https://www.algolia.com/doc/rest-api/search
- **SDKs/Libraries:** JavaScript, Python, Ruby, PHP, Go, Java, Swift, Kotlin, Scala — https://www.algolia.com/doc/api-client/getting-started/what-is-the-api-client/javascript/
- **Developer Guide:** https://www.algolia.com/doc/
- **OpenAPI Spec:** Not publicly published; Algolia uses a proprietary REST API documented by reference
- **Standards:** REST/JSON, HTTPS only, API-Key authentication (X-Algolia-Application-Id + X-Algolia-API-Key headers)
- **Authentication:** Scoped API keys with ACL; no OAuth 2.0 on the search path — OAuth used only for dashboard SSO

### DocSearch by Algolia

- **Description:** Free hosted search for qualifying open-source documentation sites. Uses a web crawler (Python Scrapy-based legacy; new Algolia Crawler for v3) to build and maintain the index automatically.
- **API Documentation:** https://docsearch.algolia.com/
- **Scraper Repository:** https://github.com/algolia/docsearch-scraper
- **Config Reference:** https://docsearch.algolia.com/docs/legacy/config-file/
- **Standards:** JSON config files with CSS selectors; sitemaps.xml consumption for crawl discovery; Robots Exclusion Protocol honoured
- **Authentication:** API key embedded in frontend InstantSearch widget

### Typesense

- **Description:** Open-source search engine offering a REST API compatible with the Algolia InstantSearch ecosystem. Self-hostable and available on Typesense Cloud.
- **API Documentation:** https://typesense.org/api
- **OpenAPI Spec:** https://github.com/typesense/typesense-api-spec (OpenAPI YAML, used to auto-generate client libraries)
- **SDKs/Libraries:** JavaScript, Python, Ruby, PHP, Go, Java, Swift, Dart — https://typesense.org/docs/guide/
- **Postman Collection:** https://www.postman.com/typesense/typesense-api/documentation/vui2fuq/typesense-api
- **Standards:** REST/JSON, OpenAPI 3.x, HTTPS; scoped API keys; Raft-based clustering protocol for HA
- **Authentication:** X-TYPESENSE-API-KEY header; key scoping by collection and operation

### Meilisearch

- **Description:** Lightning-fast open-source search engine with first-class support for hybrid (keyword + vector) search and a developer-friendly REST API.
- **API Documentation:** https://www.meilisearch.com/docs/getting_started/overview
- **API Specification:** https://specs.meilisearch.dev/specifications/text/0118-search-api.html
- **SDKs/Libraries:** JavaScript, Python, Ruby, PHP, Go, Java, Swift, Rust, Dart — listed at https://github.com/meilisearch/meilisearch
- **Rust SDK:** https://docs.rs/meilisearch-sdk
- **Standards:** REST/JSON; OpenAPI-compatible interface documented at https://bump.sh/doc/meilisearch; sitemaps.xml ingestion for crawler mode
- **Authentication:** Bearer token (Authorization: Bearer <master-key>); scoped search-only keys for frontend use

### Elasticsearch

- **Description:** Distributed search and analytics engine. The dominant choice for large-scale enterprise search deployments; offers full-text, vector (kNN), and hybrid search.
- **API Documentation:** https://www.elastic.co/docs/api/doc/elasticsearch/
- **REST API Reference:** https://www.elastic.co/docs/reference/elasticsearch/rest-apis
- **SDKs/Libraries:** Python, JavaScript/Node.js, Java, Go, Ruby, PHP, .NET, Rust — https://www.elastic.co/guide/en/elasticsearch/client/index.html
- **Standards:** REST/JSON; NDJSON bulk format; OpenAPI spec partially available; TLS + Basic Auth / API Key / PKI certificate; supports OAuth 2.0 via Elastic Security
- **Authentication:** API Keys, Basic Auth, PKI; Elasticsearch Security with role-based access control (RBAC) for index-level permissions

### OpenSearch

- **Description:** Apache 2.0-licensed Elasticsearch fork maintained by AWS and the open-source community. API-compatible with Elasticsearch OSS. Provides vector search via the k-NN plugin.
- **API Documentation:** https://docs.opensearch.org/latest/api-reference/
- **Vector Search API:** https://docs.opensearch.org/latest/vector-search/api/index/
- **OpenAPI Spec Repository:** https://github.com/opensearch-project/opensearch-api-specification
- **SDKs/Libraries:** Python, JavaScript, Java, Go, Ruby, .NET — https://opensearch.org/docs/latest/clients/
- **Standards:** REST/JSON; NDJSON bulk; gRPC (v3.2+); HNSW/IVF for approximate nearest-neighbour vector search
- **Authentication:** HTTP Basic Auth, API Key; OpenSearch Security plugin for LDAP/SAML/OIDC federation and document-level security

### Vectara

- **Description:** Neural search platform with hallucination-resistant RAG (Retrieval-Augmented Generation). Designed for grounded answer generation from ingested corpora.
- **API Documentation:** https://docs.vectara.com/docs/
- **Query API Reference:** https://docs.vectara.com/docs/1.0/api-reference/search-apis/search
- **Quickstart:** https://docs.vectara.com/docs/developer-quickstart
- **Python SDK:** https://docs.vectara.com/docs/sdk/vectara-python-sdk
- **Standards:** REST/JSON; OAuth 2.0 for authentication; OpenAPI-compatible interface
- **Authentication:** OAuth 2.0 client credentials flow; JWT bearer tokens per corpus

### Glean

- **Description:** Enterprise AI search that unifies content across 100+ SaaS connectors (Confluence, Jira, Slack, Google Drive, GitHub) and enforces source-system permissions.
- **API Documentation:** https://developers.glean.com/
- **Search API:** https://developers.glean.com/api/client-api/search/overview
- **Indexing (Push) API:** https://developers.glean.com/api-info/indexing/getting-started/overview
- **SDKs/Libraries:** Python, TypeScript, Java, Go — https://developers.glean.com/
- **Standards:** REST/JSON; MCP-compatible (Glean ships an MCP server); framework-agnostic (LangChain, OpenAI Agents SDK, Google ADK compatible)
- **Authentication:** API token (Bearer); instance-name + token model; inherits source-system ACLs for permission-aware result filtering

### Kapa.ai

- **Description:** AI assistant trained on technical documentation, GitHub issues, Slack history, and Confluence; deployed as a website widget, Slack/Discord bot, or MCP server.
- **API Documentation:** https://docs.kapa.ai/
- **Standards:** REST API for index management; MCP server endpoint for agent integration; webhook integration for Slack/Discord
- **Authentication:** API Key; OAuth for Slack/GitHub integrations

### Mintlify

- **Description:** AI-native documentation platform with built-in search, API playgrounds, and AI assistant. Documentation-as-code with Git-based workflows.
- **API Documentation:** https://www.mintlify.com/docs
- **Developer Guide:** https://www.mintlify.com/use-cases/developer-documentation
- **Standards:** Markdown/MDX source; OpenAPI-driven API reference generation; MCP output support; REST-based analytics API
- **Authentication:** Team-based access; OAuth for GitHub/GitLab sync

---

## Embedding Model APIs (Semantic Search Infrastructure)

Semantic search in documentation products relies on text embedding APIs to convert queries and passages into dense vectors for nearest-neighbour retrieval.

| Provider | API Docs | Key Models | Pricing |
|----------|----------|------------|---------|
| OpenAI Embeddings | https://developers.openai.com/api/docs/guides/embeddings | text-embedding-3-small (1536-dim), text-embedding-3-large (3072-dim) | $0.02/1M tokens (small) |
| Cohere Embed v3 | https://docs.cohere.com/reference/embed | embed-english-v3.0, embed-multilingual-v3.0 | Usage-based; input_type param separates query vs. document |
| Voyage AI | https://docs.voyageai.com/ | voyage-3, voyage-code-3 (code-optimised) | Usage-based; strong on code documentation |
| BGE (BAAI) — open-source | https://huggingface.co/BAAI/bge-large-en-v1.5 | bge-large-en-v1.5, bge-m3 (multilingual) | Free self-hosted |

---

## Notes

- **Hybrid search** (keyword BM25 + vector ANN) is the current architectural consensus for documentation search — no single transport standard has emerged; each engine implements its own blend parameter.
- **MCP as the integration layer**: The MCP specification is the strongest emerging standard for connecting documentation search to AI assistants. Building MCP server support from day one avoids proprietary plugin formats.
- **Permission-aware search** remains an area without a universal standard. Glean's connector model (inheriting source ACLs at index time) and Elasticsearch's document-level security (DLS) represent two different approaches; neither is codified in an open standard.
- **DocSearch compatibility**: Typesense and Meilisearch both implement partial compatibility with the Algolia DocSearch scraper configuration format, giving open-source projects a migration path away from Algolia dependency.
