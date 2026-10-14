# Enterprise AI platforms: ontology, organizational context, and action architectures

Research date: **2026-10-14**. Scope: Palantir, Glean, Microsoft, Salesforce, and ServiceNow. This is a public-evidence comparison, not an implementation audit. Product documentation was accessed on the research date; publication/update dates are recorded when visible. Undated pages and search-engine crawl dates do not establish feature launch dates. Availability can differ by release, tenant, entitlement, and preview enrollment.

Evidence labels: **D** = official documentation or first-party technical explanation; **V** = vendor product/positioning claim; **I** = analysis inferred from the cited evidence; **U** = not established by the reviewed public evidence. D documents intended behavior; it does not independently verify operational performance.

## The distinctions that make the market legible

**I — Analytical vocabulary.** An ontology schema defines categories, properties, relationships, and sometimes permitted operations. A knowledge graph instance connects actual entities. A search index organizes retrievable content, including keywords or embeddings; similarity is not automatically a business relationship. A semantic metrics layer defines measures, dimensions, aggregation rules, and business meanings. Organizational context adds people, ownership, roles, projects, activity, and situations. An action/workflow layer changes state under authority. Products can combine these layers without implementing them in the same database.

**I — Core finding.** These platforms share the ambition of grounding AI in an organization, but differ in their starting point and resulting engineering burden. The useful question is which relationships and decisions are explicitly modeled, which are inferred, and which remain buried in documents or application code. Calling every substrate an “ontology” hides these differences.

| Platform | Documented center of gravity | Architectural interpretation (I) |
|---|---|---|
| Palantir | Business object/link types plus actions and functions. [P1] | Explicit operational domain modeling; applications and agents share a business interface. |
| Glean | Content, people, and activity connected in its Knowledge Graph. [G1] | Organizational discovery and relevance expanded into execution and shared work. |
| Microsoft | Microsoft Graph resources, semantic indexes, and Work IQ context/tools. [M1] [M4] | Workplace context and application operations spanning an existing productivity estate. |
| Salesforce | Harmonized/unified data objects, calculated insights, and agent actions. [S2] | Customer/process identity and CRM execution with a separate retrieval pipeline. |
| ServiceNow | Table-based graph schemas, relationships, contextual querying, workflow integration. [N1] | Service/employee operations enriched with semantic context and external data access. |

## Palantir: an explicit operational ontology

**D — Inputs and canonical model.** The Ontology maps datasets, virtual tables, and models into real-world concepts. Public primitives include object types, properties, link types, interfaces, action types, and functions. Examples include equipment, orders, and transactions; the organization defines its domain mapping. Interfaces describe common shapes/capabilities across object types. These are documented schema constructs, not a claim that every customer shares one universal enterprise schema. [P1]

**D — Retrieval.** Ontology-augmented generation documentation includes document chunks modeled as objects, embeddings, ranked keyword retrieval, query augmentation, and hybrid search. It recommends investigating retrieval when relevant evidence fails to reach the model and explicitly allows starting without search when the entire useful context fits. Ontology-based applications therefore still need retrieval engineering; the ontology does not eliminate RAG. [P2]

**D — Permissions.** Palantir separates permissions on ontology resources—the schema definitions—from permissions on actual objects and links. Seeing an object type's definition is conceptually different from accessing its records. This makes schema management and operational data authorization separate concerns. [P3]

**D — Actions.** Action types define coordinated object/property/link changes and associated side effects. Rules and parameters can constrain updates; the same action logic can be reused across applications. The documentation's employee reassignment example combines property changes, a manager relationship, validation, and notifications. Human decisions become persisted changes rather than remaining only in chat history. [P4]

**D — Human/agent collaboration.** AIP's architecture describes batch, streaming, and change-data-capture integration; action/workflow tracing; agent evaluation; and applications serving operators, engineers, and compliance teams. It places humans and agents within common change management and governance. **I:** This supports collaboration around shared business state, but is not evidence that every application offers a simultaneous multi-person chat or automatically resolves conflicting intentions. [P5]

**D — Concrete technical boundary.** Actions' all-or-nothing guarantee applies to ontology edits, not notifications, webhooks, or a function's external calls. Different isolation settings make different concurrency tradeoffs. New actions using batched writes default to snapshot isolation; staged writes have a different documented limitation. A graph-backed action is therefore not an atomic transaction across every connected enterprise system. [P6]

**I — Deployment consequence.** This architecture is attractive when correctness depends on named entities and governed transitions: allocating an asset, approving an order, or changing a plan. The implementation task is to decide authoritative sources, object identity, allowed transitions, ownership, and operational UI. Modeling these decisions is substantial work, even if an AI assists with construction.

**U — Public unknowns.** The reviewed documents do not establish a universal object-resolution algorithm, guaranteed cross-system freshness, or an automatic method for discovering an organization's informal policies. They also do not prove every customer's ontology is complete or correct. Metrics can be expressed through functions and applications, but that does not make “ontology” interchangeable with a standardized financial metrics catalog.

## Glean: a people/content/activity graph, then execution

**D — Canonical knowledge and organizational model.** Glean documents content such as documents, messages, and tickets; people identities, roles, teams, and organizational relationships; and activity such as interactions and document history. Its people layer consolidates identities across applications and represents collaborators and project involvement. Connectors extract content, metadata, permissions, and structure. **U:** This describes meaningful graph concepts but does not publish a complete graph schema, edge-confidence model, or graph storage implementation. [G1]

**D — Inputs and live access.** Its ingestion architecture distinguishes indexed unstructured/semi-structured content from tools that communicate directly with third-party systems, including dynamic warehouse retrieval. It explicitly says structured warehouse data need not be ingested into Glean's index. An additional context-provisioning route is marked upcoming on the reviewed page; it should not be assumed generally available. [G2]

**D — Retrieval substrate.** The processing pipeline combines source content, permission mappings, user information, and activity metrics into a tenant knowledge base. **I:** The organizational graph is a relevance/context layer over enterprise material, not evidence that every document statement becomes a validated symbolic fact or that search always traverses graph edges. Exact ranking weights and extraction quality remain **U**. [G3]

**V — Broader graph positioning.** A September 2025 announcement describes Enterprise Graph as company-wide knowledge plus personal graphs connecting projects, collaborators, work style, workflows, and applications. Treat this as the vendor's expanded product model; it is not an openly specified general-purpose ontology language. [G6]

**D — Permissions vary by surface.** Web-app agents use the invoking user's document access. Slack responses visible to an entire channel instead use a broad-access policy, including organizationally public content and recognized channel messages; documentation says it does not check every channel member's access to each document. Agent editor/viewer/owner permissions are a separate sharing system. [G4]

**D — Actions and human checkpoints.** Write tools can create/update external records and documents. Interactive web sessions default to confirmation; administrators and builders can authorize configured no-confirmation steps. Scheduled/background behavior differs, and an Agent Inbox can expose blocked approvals when enabled. Tool access and approval requirements are explicitly separate controls. **I:** A permission-aware search result does not itself authorize sending or modifying anything. [G5]

**D — Actual multiplayer behavior.** Team chat lets colleagues prompt in the same thread, co-create artifacts, and continue investigations. Each message retrieves using its sender's permissions, while all chat members can read answers already generated—even when they cannot open the underlying sources. Responses appear without a prior review step. Concurrent requests run serially; artifact editing follows chat access. The page contains beta qualifications. [G7]

**I — Deployment consequence.** Glean's main modeling advantage is organization-wide context assembled from existing knowledge-work systems. A critical implementation question is how derived outputs are shared: source authorization and answer visibility are different decisions. **U:** The reviewed material does not establish universal fact conflict resolution, transactional external writes, or guaranteed semantic coverage of every connector. Search quality and stale permissions still require connector-specific evaluation.

## Microsoft: workplace resources, retrieval, and Work IQ

**D — Canonical objects.** Microsoft Graph exposes resources including users, groups, files, messages, and calendar events, with relationships such as manager and group membership. It also exposes people/item relevance signals. **I:** It is a documented resource/API model across Microsoft services; the word “Graph” alone does not establish that every Copilot request performs knowledge-graph traversal or that Microsoft publishes its internal contextual inference graph. [M1]

**D — External inputs.** Synced Copilot connectors index external content into Microsoft Graph; federated connectors fetch it live through MCP. Synced items carry content, metadata, and ACLs. The overview distinguishes organization-configured connections from user-authenticated routes. **U — Rollout ambiguity:** The same page calls federated connectors read-only while noting writes starting early October 2026. A deployment should verify its specific connector/release instead of treating the date as proof of universal write support. [M2]

**D — Retrieval and limits.** Semantic indexing combines lexical and vector retrieval with Graph context and user access boundaries. Third-party connector content can enter that index. The reviewed support table excludes delegated/shared/archived mailbox content and archived SharePoint data; these are limits of the documented indexing path, not proof that no Microsoft product can access those resources. The page also distinguishes initial/new-content indexing from updates. **I:** “Connected” and “immediately retrievable” are not equivalent. [M3]

**D — Work IQ.** The September 2026 overview describes chat, assembled context, tools, and persistent workspaces; A2A, MCP, and REST interfaces; Microsoft 365 plus business/workflow data; and user-scoped operations. It documents policy checks using resource paths, request methods, identity, and content, with invocation logging. SharePoint Embedded workspaces hold intermediate data and outputs for longer-running tasks. **I:** This is an agent-facing workplace context/action service, not simply another name for a vector index. [M4]

**D — Human collaboration.** Copilot Pages turns generated responses into durable editable/shareable material inside a persistent canvas. This provides an explicit artifact for human co-authoring. **I:** Co-authoring an artifact, continuing a conversation, delegating to another agent, and approving an operation are separate collaboration capabilities; one should not infer all four from a Pages demo. [M5]

**I — Deployment consequence.** Microsoft can begin with an organization's existing workplace identities and collaboration estate. The architecture question becomes which relevant business state lives outside that estate, whether to index or fetch it, and how actions obtain authority. A sales approval, procurement exception, or legal matter will still require domain definitions and business logic even if its emails and documents are searchable.

**U — Public unknowns.** These sources do not expose the full Work IQ inferred-relationship schema, edge provenance, entity-resolution thresholds, or deterministic explanation of every ranking decision. The precise compatibility and availability matrix across custom agents, native experiences, connectors, and runtime versions needs feature-specific validation. Graph resources and a contextual retrieval service should not be mistaken for a complete enterprise metrics model.

## Salesforce: harmonized customer/process data and governed agent actions

**D — Inputs.** Data 360, called Data Cloud in older material and some interfaces, ingests Salesforce and external data through connectors, APIs, SDKs, and MuleSoft. Its documented zero-copy route federates read-only access to partner data. Structured ingestion, unstructured ingestion, federation, and action delivery are therefore different paths rather than one universal connector capability. [S1]

**D — Canonical objects and metrics.** Data Lake Objects retain ingested data; Data Model Objects harmonize it; Unified DMOs hold identity-resolved representations; Calculated Insight Objects represent multidimensional metrics. This is unusually explicit separation between source structures, common entities, and derived measures. **I:** A calculated customer lifetime value is not the same kind of semantic object as a relationship connecting two source identities. [S2]

**D — Identity relationships.** The identity-resolution explanation describes schema mapping, matching rules, and reconciliation rules. Matching determines records that represent the same person/business; reconciliation prioritizes competing attributes. The output links source representations into unified objects. **I:** “Unified” is a configured resolution result, not independent proof that the selected customer identity or preferred address is correct. [S3]

**D — Retrieval.** A first-party Agentforce grounding tutorial configures parsing/chunking, hybrid search, vector data objects, and a retriever returning URL, title, and chunks for citations. Index creation and retriever activation are separate steps. **I:** Identity resolution and document RAG solve different problems; a harmonized customer model does not remove document retrieval tuning. [S4]

**D — Actions and permissions.** Custom actions can reuse Apex, flows, and prompt templates. [S5] Employee agents normally run under the authenticated user's permissions; external service agents often use a dedicated agent user. Salesforce expressly warns that customer-identifying context variables do not change the permission identity governing access. Authenticated Experience Cloud configurations can differ. This is a material distinction when building customer-facing retrieval and actions. [S6]

**D — Human/agent coordination.** Agent Script documentation distinguishes handing conversational control to a subagent from keeping a supervisor responsible for the conversation. It also describes configurable escalation to a human representative, including fallback behavior when routing fails or queues are offline. **I:** Human handoff is a modeled runtime transition, not merely placing a human somewhere in the product story. [S7]

**D — Architecture versus shipping scope.** Salesforce Architects describes same-org, multi-org, and multi-vendor orchestration patterns. [S8] However, the feature-specific limitations reviewed restrict native multi-agent orchestration to same-org Agentforce agents, one delegation level, 120-second orchestrator and 30-second subagent timeouts, and no supported Voice configuration. **I:** The broad architecture patterns must not be reported as blanket availability of the native feature. [S9]

**I — Deployment consequence.** Salesforce's advantage is proximity to customer records, application metadata, process state, and existing automation. It still requires explicit mapping from customer identity to permitted objects and actions, particularly for external users. **U:** The reviewed evidence does not establish automatic permission equivalence across every Data 360 index, custom Apex/Flow implementation, and external system, or guaranteed compensation for partially completed external workflows.

## ServiceNow: service/workflow state plus a graph and data fabric

**D — Canonical graph.** Knowledge Graph schemas model nodes as tables, properties as columns, and relationships as edges. Administrators configure them through a designer and can inspect queries visually. Integrations supply employee context, natural-language structured queries, slot filling, and graph retrieval to agents. **I:** This is an explicit semantic schema over operational entities; it does not imply every relationship is extracted automatically from unstructured text. [N1]

**V — Operational organization model.** ServiceNow's technical blueprint emphasizes CSDM, CMDB, services, digital assets, people, locations, contracts, and issues, linking operational state with ownership and dependencies. **I:** The architecture's organizational understanding is especially concrete where work is already represented by service dependencies and managed records. The blueprint is a vendor architecture narrative, not proof that a customer's CMDB is complete or current. [N2]

**D — External inputs.** Zero Copy Connector documentation lists supported systems such as Snowflake, Databricks, BigQuery, Oracle, SAP, and remote ServiceNow instances, with release compatibility. Some connectors are explicitly preview-scoped. [N3] A first-party technical explanation describes virtual data-fabric tables and a SQL query engine that requests external data as needed without persisting that retrieved data in ServiceNow. **I:** Query federation is distinct from copying the source into an enterprise knowledge database. [N4]

**D — Retrieval and workflow meaning.** The graph's natural-language examples include finding a manager, an incident's status, or assigned assets. It can operate over data-fabric tables and supply facts/relationships to follow-up tasks. [N1] **I:** This complements retrieval from prose: “my asset” and “service affected by this component” require identity and operational relations that a document similarity score cannot establish alone.

**D — Permissions and human controls.** Agent security separates invocation ACLs from the identity used during execution. Downstream ACL checks use the preceding component's run-as identity. Role masking narrows roles for dynamic users but does not apply in the same way to dedicated AI users. Supervised tool mode requires human approval before execution. This is richer than asserting that every agent simply inherits the current person's rights. [N5]

**D — A concrete deployment limit.** The reviewed domain-separation support matrix lists Workflow Data Fabric Hub/Zero Copy Connectors as having no support. **I:** Large organizations using domain separation should validate this exact product boundary rather than assume all platform isolation features apply uniformly. This does not mean the feature has no ACLs or security controls. [N6]

**I — Deployment consequence.** ServiceNow provides a practical path when AI should change an existing process: resolve an incident, route an employee request, or coordinate service work. Human collaboration can revolve around records, approvals, assignments, and escalations. Those are different interaction primitives from several employees sharing one AI chat.

**U — Public unknowns.** The reviewed sources do not specify one universal ontology spanning every external warehouse, a general entity-resolution method across all connected systems, graph query coverage for every application, or cross-system transaction guarantees. They also do not establish that AI can reconstruct informal authority or exceptions absent from records and workflow definitions.

## Implications for a large organization

**I — A useful deployment unit is a decision/process, not the entire company at once.** Define the entities, sources of evidence, permitted transitions, human owners, and required outcomes for one workflow. Then decide which shared platform layers it needs. Organization-wide search can deliver broad value, but high-consequence actions demand a more explicit domain model.

**I — “Multiplayer” needs several state models.** At minimum distinguish agent definition, shared conversation, generated artifact, business record, and execution. Each needs identity, permissions, ownership, history, and conflict behavior. Glean's documented answer visibility and Palantir's documented transaction boundary illustrate why a single “permissions-aware” label cannot settle the design.

**I — Scale depends on preserving authority and evidence through transitions.** For any candidate workflow, test: whose identity retrieved each fact; which version/source supports it; who can see the derived output; who can approve it; which identity executes; what happens after partial failure; and how another person resumes work. These are architectural acceptance tests, not substitutes for domain-specific accuracy evaluation.

## Compact source register

All sources were accessed 2026-10-14. “n.d.” means no reliable publication/update date was captured. Dates describe the page, not an inferred product release. Linked IDs resolve directly to primary sources.

| ID | Primary source and date observed |
|---|---|
| [P1] | Palantir, Ontology building; n.d. |
| [P2] | Palantir, Ontology-augmented generation; n.d. |
| [P3] | Palantir, Object permissioning overview; n.d. |
| [P4] | Palantir, Action types; n.d. |
| [P5] | Palantir, AIP architecture; n.d. |
| [P6] | Palantir, Consistency and isolation; n.d. |
| [G1] | Glean, Knowledge Graph; updated 2026-09-29. |
| [G2] | Glean, Data ingestion flow; n.d. |
| [G3] | Glean, Data processing flow; updated 2026-09-29. |
| [G4] | Glean, Sharing and permissions; canonical page displayed 2026-10-14; search excerpt showed 2026-09-30. |
| [G5] | Glean, Human-in-the-loop confirmations; updated 2026-08-27. |
| [G6] | Glean, Enterprise Graph announcement; published 2025-09-25. |
| [G7] | Glean, Team chat; updated 2026-09-25; includes beta qualification. |
| [M1] | Microsoft Learn, Microsoft Graph overview; n.d. |
| [M2] | Microsoft Learn, Copilot connectors overview; n.d. |
| [M3] | Microsoft Learn, Semantic indexing; updated 2026-04-23. |
| [M4] | Microsoft Learn, Work IQ overview; updated 2026-09-25. |
| [M5] | Microsoft Support, How Copilot Pages works; n.d. |
| [S1] | Salesforce Developers, Data 360 architecture; n.d. |
| [S2] | Salesforce Developers, Object Model in Data 360; n.d. |
| [S3] | Salesforce Developers, Data Cloud and identity resolution; published 2024-10. |
| [S4] | Salesforce Developers, Create Search Index and Retriever; n.d. |
| [S5] | Salesforce Developers, Build custom actions using Apex; original URL dated 2024-03, updated branding. |
| [S6] | Salesforce Help, Agent context versus user context; published 2026-02-10. |
| [S7] | Salesforce Help, Agent Script in Multi-Agent Solutions; n.d. |
| [S8] | Salesforce Architects, Enterprise Agentic Architecture and Design Patterns; n.d. |
| [S9] | Salesforce Help, Multi-Agent Solutions considerations/limitations; n.d. |
| [N1] | ServiceNow, Exploring Knowledge Graph; Australia release; search excerpt updated 2026-03-12. |
| [N2] | ServiceNow, Blueprint for Agentic Business: Technical Foundation; PDF, n.d. |
| [N3] | ServiceNow, Primary connectors; Australia release, updated 2026-03-12. |
| [N4] | ServiceNow employee article, Zero Copy Connectors are here; published 2025-06-26, edited 2025-06-27. |
| [N5] | ServiceNow, Implement access control in AI agents; Australia release; search excerpt updated 2025-09-11. |
| [N6] | ServiceNow, Application support for domain separation; n.d. |

[P1]: https://www.palantir.com/docs/foundry/ontology/overview
[P2]: https://www.palantir.com/docs/foundry/ontology/ontology-augmented-generation
[P3]: https://www.palantir.com/docs/foundry/object-permissioning/overview
[P4]: https://www.palantir.com/docs/foundry/action-types/overview
[P5]: https://www.palantir.com/docs/foundry/architecture-center/aip-architecture
[P6]: https://www.palantir.com/docs/foundry/action-types/consistency-guarantees
[G1]: https://docs.glean.com/security/knowledge-graph
[G2]: https://docs.glean.com/security/architecture/data-flow/ingestion
[G3]: https://docs.glean.com/security/architecture/data-flow/processing
[G4]: https://docs.glean.com/agents/concepts/sharing-permissions
[G5]: https://docs.glean.com/agents/actions/human-in-the-loop-experience-for-actions
[G6]: https://www.glean.com/press/glean-introduces-third-generation-ai-assistant-new-enterprise-graph-to-enable-the-superintelligent-enterprise
[G7]: https://docs.glean.com/user-guide/assistant/team-chat
[M1]: https://learn.microsoft.com/en-us/graph/overview
[M2]: https://learn.microsoft.com/en-us/microsoft-365/copilot/connectors/overview
[M3]: https://learn.microsoft.com/en-us/microsoftsearch/semantic-index-for-copilot
[M4]: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/work-iq/
[M5]: https://support.microsoft.com/en-us/microsoft-365-copilot/how-microsoft-365-copilot-pages-works
[S1]: https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-architecture.html
[S2]: https://developer.salesforce.com/docs/data/data-cloud-dev/guide/dc-object-model.html
[S3]: https://developer.salesforce.com/blogs/2024/10/data-cloud-and-identity-resolution
[S4]: https://developer.salesforce.com/docs/ai/ground-agentforce-on-website/guide/aes-create-search-index-and-retriever.html
[S5]: https://developer.salesforce.com/blogs/2024/03/build-custom-copilot-actions-using-apex
[S6]: https://help.salesforce.com/s/articleView?id=005314096&language=en_US&type=1
[S7]: https://help.salesforce.com/s/articleView?id=ai.agent_multi_orch_script.htm&language=en_US&type=5
[S8]: https://architect.salesforce.com/docs/architect/fundamentals/guide/enterprise-agentic-architecture.html
[S9]: https://help.salesforce.com/s/articleView?id=ai.agent_multi_orch_consider.htm&language=en_US&type=5
[N1]: https://www.servicenow.com/docs/r/intelligent-experiences/knowledge-graph/exploring-knowledge-graph.html
[N2]: https://www.servicenow.com/content/dam/servicenow-assets/public/en-us/doc-type/brief/servicenow-blueprint-for-agentic-business-the-technical-foundation.pdf
[N3]: https://www.servicenow.com/docs/r/integrate-applications/workflow-data-fabric/primary-connectors-zcc.html?contentId=nd18_b9xcQt_g9jW2_ojsg
[N4]: https://www.servicenow.com/community/workflow-data-fabric-articles/zero-copy-connectors-are-here-unlock-real-time-enterprise-data/ta-p/3302004
[N5]: https://www.servicenow.com/docs/r/intelligent-experiences/aia-security-implementation.html
[N6]: https://www.servicenow.com/docs/r/platform-security/domain-separated-apps.html
