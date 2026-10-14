# Data platforms, general assistants, process context, and agent identity

Research date: **14 October 2026**. Public documentation reviewed on that date; this is not a product benchmark. **D** = public documentation or disclosed implementation; **V** = vendor assertion; **I** = architectural interpretation; **U** = not established by the reviewed sources. Undated documentation is a live page, not a dated release commitment.

## Snowflake: business semantics, search, and tools

**D.** Semantic Views are database objects defining business entities, joins, facts, metrics, and dimensions. Their purpose includes expressing calculations consistently across analytics and AI. This is explicit business semantics, but it does not by itself define human assignments, contractual authority, or transaction lifecycles. [Semantic Views overview](https://docs.snowflake.com/en/user-guide/views-semantic/overview).

**D.** Cortex Agents combines SQL generation through Cortex Analyst, retrieval through Cortex Search, and extensible tools. The documentation describes persistent conversation threads, custom procedures/functions, MCP connectors, monitoring, and evaluations. Access depends on the request context **and each tool's execution context**. [Cortex Agents](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-agents).

**D.** Cortex Search combines vector retrieval, keyword retrieval, and reranking. Its searches execute with **owner's rights**; permission to query a service should not be mistaken for a fresh check against each caller's privileges on its underlying tables. This is a material difference from user-delegated document search. [Cortex Search](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-search/cortex-search-overview).

**I.** The natural work object is an analytical question grounded in governed data and definitions. A procurement application could use it to calculate spend and retrieve contract passages, while another application remains responsible for approvals and purchase orders. A graph database is unnecessary for many such joins and metrics. **U:** these sources do not establish a universal ontology spanning organizational roles, decisions, and transactions.

## Databricks: modeled semantics plus inferred context

**D.** Unity Catalog semantics includes Metric Views, business Domains, Pages, and certification/deprecation signals. These provide governed definitions and authority signals over data assets. [Unity Catalog semantics](https://docs.databricks.com/aws/en/uc-semantics/).

**D.** Genie Ontology is explicitly **Public Preview** in the documentation updated 11 September 2026. It combines modeled semantics with inferred snippets extracted from assets and usage. Snippets are ranked using authority, usage, and freshness and gated by Unity Catalog permissions. The described context is shared across Genie One and Genie Code. [Genie Ontology](https://docs.databricks.com/aws/en/genie/genie-ontology).

**V.** Databricks' 1 September 2026 implementation guidance recommends a deliberately curated core alongside inferred context, supported by entity resolution, metadata, trusted assets, governance, and evaluation. [Operationalizing Genie Ontology](https://www.databricks.com/blog/operationalizing-genie-ontology-your-data-stack).

**I.** This is a useful hybrid: authoritative definitions remain distinct from machine-inferred organizational knowledge. An authority score is a ranking signal, not a grant of decision-making power. **U:** the public pages do not establish formal OWL reasoning, a complete graph schema, the precision of inferred rules, or exact conflict-resolution guarantees. Preview context features should not be conflated with the maturity of all Unity Catalog features.

## ChatGPT in enterprise: execution, connections, and shared artifacts

**D.** Official OpenAI documentation describes ChatGPT Work tasks using authorized files, apps, and tools with cloud coordination and supported local/cloud execution. Connected accounts may be individual, shared, or agent-owned. Source changes and revocations can take time to propagate through synced apps; previously saved outputs have their own retention. Availability depends on workspace, plan, and rollout. [ChatGPT Work overview](https://learn.chatgpt.com/docs/enterprise/chatgpt-work-overview).

**D.** Plugin controls distinguish availability, skills, MCP-server access, allowed actions, external-service authorization, and runtime permissions. Installing a plugin does not grant an external account's authority. [Plugin controls](https://learn.chatgpt.com/docs/enterprise/apps-and-connectors).

**D.** ChatGPT Space provides shared pages/files and human-agent editing. Linked files retain original permissions, whereas copied or summarized content is visible to the page's audience. Private chats and saved memory are not shared merely by sharing a page. [Space](https://learn.chatgpt.com/docs/space).

**I.** The architectural starting point is a task and its artifacts, extended by tools and connections. Calling it a generic chatbot misses the execution and collaboration layers described in current documentation. **U:** these pages do not disclose a company-wide canonical business ontology or graph implementation. The existence of shared pages does not establish transactional co-ownership of a task across unrelated business systems.

## Claude enterprise search: a concrete federation model

**D.** The documented Ask Your Org experience searches connected services through MCP calls, returns citations, and does **not** index connected-service data externally for serving search queries. Users generally authenticate individually; custom connectors can instead use shared credentials, in which case access follows those credentials. Search conversations are private unless shared. [Use enterprise search](https://support.claude.com/en/articles/12489464-use-enterprise-search).

**I.** This is evidence against the claim that enterprise AI always requires a centralized knowledge database. Live federation can reuse source search and identity controls. Its limits include source API availability, search quality, query latency, and cross-source reconciliation. **U:** this feature-specific documentation should not be generalized to every Claude product's storage, execution, or memory architecture.

## Gemini Enterprise: connected search and agent access

**D.** Gemini Enterprise documentation covers organization search, assistants/agents, task execution, deliverables, administrative deployment, and developer APIs. [Product documentation](https://docs.cloud.google.com/gemini/enterprise/docs).

**D.** Custom Cloud Storage and BigQuery data sources require an access-controlled data store plus ACL metadata; identity-provider configuration maps the end user to permissions. These are explicit ingestion steps. [Custom-source access controls](https://docs.cloud.google.com/gemini/enterprise/docs/identity).

**D.** The Cloud Storage connector documentation warns that importing content does not import the source's Cloud Storage permissions automatically. It also distinguishes data-store modes with different ACL support. [Cloud Storage connector](https://docs.cloud.google.com/gemini/enterprise/docs/connectors/connect-cloud-storage).

**I.** Enterprise app access and source-document access are different controls. Connector mode matters as much as a vendor-wide security statement. **U:** these pages do not establish an explicit business ontology or identical access semantics across all connectors.

## Celonis: understanding the organization through events

**V.** Celonis describes its Process Intelligence Graph as combining an object-centric data model with a process knowledge layer: process events and business objects are enriched with the context of how work runs. Its announcement dates to Celosphere 2023. [PI Graph explanation](https://www.celonis.com/news/article/celonis-process-intelligence-graph-provides-a-common-language-for-enterprise-process-performance).

**V.** AgentC is positioned as tooling and integrations that expose Process Intelligence to agents built in other platforms as well as Celonis/partner agents. [Next 2025 announcement](https://www.celonis.com/news/press/celonis-showcases-latest-process-intelligence-and-ai-innovations-at-next-2025).

**I.** A process view contributes something a document corpus or employee directory cannot: observed sequences, waiting times, exceptions, and relationships between orders, invoices, shipments, and payments. It can reveal where a workflow stalls. Event correlations alone do not prove why a human made a decision, whether a shortcut was authorized, or how much unrecorded work occurred. **U:** the reviewed public material does not establish complete visibility into offline work or universal causal explanations.

## Workday: agents as governed organizational actors

**D.** Workday documents agent skills, tools, API resources, and Agent System of Record. Agents can be Workday-, partner-, or customer-built. [About Workday Agents](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/setup-considerations--agent-system-of-record.html).

**D.** Security differs by execution mode: delegate agents use the invoking user's security access, while ambient agents have their own permissions and a generated Ambient Agent Security Group that must be granted relevant access. [Security policies for agent skills](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/agent-security/configure-security-policies-for-agents.html).

**V.** The product page positions Agent System of Record as a directory, governance, and analytics hub for the agent workforce, including third-party registration through Agent Gateway. [Agent System of Record](https://www.workday.com/en-us/ai-platform/agent-system-of-record.html).

**I.** The important ontology expansion is from people alone to accountable actors: human sponsors, agent identities, skills, grants, and activity. Registration and monitoring do not, by themselves, prove enforcement inside every third-party runtime. **U:** cross-platform enforcement coverage and the completeness of external action logs require deployment-specific verification.

## Formal ontology versus operational modeling

**D.** OWL 2 defines a formal language with classes, properties, individuals, and logical semantics. SHACL separately defines validation of RDF data against shapes and produces conformance reports. [OWL 2 Primer](https://www.w3.org/TR/owl2-primer/); [SHACL](https://www.w3.org/TR/shacl/).

**I.** Neither is necessary for every enterprise AI application. A typed relational schema and validated APIs can implement useful domain semantics. Formal ontologies become attractive when interoperable vocabularies, inference, and cross-system constraints justify their cost. A graph used internally for nearest-neighbor indexing is not evidence that the product maintains business entities and relationships. A workflow graph expresses execution order, not necessarily domain meaning. A vendor's use of the word ontology should therefore trigger inspection of the exposed primitives, not assumptions about RDF or a particular graph database.

## Comparative implications

| Starting point | Products examined | Context that becomes first-class | Integration question |
|---|---|---|---|
| Governed analytics | Snowflake, Databricks | Entities, joins, definitions, trusted assets | Who owns the meaning of each metric? |
| Connected task/assistant | ChatGPT, Claude, Gemini Enterprise | Sources, conversations/tasks, files, tools | Which identity retrieves and which audience receives output? |
| Observed business execution | Celonis | Objects, events, process context | Which work is missing from the event record? |
| Agent workforce governance | Workday | Agent, skill, permissions, activity | Is control enforced where an external action actually occurs? |

These are analytical classifications, not mutually exclusive product categories or completeness scores. Every cited URL above was opened or retrieved during the research; product claims remain bounded by the feature documented on that page.
