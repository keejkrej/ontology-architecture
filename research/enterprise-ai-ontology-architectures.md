# Enterprise AI ontology architectures

**Research date: 14 October 2026.** A comparative study of how enterprise AI products represent knowledge, organizations, shared work, and authority to act.

## Findings

Enterprise AI products share a broad pattern: **connect to organizational information, select relevant context, reason about a task, produce or change an artifact, and feed the outcome back into work**. But their differences go well beyond input and output. The decisive choices are what they treat as a durable business object, where authoritative state lives, how knowledge becomes trusted, and who can authorize a change.

The evidence supports five conclusions:

1. **An ontology is a model of meaning; it is not synonymous with a vector database or RAG.** Some products expose configurable business objects and actions. Others primarily model documents, people, conversations, metrics, or domain-specific work. These can coexist in one architecture.
2. **Organizational understanding requires several kinds of context.** Formal structure, business entities, observed activity, current tasks, and policies answer different questions. An employee directory cannot tell an agent whether a contract exception was approved. A message mentioning an employee cannot grant that employee authority.
3. **Vertical products encode a unit of work.** Legal matters, contract reviews, procurement requests, support cases, and financial investigations need different state, evidence, tools, and completion criteria. Their differentiation is substantially about domain workflow and review, not only specialized prompting.
4. **Multiplayer AI requires explicit sharing semantics.** Shared assistant configurations, shared conversations, shared editable artifacts, and shared operational tasks are distinct. Retrieval permissions and the audience of a generated output are also distinct.
5. **Large-scale deployment is a distributed systems and organizational design problem.** Retrieval quality matters, but so do identity mapping, freshness, ownership, durable execution, integration contracts, human intervention, and cost per completed outcome.

These conclusions are **analytical synthesis**, supported by the product evidence below and the companion research notes. They are not claims that every vendor implements the proposed architecture.

## Scope and evidence

The study samples enterprise platforms, collaboration products, vertical agents, analytics platforms, and infrastructure. It prioritizes technical documentation, vendor engineering disclosures, protocol specifications, and official product material. It does not estimate market share or independently benchmark product quality.

Evidence labels throughout the research:

| Label | Meaning | What it establishes |
|---|---|---|
| **D — documented** | Public technical documentation, specifications, or first-party engineering disclosure | A documented capability/design, not independent verification of a live customer deployment |
| **V — vendor claim** | Official product page, announcement, or case study | The vendor's stated behavior or positioning; outcome claims need independent validation |
| **I — interpretation** | Our comparison, inference, or proposed architecture | An explanatory model, not a discovered proprietary schema |
| **U — unknown** | Not established by sources reviewed | An evidence gap; not proof of missing functionality |

Dynamic pages were reviewed on the research date. Specific beta/preview labels and dated disclosures are retained where material. Availability varies by edition, region, configuration, connector, and rollout. Product categories overlap; their placement describes the documented architectural starting point rather than the entirety of the product.

Companion evidence: [enterprise platforms](enterprise-platforms.md), [vertical agents](vertical-agents.md), [collaboration and infrastructure](collaboration-infrastructure.md), and [data platforms and assistants](data-platforms-and-assistants.md). [Source index](sources.md) lists the cited URLs.

## 1. A vocabulary that makes the market comparable

| Concept | What it represents | Enterprise example | What it does not supply by itself |
|---|---|---|---|
| Document store / knowledge base | Files, pages, messages, structured records | Contract PDFs and procurement policies | Reliable entity identity or workflow state |
| Search index | A searchable projection of source content | Keyword index, embeddings, metadata filters | A business model or authorization to act |
| RAG | Retrieval used to ground generation | Retrieve renewal clauses before drafting a brief | Guaranteed truth, complete recall, or a shared task |
| Knowledge graph | Entities connected by typed relationships | Supplier → contract → business unit | Correctness of extracted edges or formal reasoning |
| Ontology / domain model | Types, meanings, relationships, sometimes constraints | Supplier, agreement, approver, owns, supersedes | Necessarily a graph database or RDF implementation |
| Semantic metrics layer | Canonical definitions and calculation rules | Recognized revenue versus bookings | Full operational behavior of a business |
| Workflow graph / state machine | Execution stages and transitions | Review → approve → create order | Knowledge about the business outside that workflow |
| Agent memory | Persisted context at a chosen scope | A user's preferences; a task's previous attempts | An authoritative organization-wide fact store |
| Organization model | People, teams, roles, responsibilities, work relationships | Who operates a service and who approves spend | Permission inferred merely from proximity or popularity |
| Action / capability model | Typed operations and their permitted conditions | Create purchase order for an approved request | A guarantee of success or a completed transaction |

The examples and distinctions are **I**. For formal terminology, OWL 2 defines classes, properties, individuals, and logical semantics; SHACL provides RDF constraint validation. Commercial products can use useful domain models without either standard. [OWL 2 Primer](https://www.w3.org/TR/owl2-primer/); [SHACL](https://www.w3.org/TR/shacl/).

Two easy mistakes matter. A nearest-neighbor algorithm can use a graph internally without maintaining a business knowledge graph. And a diagram of agents passing messages is an execution topology, not necessarily an ontology. Ask what the nodes and edges **mean**, how they are created, and which interfaces expose them.

## 2. Architectural families in the market

This classification is **I**; product-specific evidence is linked in the market comparison and notes.

| Family | Architectural starting point | Typical output | Main architectural question |
|---|---|---|---|
| Connected assistants | Conversation/task + authorized sources and tools | Answer, report, edited file, tool result | What context and identity does this run have? |
| Enterprise knowledge platforms | People/content/activity relationships + retrieval | Organizational answer, discovery, reusable agent | Which source and person should be trusted for this question? |
| Operational ontology platforms | Typed business objects + relationships + actions | Analyzed and changed business state | Which business object changes under which rules? |
| Systems of record with agents | CRM, ITSM, HR, ERP objects and workflows | Record update or completed service process | How does the agent inherit existing process authority? |
| Vertical work platforms | Matter, contract, request, case, investigation | Domain artifact and workflow completion | What counts as correct, reviewable professional work? |
| Analytics/context platforms | Tables, metrics, governed definitions, inferred context | Query result, analysis, analytical action | Which definition, grain, and source govern the answer? |
| Collaboration surfaces | Channel, page, issue, shared conversation | Shared artifact, handoff, assigned work | Who can see, edit, steer, and approve the work? |
| Graph/process infrastructure | Graph schema, assertions, events, provenance | Context and relationships for other applications | How is organizational meaning maintained over time? |

These are complementary layers as often as competing products. An enterprise might use a knowledge platform for discovery, a legal product for review, an ERP for transactions, and a data platform for analytics. The integration problem is the preservation of identity, evidence, state, and authority across them.

### Representative market comparison: 23 products

This is a purposive architectural sample, not an exhaustive vendor directory. The “reading” column is **I**. The evidence column carries **D/V** labels; source notes contain additional capabilities and limitations. “Not established” means unknown from this research, not absent from the product.

| Product | Publicly described foundation | Architectural reading and main boundary |
|---|---|---|
| **Palantir Foundry / AIP** | **D:** configurable object/link types, functions, and action types. [Ontology](https://www.palantir.com/docs/foundry/ontology/overview) | Explicit operational ontology. Ontology edits and external side effects have different transaction boundaries. |
| **Glean** | **D:** content, people, and activity connected in a Knowledge Graph. [Knowledge Graph](https://docs.glean.com/security/knowledge-graph) | Organizational discovery and relevance extended into agents. Complete inferred schema and ranking logic are not public here. |
| **Microsoft 365 Copilot / Work IQ** | **D:** Graph resources, contextual tools, and persistent workspaces for agent work. [Work IQ](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/) | Workplace context connected to existing applications; domain transaction meaning still needs mapping. |
| **Salesforce Agentforce / Data 360** | **D:** source objects, harmonized objects, unified identities, and calculated insights. [Object model](https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-object-model.html) | Customer and process semantics close to CRM actions. Customer identity and execution identity must remain distinct. |
| **ServiceNow** | **D:** graph schemas use tables, properties, and relationships to provide agent context. [Knowledge Graph](https://www.servicenow.com/docs/r/intelligent-experiences/knowledge-graph/exploring-knowledge-graph.html) | Service and workflow state supply operational meaning; external data and run-as identity require explicit configuration. |
| **Snowflake Cortex** | **D:** semantic views model entities, joins, facts, metrics, and dimensions. [Semantic Views](https://docs.snowflake.com/en/user-guide/views-semantic/overview) | Governed analytics plus search/tools; an analytical model alone does not specify business approval state. |
| **Databricks Genie** | **D:** Unity Catalog semantics provides metrics, domains, pages, and trust signals. [Catalog semantics](https://docs.databricks.com/aws/en/uc-semantics/) | Curated business meaning plus inferred context through Genie Ontology, which is Public Preview in reviewed docs. |
| **Celonis** | **V:** object-centric process data enriched with process knowledge. [PI Graph](https://www.celonis.com/news/article/celonis-process-intelligence-graph-provides-a-common-language-for-enterprise-process-performance) | Observed work sequences complement document knowledge. Event records do not establish all human intent. |
| **Workday** | **D:** agent skills, tools, and Agent System of Record. [Agents](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/setup-considerations--agent-system-of-record.html) | Treats agents as governed actors. Directory visibility is different from enforcement in a third-party runtime. |
| **ChatGPT Enterprise / Work** | **D:** tasks use authorized files, tools, and connected accounts, under workspace/runtime controls. [Work overview](https://learn.chatgpt.com/docs/enterprise/chatgpt-work-overview) | General execution and artifact creation; a complete business ontology is not disclosed in these sources. |
| **Claude enterprise search** | **D:** MCP-based live searches with citations and no external search indexing for this feature. [Enterprise search](https://support.claude.com/en/articles/12489464-use-enterprise-search) | Federation demonstrates that enterprise knowledge access need not start with a copied corpus. |
| **Gemini Enterprise** | **D:** connected organization search, agents, and deliverables. [Documentation](https://docs.cloud.google.com/gemini/enterprise/docs) | Search/agent platform; connector and data-store modes determine access semantics. |
| **Harvey** | **D:** parallel rule-review workers use branches of a versioned document model, with conflict reconciliation. [Playbook review](https://www.harvey.ai/blog/rebuilding-playbook-review-as-a-multi-agent-system) | Domain work product and review state are central; this does not establish a general business graph. |
| **Legora** | **V:** Lists adds source-linked items, status, and assignees to legal collaboration. [Lists](https://legora.com/blog/introducing-lists) | Matter context becomes inspectable shared work, alongside its documented retrieval infrastructure. |
| **Lio** | **V:** purchasing execution over existing ERP systems, which remain authoritative. [ERP execution](https://www.lio.ai/newsroom/enterprise-systems-aren-t-the-bottleneck-manual-execution-is) | Procurement procedure and authority connect intent to transactions. Retry and consistency guarantees remain unknown. |
| **Zip** | **V:** specialized agents operate at nodes in procurement approval processes. [Procurement orchestration](https://zip.com/blog/introducing-agentic-procurement-orchestration) | The visible workflow coordinates departments and automation; published autonomy forecasts are not measured outcomes. |
| **Ironclad** | **D:** contract records, properties, workflow roles, review, signature, and archive stages. [Product definitions](https://legal.ironcladapp.com/fy2026-product-descriptions) | An existing contract lifecycle supplies the domain state AI works within. |
| **Sierra** | **V:** customer context and memory span interactions and system-of-record history. [Context Engine](https://sierra.ai/product/context-engine) | Customer identity and service outcomes drive the model; exact identity-resolution rules are not disclosed here. |
| **Decagon** | **V:** Agent Operating Procedures express service behavior, with engineering-owned code/versioning. [AOPs](https://decagon.ai/product/aop) | Procedures and escalation boundaries guide execution; a natural-language procedure is not proof of deterministic correctness. |
| **Hebbia** | **V:** Matrix exposes decomposed analytical work in an inspectable grid. [Matrix](https://www.hebbia.com/blog/introducing-matrix-the-interface-to-agi) | Evidence-linked analytical artifacts support human verification; research is distinct from committing a financial decision. |
| **Atlassian Rovo / Teamwork Graph** | **D:** common work-item, document, message, user, group, and project objects. [Teamwork Graph](https://developer.atlassian.com/platform/teamwork-graph/what-is-teamwork-graph/) | Work relationships enrich retrieval; a shared issue need not imply a shared agent session. |
| **Notion Custom Agents** | **D:** recurring/event-driven workflows over selected resources and tools. [Custom Agents](https://www.notion.com/help/custom-agents) | A shared actor over a workspace; resource permissions belong to the agent separately from its callers. |
| **Slack agents** | **D:** agent interactions can occur in channels or individual conversations. [Slack agents](https://slack.com/help/articles/33076000248851-Work-with-AI-agents-in-Slack) | Conversation is the collaboration surface; third-party agent semantics and retrieval audience still matter. |

Several additional boundaries change how this map should be read. **D:** Palantir's action atomicity covers ontology edits, not external side effects. Salesforce's native multi-agent feature has narrower limits than its broad architecture guidance. Microsoft's connector overview contains ambiguous read/write rollout language. ServiceNow distinguishes invocation access from execution identity. These are concrete reasons to compare feature-specific behavior rather than platform slogans. [Palantir consistency](https://www.palantir.com/docs/foundry/action-types/consistency-guarantees), [Salesforce limits](https://help.salesforce.com/s/articleView?id=ai.agent_multi_orch_consider.htm&language=en_US&type=5), [Microsoft connectors](https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/overview), [ServiceNow security](https://www.servicenow.com/docs/r/intelligent-experiences/aia-security-implementation.html).

## 3. What it means for AI to understand an organization

The following model is a **proposal**, not a schema attributed to a vendor. It separates six views of the same organization.

**Formal organization.** People, teams, roles, legal entities, reporting lines, locations, employment dates, and delegations. HR and identity systems can be authoritative for particular fields. A line manager relationship is different from membership in an access-control group.

**Business entities.** Customers, suppliers, products, services, contracts, assets, accounts, matters, and orders. Resolve identities across systems while preserving original identifiers. The CRM's customer account and the ERP's billing entity may overlap without being interchangeable.

**Knowledge and evidence.** Documents, passages, claims, definitions, policies, versions, sources, and owners. A claim should retain where it came from, when it was observed, and whether it is extracted, asserted, verified, or superseded. A summary is a derivative artifact with an audience, not a replacement for its sources.

**Observed collaboration and process.** Who worked with whom, which artifacts were edited, which steps occurred, and where work waited. This helps discover expertise and route work. It should not silently convert activity into authority. Celonis illustrates the process angle by combining object-centric process data with a knowledge layer. **V:** [PI Graph](https://www.celonis.com/news/article/celonis-process-intelligence-graph-provides-a-common-language-for-enterprise-process-performance).

**Intent and active work.** Goals, tasks, owners, dependencies, deadlines, decisions, exceptions, blockers, and expected outcomes. This is the missing layer when an assistant can retrieve every document but cannot answer what the team is currently trying to finish.

**Normative authority.** Which policy applies, who may decide, who may execute, what must be reviewed, and which conditions invalidate an approval. Keep this separate from descriptive facts about what usually happens. A frequently repeated workaround does not become approved policy.

The resulting context is a permissioned, time-sensitive view, not an omniscient model. Informal commitments, undocumented decisions, and work outside integrated systems remain uncertain. Good organization understanding includes knowing when to ask a responsible person.

### A minimal shared model

| Record | Essential fields or relationships | Why it matters |
|---|---|---|
| Actor | Human/agent identity, sponsor, organization, lifecycle | Makes accountability explicit |
| Entity reference | Canonical ID, type, source-system IDs, merge history | Prevents inconsistent cross-system identity |
| Evidence / claim | Source/version/span, assertion, confidence, valid time, observed time, audience | Separates inference from authoritative facts |
| Work item | Objective, owner, participants, status, dependencies, success criteria | Lets humans and agents coordinate persistent work |
| Decision | Alternatives, chosen option, rationale/evidence, decision-maker, timestamp | Preserves why work changed direction |
| Action proposal | Typed operation, arguments, target version, expected effect, execution identity | Makes planned changes reviewable |
| Approval | Approver, authority basis, exact proposal/version, expiry, conditions | Prevents an old approval authorizing a changed action |
| Execution / outcome | Attempt, idempotency key, external receipt, resulting state, failure/compensation | Distinguishes intent from completed work |

This can be implemented with relational tables, a graph, an event log, or several stores. Choose storage by access patterns. An ontology is the agreement about meaning across those stores.

### How the organizational model is built and maintained

The following lifecycle is a **proposed design**. Four streams contribute different kinds of meaning: structured system records, human-authored definitions and policies, machine-extracted claims from content, and observed events. Preserve their differences rather than promoting every extracted sentence into authoritative state.

| Stage | Responsibility | Result |
|---|---|---|
| Define a bounded domain | Domain owner identifies important questions, entities, relationships, and decisions | Versioned vocabulary with explicit ownership |
| Map authoritative sources | Data stewards map source IDs, fields, units, time, and access rules | Traceable mappings; no accidental merging of incompatible concepts |
| Propose missing structure | Extraction suggests entities, links, claims, and definitions with evidence | Candidate assertions, carrying uncertainty and provenance |
| Resolve and accept | Rules and responsible people reconcile identity and contradictions | Accepted facts/definitions separated from unresolved hypotheses |
| Publish projections | Services build task-relevant indexes, graph views, metrics, and context | Several optimized views of common meaning |
| Handle change | Owners version schemas and mappings; pipelines process updates and revocations | Dependent indexes, summaries, caches, and tasks invalidated or refreshed |
| Correct and retire | Reviewers correct errors, supersede assertions, and remove expired knowledge | A maintained history with clear current applicability |

Not every fact needs manual review. Deterministic source mappings can be accepted automatically; low-impact inferred context can remain provisional. Decision rights and consequential policy changes need an authoritative acceptance path. Thresholds should depend on the consequence of error, not one global confidence score.

Avoid building a company-wide ontology before delivering value. Start with the identities and relations required by one cross-functional workflow. Expand when another task needs shared meaning. Conversely, do not make every agent invent its own definition of supplier, customer, approval, or completion. Versioned contracts between domain models make incremental expansion possible.

Graph, relational, document, and vector storage solve different access needs. Relational storage is effective for typed state and transactions; graph representations help traverse varying relationships; RDF/ontology tooling can support explicit interoperable semantics; text/vector indexes support discovery; event logs preserve change. Using several is reasonable if authority, lineage, and synchronization are explicit. “One knowledge database” is a product abstraction, not a required physical deployment.

## 4. RAG, graph retrieval, and direct querying

**Recommendation:** route by the question's structure; do not choose one retrieval technique for the whole enterprise.

| Question | Useful starting mechanism | Reason |
|---|---|---|
| “What does this clause say?” | Exact document lookup + passage retrieval | Wording and version matter |
| “Where is the travel policy?” | Keyword/vector hybrid search + authority/freshness signals | Wording varies; authoritative policy must outrank discussion |
| “Which suppliers depend on the same sanctioned parent?” | Entity resolution + typed relationship traversal + verified source data | Multi-hop identity and relationships dominate |
| “How much did we spend last quarter?” | Governed SQL / semantic metrics | Aggregation, currency, grain, and time boundaries matter |
| “What themes appear across these interviews?” | Broad retrieval and summarization; evaluate GraphRAG where useful | Coverage across the corpus matters |
| “Can this renewal proceed?” | Evidence + current transaction state + policy/authority checks | This is a decision/workflow problem |
| “Create the approved order” | Validated action API + transaction controls | Retrieval alone cannot complete the operation |

Graph retrieval can follow known relations; Microsoft Research GraphRAG also constructs and summarizes communities of extracted entities for corpus-wide questions. These are related but not identical uses of graphs. The extracted graph is not automatically an authoritative enterprise ontology. See the [GraphRAG evidence and tradeoffs](collaboration-infrastructure.md).

**D:** Neo4j's retrieval library combines vector/full-text search with graph queries; Stardog supports mapped virtual graphs and symbolic inference; LangGraph supplies checkpointed execution and human interrupts. These occupy different layers of the architecture and are not interchangeable end-user products. [Neo4j retrievers](https://neo4j.com/docs/neo4j-graphrag-python/current/user_guide_rag.html), [Stardog Virtual Graphs](https://docs.stardog.com/virtual-graphs/), [Stardog inference](https://docs.stardog.com/inference-engine/), [LangGraph persistence](https://docs.langchain.com/oss/python/langgraph/persistence).

Snowflake provides a documented example of combining semantic views with SQL generation and document search in an agent. Databricks documents combining governed semantics with inferred context snippets; Genie Ontology is Public Preview in the reviewed documentation. **D:** [Cortex Agents](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-agents); [Genie Ontology](https://docs.databricks.com/aws/en/genie/genie-ontology).

**Tradeoff:** graphs can improve relationship queries but add entity resolution, extraction, curation, update, and access-control work. Long context can help on bounded matters but does not remove freshness or authority problems. Fine-tuning may help task behavior but is not a substitute for live organizational state. Evaluate each against a simpler baseline on the actual workload.

### Centralize, federate, or combine

| Pattern | Benefit | Cost / limitation |
|---|---|---|
| Replicated/indexed corpus | Consistent cross-source ranking and predictable retrieval | Sync lag, deletion propagation, indexing expense, copied ACLs |
| Live federation | Source freshness and reuse of source APIs/access rules | Source latency, outages, rate limits, uneven search semantics |
| Hybrid | Index discovery metadata; fetch authoritative detail when needed | More identity mapping and consistency logic |

Claude's enterprise-search documentation explicitly describes live MCP searches without external indexing for that feature. Legora's engineering disclosure describes project-scoped hybrid keyword/vector indexes. Both are valid enterprise architectures with different workloads. **D:** [Claude enterprise search](https://support.claude.com/en/articles/12489464-use-enterprise-search); [Legora search](https://legora.com/engineering/scaling-search-for-legal-ai).

For a consequential action, a useful hybrid is to use indexed context to discover the target, then read current authoritative state before committing a write. This is a design recommendation, not a universal vendor behavior.

## 5. Why the vertical agents differ beyond input and output

The table is an **illustrative domain comparison**, not a claim about proprietary vendor schemas.

| Dimension | Legal work: Harvey / Legora | Procurement: Lio / Zip | Customer support: Sierra / Decagon | Financial analysis: Hebbia |
|---|---|---|---|---|
| Durable work unit | Matter, review, negotiation | Request, sourcing event, purchase | Case/conversation | Investigation, model, diligence workstream |
| Core evidence | Clauses, precedents, client facts, playbooks | Supplier facts, policies, budget, quotes, contracts | Policy, account state, order and service history | Filings, data rooms, spreadsheets, assumptions |
| State that matters | Document version, issues, review status | Approvals, supplier qualification, commitment status | Identity, resolution, escalation, completed actions | Source version, comparison cells, assumptions, reviewer state |
| Human role | Judgment, exceptions, client accountability | Budget owner, procurement, legal, finance | Escalation and exceptions | Assumption setting, verification, decision |
| Output | Advice, draft, redline, structured review | Purchase/sourcing outcome and system updates | Answer plus permitted resolution | Evidence-linked analysis and artifacts |
| Success test | Correct, supported, reviewable work | Correctly authorized purchase at acceptable effort/cost | Correct resolution without repeat contact | Accurate, traceable, useful analytical conclusion |

The common abstraction is **evidence → work state → judgment → authorized action → outcome**. But the domain objects, review rules, and tools are not interchangeable.

### Three revealing implementation examples

**Legora: matter structure shapes physical infrastructure.** Its September 2026 engineering account describes project/matter-scoped retrieval and migration to Turbopuffer namespaces, allowing dormant matters to behave differently from active ones. **I:** domain boundaries influence partitioning and cost, not just the interface. The ANN search graph should not be labeled a legal knowledge graph. **D:** [Scaling Search for Legal AI](https://legora.com/engineering/scaling-search-for-legal-ai).

**Harvey: connectors are governed capabilities.** Its October 2026 disclosures describe a registry of native/MCP integrations and runtime policy checks outside the model. The policy engine can allow, deny, or pause partner MCP tool calls, using maintained tool annotations and workflow history. **I:** legal context must be paired with enforceable action boundaries. **D:** [Connector Library](https://www.harvey.ai/blog/how-we-built-harvey-connector-library); [MCP Policy Engine](https://www.harvey.ai/blog/building-harveys-mcp-policy-engine).

**Lio: organizational context must become executable procurement procedure.** The reviewed official materials describe procurement execution in existing enterprise systems and Agent Operating Procedures designed with humans. **I:** a supplier summary is only an intermediate artifact; the work crosses request, review, approval, and transaction state. Lio's internal graph/storage schema is not publicly established by these sources. Details and links are in the [vertical-agent research](vertical-agents.md).

## 6. What “multiplayer AI” actually requires

Separate four patterns:

1. **Shared configuration:** teammates use the same prompt, skill, or agent template, with separate runs.
2. **Shared conversation:** teammates contribute to a common thread and see generated responses.
3. **Shared artifact:** people and agents edit the same document, table, canvas, or issue.
4. **Shared operational task:** people and agents have explicit assignments, dependencies, decision rights, handoffs, and a persistent completion state.

Multi-agent reasoning is orthogonal: several model workers can solve a task for a single person. Conversely, one agent can collaborate with several people. Neither pattern implies the other.

**D.** Glean Team chat, documented as beta, executes retrieval under each sender's permissions but makes the generated answer visible to all chat participants. Its documentation explicitly says it does not restrict responses to the group's common source access. This is a deliberate collaboration model, not evidence that underlying document ACLs are bypassed. [Team chat](https://docs.glean.com/user-guide/assistant/team-chat).

**D.** ChatGPT Space likewise distinguishes linked-file permissions from the audience of copied or summarized page content. [Space](https://learn.chatgpt.com/docs/space).

**D.** Other collaboration models differ materially: Notion Custom Agents use their own granted resource access, while Jira's documented agent workflow lets the initiating person review output before sharing it to the work item. Slack Real-time Search constrains retrieval by conversational audience and prohibits copying/storing its retrieved data. A shared workflow may persist its own state while retaining only source material that the integration permits. [Notion permissions](https://www.notion.com/help/custom-agents-sharing-and-permissions), [Jira agent collaboration](https://support.atlassian.com/jira-software-cloud/docs/collaborate-on-work-items-with-ai-agents/), [Slack Real-time Search](https://docs.slack.dev/apis/web-api/real-time-search-api/).

**Design implication:** maintain separate answers to “may this actor retrieve it?”, “may this group receive the derivative?”, and “may this actor execute the action?” A private draft, an explicit publish operation, or a tightly scoped shared workspace may be appropriate depending on the work.

For sustained collaboration, the work object should support ownership, versioned edits, pause/resume, attribution, private and shared context, explicit handoffs, notification, and an event history. Use optimistic concurrency or locking for state changes. Collaborative text merging can resolve simultaneous edits; it cannot decide whether two contradictory approvals are both valid. Human review needs the actual proposed change and evidence, not just a generic confirmation button.

## 7. A reference architecture for a large organization

The following is a **proposed composition** of the patterns observed, not a vendor diagram.

```text
People and business events
        │
        ▼
Work surface: conversation · document · case · shared task
        │
        ▼
Durable work service: ownership · state · decisions · history
        │                            ▲
        ▼                            │ outcomes / corrections
Agent runtime: plan · retrieve · use tools · pause · resume
        │                            │
        ├── Context service ──► search / graph / SQL / live APIs
        │        │
        │        └── Meaning + identity + evidence + time + source access
        │
        └── Action gateway ──► policy / approval / version checks
                                  │
                                  ▼
                        Systems of record and external services

Across every layer: scoped identities, audit, evaluation,
tenant boundaries, observability, lifecycle and cost controls
```

The context service assembles a task-specific view. It does not need to put the entire company in one model context window. The durable work service owns the business task beyond any individual model run. The action gateway validates operations against current policy and target state. Systems of record remain authoritative for their transactions unless ownership is deliberately moved.

Use a small common vocabulary—actors, entity references, work items, evidence, decisions, actions—and domain extensions. “Contract” in sales, procurement, and legal needs shared identity, but each domain can maintain additional semantics. A universal model with every department's fields is costly to change; disconnected models make cross-functional work brittle. Explicit mappings and versioned interfaces provide a middle path.

### Walkthrough: a supplier renewal crossing teams

This is a **hypothetical design scenario**, not a claim that the named products interoperate this way today.

1. A renewal event opens a persistent work item linked to the supplier, contract, owner, deadline, and source versions.
2. A procurement agent retrieves permitted terms and joins governed spend data. It records uncertainty about supplier identity rather than silently merging similar names.
3. Legal reviews a proposed clause change against the applicable playbook. Its output is a versioned artifact and a decision on specific issues.
4. Finance checks budget and approval authority. Discussion participants do not automatically become approvers.
5. A responsible human approves a specific proposal: supplier, amount, currency, term, legal entity, document version, and policy conditions.
6. Before writing to ERP, the executor verifies authority and current versions. A changed amount or document requires the appropriate new approval. Receiver-enforced idempotency, where supported, plus reconciliation of external receipts/state guards against duplicate retries. A locally generated key alone provides no such guarantee.
7. The workflow reconciles the external result, records the outcome, and surfaces any exception. Validated corrections can improve future retrieval or procedures; one user's edits do not silently become company policy.

The AI's contribution is not only drafting. It carries evidence and unfinished work across specialists without losing responsibility or state.

## 8. Identity, permissions, and delegated authority

Avoid the blanket claim that enterprise agents always act with the current user's permissions. Public documentation shows several models:

| Model | Concrete evidence | Deployment implication |
|---|---|---|
| User-delegated retrieval | Claude enterprise search ordinarily uses user authentication; custom shared credentials are an exception | Inspect the actual connector identity |
| Service-owner retrieval | Snowflake Cortex Search executes with owner's rights | Search-service access needs its own data-exposure design |
| Agent-owned authority | Workday ambient agents use agent security groups; delegate agents use the invoking user | Separate background agency from interactive delegation |
| Explicit imported ACLs | Gemini Enterprise custom sources require ACL metadata and access-controlled configuration | Source permissions may not transfer automatically |
| Shared-output audience | Glean Team chat exposes generated responses to chat participants | Source authorization and output disclosure are separate |

**D sources:** [Claude](https://support.claude.com/en/articles/12489464-use-enterprise-search), [Snowflake](https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-search/cortex-search-overview), [Workday](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/agent-security/configure-security-policies-for-agents.html), [Gemini](https://docs.cloud.google.com/gemini/enterprise/docs/identity), [Glean](https://docs.glean.com/user-guide/assistant/team-chat).

**Proposed controls:** identify the initiator, run principal, tool principal, target principal, approver, and output audience. Re-evaluate authorization when consequential writes occur. Preserve source/audience information in derived artifacts and graph assertions. Do not treat retrieved text as executable policy. An approval should bind to a typed operation and its exact relevant version; changes need revalidation.

MCP and A2A can standardize interfaces and delegation, but do not make business schemas, access policies, or transaction semantics consistent by themselves. An endpoint advertising a tool is not proof that a particular employee or agent may invoke it. Protocol-specific evidence is in the [infrastructure note](collaboration-infrastructure.md).

## 9. Scale, evaluation, and operations

“Large scale” has several independent dimensions: employees, documents, relationship edges, active tasks, external API calls, legal entities, policy variations, and simultaneous edits. A successful demo rarely exercises all of them.

**Recommended engineering priorities:** use incremental ingestion and deletion; partition by meaningful tenant/domain boundaries; track source freshness; bound retrieval and model loops; apply backpressure to external services; persist work before waiting for people; and reconcile incomplete writes. Distinguish a failed API response from a failed business operation—an order may have been created before a timeout.

**D.** Legora's evaluation disclosure snapshots a legal matter's documents, database records, permissions, and storage state into reproducible environments, using durable orchestration for long-running evaluations. **I:** test the environment and workflow, not just isolated prompt answers. [Legal-agent eval infrastructure](https://legora.com/engineering/building-scalable-evals-infrastructure-for-legal-agents).

| Evaluation layer | What to measure | Example failure case |
|---|---|---|
| Data/context | Freshness, entity-match precision, source authority, denied-data exposure | Two suppliers merged incorrectly |
| Retrieval | Relevant-source recall, citation support, coverage | A newer amendment omitted |
| Reasoning/artifact | Correctness against domain rubric, calibrated uncertainty, reviewer correction effort | Unsupported legal conclusion |
| Work coordination | Handoff success, ownership clarity, completion after interruption | Two agents work from incompatible versions |
| Actions | Correct arguments, current authority, resulting external state, duplicate prevention | Retry creates a second purchase |
| Collaboration | Correct audience, attribution, edit conflict behavior | Private context copied into a broad channel |
| Business outcomes | Completion rate, cycle time, rework, service quality, user effort | Faster first response but more escalations |
| Economics | Total cost per accepted outcome and human attention | Cheap generation followed by expensive review |

This evaluation framework is a **proposal**. Build cases from real tasks with appropriate access, then include ambiguity, missing evidence, stale policies, permission revocation, interruption, conflicting edits, and partial external failures. Preserve human-reviewed reference decisions and compare against the current process. Model-based judging can help triage but should not be the only judge of consequential domain outcomes.

A useful cost model is:

```text
cost per accepted outcome =
  (model + retrieval + indexing + runtime + integration + human review + rework)
  / accepted completed outcomes
```

Also track review minutes and pending approvals. Adding parallel agents can reduce elapsed time while increasing spend, repeated retrieval, and merge effort. Use parallelism for separable work; serialize dependent decisions and commits.

## 10. Deployment sequence and organizational ownership

This is a **recommended rollout**, with gates rather than invented universal timelines.

| Stage | Scope | Evidence needed to expand |
|---|---|---|
| 1. Bounded discovery | One workflow, named owner, explicit source set | Baseline completion time, failure modes, trusted references |
| 2. Grounded assistance | Retrieval and drafts, no autonomous commitments | Source quality, useful artifacts, manageable correction effort |
| 3. Shared work | Persistent tasks, handoffs, reviewable changes | Clear ownership, audience controls, reliable resumption |
| 4. Controlled execution | Typed actions and scoped delegation | Correct writes, current authority, retry/recovery behavior |
| 5. Cross-domain expansion | More systems, teams, and agent specialists | Stable identity mappings, interfaces, evaluations, operating costs |
| 6. Bounded autonomy | Selected repeatable tasks with exception handling | Sustained outcome quality, accountable owner, reliable rollback/escalation |

The operating model matters as much as the software. Domain owners define meanings and acceptable outcomes. Data stewards maintain source authority and identity quality. Platform teams operate integration, identity, observability, and execution. Workflow owners own exception handling and human review capacity. A model team cannot decide, on its own, what “approved supplier” or “final legal review” means for the company.

**Buy versus build:** buy common infrastructure and well-matched vertical workflows where possible; retain control over organization-specific definitions, integrations, decision rights, and evaluation datasets. A product's attractiveness depends on which layer it replaces and which obligations remain with the customer. Connector count alone is a poor proxy for integration depth.

## 11. Architectural opportunities and open questions

These are **research hypotheses**, not proven market gaps or investment recommendations.

**Shared work may be a more valuable integration boundary than shared chat.** A portable task with entity references, evidence, decisions, and typed proposed actions lets specialists participate without requiring identical model runtimes. Its challenge is making state and authority semantics agree across products.

**Organizational memory needs provenance and maintenance.** Useful memory captures decisions, validated exceptions, expertise, and unresolved questions. It needs owners, expiry/review, correction, and scope. A larger pile of saved summaries can amplify stale or unauthorized information.

**Context can be federated while meaning remains coordinated.** Organizations may keep transactions and documents in existing systems while sharing identifiers, definitions, and task state. The question is what must be centralized for consistency and what can remain domain-owned.

**The durable differentiator may be the domain feedback loop.** Evidence-linked corrections and accepted outcomes can improve workflows and evaluation. Mere usage volume does not prove a compounding advantage; the feedback must be relevant, permissioned, and accurately attributed.

**Authority and responsibility need to become inspectable.** Agent directories are emerging, but registration, monitoring, invocation rights, and enforcement at an external tool are separate capabilities. Workday's explicit distinction between delegate and ambient agent identities illustrates why this matters. [Agent security documentation](https://doc.workday.com/admin-guide/en-us/workday-ai/agents/agent-security/configure-security-policies-for-agents.html).

Unresolved by public materials: production quality under realistic cross-team workloads; full proprietary schemas; inference precision and revocation latency; cross-vendor approval portability; operational recovery guarantees; deployment-specific costs; and which announced features are enabled for a particular customer. The correct next validation is a representative end-to-end workflow with its actual data, participants, and systems.
