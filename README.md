# Developer Documentation Search

> Part of the [worlds-biggest-software-project](https://github.com/worlds-biggest-software-project) initiative.
>
> Semantic search across all internal and external developer documentation, returning cited answers rather than link lists.

Developer Documentation Search is an AI-native, open-source search layer for engineering teams. It unifies internal docs, API references, code, and external knowledge into a single, permission-aware index, designed for DX engineers, DevRel teams, and platform owners frustrated by the cost or quality of incumbent search tools.

---

## Why Developer Documentation Search?

- **Algolia gets expensive fast.** Pricing of $1 per 1K searches beyond the free tier means mid-market teams consistently overpay as their docs portals grow.
- **Enterprise search is overkill and opaque.** Glean ($7.2B valuation, $208M ARR) and Coveo target $100K+/yr enterprise contracts; smaller teams need a focused doc-search tool, not a full enterprise knowledge platform.
- **Confluence search is a recurring frustration.** Engineering managers cite poor in-tool search quality as a productivity blocker, with the global enterprise search market projected to reach USD 8.9 billion by 2026.
- **RAG-based answers are now expected UX.** Link-list results no longer meet developer expectations; semantic search and grounded answer generation are becoming table stakes.
- **Permission-aware search is still a gap.** Respecting source-system ACLs (OAuth 2.0 / OIDC) is a known blocker for enterprise adoption that not all incumbents handle cleanly.

---

## Key Features

### Core Search

- Full-text search across internal and external documentation
- Markdown and HTML parsing and indexing
- Sub-100ms search response targets
- Faceted filtering by product, language, and version
- Real-time indexing updates

### API & Code Awareness

- REST API documentation support
- API schema integration with OpenAPI and GraphQL
- Code example extraction and ranking
- Versioned documentation with fallback behaviour

### AI & Semantic Layer

- Semantic search that understands developer intent
- NLP-based query expansion and refinement suggestions
- Natural language question answering over the corpus
- Automatic documentation generation from code comments

### Platform & Operations

- Integration with major doc platforms (Markdown, GitBook) and internal sources
- Mobile-responsive search interface
- User management and search analytics
- Popular-query reporting for content teams

---

## AI-Native Advantage

Unlike incumbents that bolt AI onto a keyword index, this project is designed AI-first: heterogeneous sources (Confluence, GitHub, Notion, OpenAPI specs, Slack threads) are ingested into a single ranked answer surface with cited sources and page previews. Embeddings refresh automatically on commit, eliminating manual re-indexing. The system also detects documentation coverage gaps by identifying concepts developers search for but no page answers adequately, and offers a conversational "ask the docs" assistant that reformulates incomplete queries before retrieving results.

---

## Tech Stack & Deployment

Expected to support both self-hosted and managed deployment, in line with open-source incumbents like Typesense, Meilisearch, and OpenSearch. Relevant standards include OpenAPI/Swagger for API corpora, OpenSearch as a deployment target for enterprise internal search, RSS/Atom for changelog and blog ingestion, OAuth 2.0 / OIDC for permission-aware results, and pluggable vector embedding providers (OpenAI, Cohere, Voyage) given that embedding choice materially affects recall.

---

## Market Context

The global enterprise search market is projected to reach USD 8.9 billion by 2026, with over 70% of organisations citing it as critical for employee productivity. Pricing across incumbents ranges from free self-hosted (Typesense, Meilisearch) through usage-metered SaaS (Algolia at $1/1K searches) to enterprise contracts (Glean, Coveo at $100K+/yr). Primary buyers are DX engineers managing internal docs portals, DevRel teams publishing public API references, engineering managers dissatisfied with Confluence search, and platform teams owning the internal knowledge graph.

---

## Project Status

> This project is in the **research and specification phase**.  
> Contributions, feedback, and domain expertise are welcome.

---

## Contributing

We welcome contributions from developers, domain experts, and potential users.
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Important:** All contributions must be your own original work or clearly attributed
open-source material with a compatible licence. Copyright infringement and licence
violations will not be tolerated and will result in immediate removal of the offending
contribution. If you are unsure whether a piece of code, text, or other material is
safe to contribute, open an issue and ask before submitting.

---

## Licence

Licence to be determined. See [discussion](#) for context.
