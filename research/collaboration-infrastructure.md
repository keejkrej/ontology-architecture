# Human–agent collaboration and enterprise knowledge infrastructure

Research date: **2026-10-14**. Scope: public primary-source documentation for collaboration products, retrieval/semantic infrastructure, execution frameworks, and interoperability. This note complements vertical-product research; it does not reverse-engineer undisclosed vendor internals. Documentation was accessed on the research date; rolling documentation can change.

Evidence labels: **[D]** documented behavior or specification; **[V]** vendor positioning or empirical claim, not independently validated; **[I]** architectural inference or proposed design; **[U]** unresolved from the reviewed public sources. References link directly to primary sources; the source register identifies their types. No product was tested hands-on.

## 1. The distinctions that prevent misleading comparisons

**[I]** Enterprise AI requires several related models, but these are different things:

- A **knowledge graph** represents entities and relationships: a supplier supplies a product, a person owns a service, a document supports a decision.
- An **ontology** defines the intended meanings, types, relationships, and constraints. A graph can have a weak or implicit ontology; the presence of graph storage does not establish a rigorous organizational model.
- An **execution graph** represents computational steps and transitions: retrieve evidence, produce a draft, request review, execute. LangGraph's name does not imply a business knowledge graph.
- **Multi-agent computation** distributes work among software agents. **Multiplayer collaboration** lets multiple humans and agents participate in shared, inspectable work with explicit ownership, changes, and handoffs.

**[I]** A system can have excellent retrieval and poor collaboration, or excellent shared editing and little organizational understanding. Evaluate these dimensions independently. An enterprise deployment combines them around concrete work objects; putting a chat window over a document index is only one possible component.

## 2. Compact classification for a market map

The classifications below are **[I]** interpretations of the cited capabilities, not vendor certifications.

| Product or infrastructure | Architectural center | Main inputs → outputs | Distinctive boundary to examine |
|---|---|---|---|
| Atlassian Rovo / Teamwork Graph | Cross-tool work objects and relationships | Work items, documents, people, connected content → contextual answers and work-item assistance | Shared work item versus initiator-only agent session [S1–S4] |
| Notion Custom Agents | Shared configurable workflow actor | Pages, databases, connected tools, triggers → reports and record updates | Agent resource rights versus permissions to use the agent [S5–S6] |
| Slack agents | Conversation as collaboration surface | Channels, messages, events, connected agents → shared or private interaction | Audience, app scopes, and retrieval retention rules [S7–S9] |
| Microsoft Research GraphRAG | Corpus-derived graph and summaries | Unstructured text → local/global grounded synthesis | Extracted structure and query-dependent cost [S10–S13] |
| Neo4j / Stardog | Graph retrieval and semantic data infrastructure | Graphs, text indexes, enterprise data mappings → retrieved context or query results | Graph ownership, schema, inference, and query access [S14–S18] |
| LangGraph plus MCP / A2A | Durable execution and integration | State, tools, delegated tasks → checkpoints, artifacts, actions | Persistence and interoperability versus business authorization [S19–S24] |

## 3. What collaboration products actually demonstrate

**[D] Atlassian:** Teamwork Graph documents a common model for work items, documents, messages, users, groups, and projects. Connectors map objects from different tools into that model and relate them, such as connecting a page to an issue or a message to a project. This is concrete evidence of an organizational context model, beyond a collection of embeddings. [What is Teamwork Graph?][S1]

**[D]** Connector behavior differs: synced connectors store and index workspace content; direct connectors retrieve through provider search APIs without storing or indexing that content. Smart Link connectors have narrower coverage based on links encountered in Atlassian. Separate documentation says source restrictions and deletions are reflected in Rovo access. **[U]** These pages do not establish one universal revocation-latency SLA or fully describe permissions on every derived relationship. [Connector types][S2], [permission synchronization][S3]

**[D]** Jira supports assigning agents to work items and invoking them through mentions or workflow transitions. Its collaboration documentation says the initiating person reviews and interacts with agent output, then can share results as comments or attachments. Other people can see that an agent was triggered. **[I]** Classify this documented flow as staged team collaboration; it does not establish unrestricted simultaneous participation in the same agent session. [Agent collaboration in Jira][S4]

**[D] Notion:** Custom Agents support recurring/event-driven work, reading selected resources, taking actions, and handing work to other granted agents. They are shared workflow resources. [Custom Agents][S5]

**[D]** Personal Notion AI uses the person's permissions; Custom Agents have separately granted resource permissions. Notion explicitly says sharing a Custom Agent lets its users retrieve information or make edits through that agent even when they lack direct access to the underlying resources. Enterprise administrators have creation, directory, and permission controls. **[I]** Agent sharing therefore becomes a deliberate delegation of authority that deserves its own review. [Sharing and permissions][S6]

**[D] Slack:** Agents can participate in channels or individual conversations, with public or private interactions. Slack exposes agent discovery, resumable sessions, and multiplayer conversation status. App capabilities depend on scopes and access; adding an agent to a conversation is part of its context boundary. **[U]** These surfaces do not by themselves establish how a particular third-party agent arbitrates competing human instructions. [Agents in Slack][S7]

**[D]** Slack's context guide recommends compact structured state containing goals, constraints, decisions, artifacts, and source attribution. Its Real-time Search documentation additionally restricts retrieval according to the destination context: public-channel invocations return public content; Slack Connect invocations are confined to that channel. The API prohibits storing or copying retrieved data. **[I]** Persisting workflow metadata and permitted references must be designed separately from building a copied Slack corpus. [Context management][S8], [Real-time Search][S9]

## 4. Retrieval: select a method for the question

**[D]** Microsoft Research GraphRAG's standard indexing pipeline extracts entities, relationships, and claims; detects communities; generates summaries at different granularities; and creates embeddings. Outputs are Parquet tables by default, with embeddings in the configured vector store. A graph database is therefore not a prerequisite of this implementation. [Indexing][S10]

**[D]** Local search combines extracted graph information with source text. Global search aggregates community reports through map/reduce and is described as resource intensive. DRIFT uses community information to broaden local exploration and generate follow-up questions. Basic vector retrieval is also available for comparison. [Query overview][S11]

**[D]** The global-search documentation identifies a quality/cost tradeoff: finer community levels can supply more detail while increasing time and LLM resources. **[V]** The research paper reports improved comprehensiveness and diversity over its conventional RAG baseline for global sensemaking questions on approximately million-token datasets. **[I]** That result is evidence for a particular task class, not proof that GraphRAG beats every hybrid retrieval system or verifies enterprise transactions. [Global search][S12], [research paper][S13]

**[I]** Use exact filters and authoritative APIs for account balances, IDs, policy versions, and current transaction state. Use lexical/vector retrieval for passages, graph traversal for explicit dependencies and relationships, and corpus summaries for broad thematic questions. Route queries rather than forcing all requests through one expensive pipeline. Count mistakes introduced during entity extraction and merging, not just answer-generation mistakes. A confidently generated edge remains a claim until its evidence and acceptance status justify stronger treatment.

## 5. Graph infrastructure supplies different kinds of semantics

**[D] Neo4j:** The GraphRAG Python package offers vector, vector-plus-Cypher, hybrid full-text/vector, hybrid-plus-Cypher, and text-to-Cypher retrieval. This provides several ways to join similarity search with graph structure; the package's name does not imply the same pipeline as Microsoft Research GraphRAG. [Retriever guide][S14]

**[D] Stardog:** Virtual Graphs map structured external data into a graph view that can be queried in place. Its inference engine evaluates queries with schema axioms and rules; supported expressivity depends on the reasoner and configuration. This supplies explicit symbolic semantics, distinct from asking an LLM to infer a relationship from prose. [Virtual Graphs][S15], [inference engine][S16]

**[D]** Stardog named-graph permissions control graph reads/writes, but schema axioms used for reasoning are not filtered by those named-graph permissions. Virtual-graph security documentation warns that registered virtual graphs are accessible through a database if named-graph security is disabled. **[I]** Federated data access therefore needs deliberate configuration and inference-aware review. Product support for permissions is not proof that a particular deployment correctly reproduces every source-system rule. [Named-graph security][S17], [virtual-graph security][S18]

**[I]** Choose infrastructure by the behavior required: semantic interoperability and rule reasoning; graph traversal and similarity; or corpus synthesis. One company may need all three, with clear authoritative sources and projections, rather than three competing copies of supposed truth.

## 6. State, memory, and durable execution

**[D]** LangGraph distinguishes thread-scoped graph checkpoints from stores for application-defined cross-thread data. Checkpointers preserve execution state and support review, resumption, and recovery; stores can hold preferences and shared knowledge. [Persistence][S19]

**[D]** Checkpoint documentation distinguishes synchronous, asynchronous, and exit-only persistence, with different durability/performance tradeoffs. Replay re-executes later nodes, including API calls and model invocations. Interrupt documentation says resuming begins again at the containing node's start and warns that preceding side effects should be idempotent or separated. [Checkpointers][S20], [interrupts][S21]

**[I]** Keep four stores conceptually separate, even if one database implements them: evidence records, business objects, execution checkpoints, and reusable memory. A checkpoint is not the current state of an ERP record. A conversation summary is not an approved company policy. A model recollection about a person's role is not an authorization grant.

**[I]** Memory should have an owner, scope, evidence references, creation time, expiry/review rule, and deletion behavior. Promote an observation into reusable organizational knowledge only through a defined acceptance path. Include correction and forgetting: otherwise a rejected inference can repeatedly reappear as remembered fact. Tenant and workstream namespaces protect different boundaries and should not be collapsed into a single user ID.

## 7. MCP and A2A connect systems; they do not define the organization

**[D]** MCP uses a host/client/server architecture for resources, tools, and prompts. The host coordinates context and security boundaries. MCP security guidance rejects accepting tokens intended for a different service and forwarding them downstream without proper validation. [MCP architecture][S22], [security guidance][S23]

**[D]** A2A defines agent discovery, tasks, messages, artifacts, asynchronous updates, and authorization responsibilities. Crucially, its current specification says Send Message operations **may** be idempotent; implementations may deduplicate using message IDs. **[I]** A2A compatibility therefore does not establish exactly-once external business actions. [A2A specification][S24]

**[D]** The A2A project describes MCP as connecting agents with capabilities and A2A as coordinating independent agents. **[I]** Neither automatically reconciles two organizations' definitions of customer, matter, approval, or completion. A delegation still needs an agreed business payload, identity, allowed outputs, evidence requirements, deadlines, and failure semantics. A tool-shaped agent is possible; choose interfaces by interaction contract rather than branding. [Protocol comparison][S25]

## 8. A practical organizational model

Everything in this section is a **[I] proposed model**, not an assertion about the internals of the products above.

Build a small shared foundation, then extend by domain:

| Object family | Minimum representation | Why it matters |
|---|---|---|
| Actors | Person, Team, Role, Agent, ServiceIdentity, delegation grant | Separate who requested, who acted, and who was authorized |
| Business context | Organization, Goal, Workstream, Project, Asset, Counterparty | Connect work to an accountable owner and outcome |
| Knowledge | SourceObject, SourceVersion, EvidenceSpan, Claim, Decision, PolicyVersion | Separate content, interpreted assertion, accepted decision, and governing rule |
| Execution | Task, Run, PlanVersion, ActionProposal, Approval, ToolInvocation, Result | Make progress and effects inspectable and resumable |
| Collaboration | Participant, Assignment, Comment, ArtifactVersion, Review, Conflict | Preserve authorship, handoff, alternatives, and disagreement |

Use stable identifiers for business objects, with source-system IDs retained as mappings. Do not identify a supplier solely by name or a person solely by an email address that can change or be reused. Model organizational structure and working relationships separately: reporting manager, project owner, contributor, reviewer, and budget approver are different relationships.

For a claim or relationship, retain `subject`, `predicate`, `object`, `source_version`, `evidence_span`, `asserted_by`, `extraction_method`, `confidence`, `status`, `valid_from`, `valid_to`, and `observed_at`. Confidence is not authority. A high-confidence inference about who usually approves purchases must not overwrite an explicit delegation policy.

Two times are particularly useful: when something was true in the business, and when the system learned it. A late-arriving employee transfer changes historical interpretation differently from a correction to a wrongly recorded transfer. Retain supersession links instead of silently overwriting contradictory claims. Queries should specify whether they seek current truth, historical truth, or what was known at a past decision point.

Domain extensions make the shared foundation operational. Legal work adds Matter, Client, Jurisdiction, Obligation, Clause, and PrivilegeClassification; procurement adds Requisition, Supplier, Quote, PurchaseOrder, Budget, and ApprovalThreshold. The reusable platform handles evidence, authority, and execution, while domain definitions specify valid actions and completion. This explains why similar AI building blocks can produce substantially different products.

## 9. Permissions, provenance, and inferred relationships

The following are **[I] design requirements** inferred from the documented variations above.

Evaluate both **who may retrieve** and **who may receive the result**. A user may read a private document but be speaking in a public channel. A shared agent may hold broader rights than its caller. Choose and document whether each operation uses caller delegation, a service identity, or an explicitly shared capability. Never assume one rule fits every product surface.

Propagate protection through transformations. Chunks, embeddings, extracted entities, relationship edges, summaries, caches, and generated artifacts can all reveal restricted content. A community summary built from mixed-access documents cannot safely be made available merely because some contributing documents were public. For derived claims requiring several premises, a conservative policy requires access to all necessary premises unless an approved release rule permits disclosure. Alternative independent evidence may justify a different policy; this needs explicit lineage.

Recheck authorization at retrieval and immediately before external effects. Track content freshness and permission freshness separately. Revocation should invalidate applicable cached retrieval results and derived artifacts, while retention and audit obligations determine what historical records remain protected. Test whether entity names, counts, graph paths, or explanations leak the existence of inaccessible objects.

Treat inferred expertise and organizational influence as tentative contextual signals. Frequency of messaging does not confer ownership; seniority does not establish signing authority. Separate sourced facts, computed relationships, model-generated hypotheses, and accepted business decisions. Let responsible people correct the model without erasing the record of why the system previously believed something.

**[U]** Public product documentation reviewed here does not establish a universal solution for permissions on every inference, historical artifact, or cross-product cache. These are deployment questions requiring demonstrations and adversarial tests.

## 10. Multiplayer work needs transaction semantics

This section is **[I] proposed application architecture**. Framework features supply useful mechanisms; the application must define the business guarantees.

Use the shared work object as the coordination center. Show the objective, current plan, evidence, draft artifact, responsible human, agent state, and pending decisions. Chat remains an interaction surface. Participants should be able to identify what is proposed, approved, executing, completed, or disputed without reconstructing a long conversation.

Bind approval to an immutable action proposal: operation, target IDs, exact parameters or content hash, recipient, acting identity, expected object version, relevant policy version, and expiry. Store the approver and the proposal version together. If an agent changes the amount, counterparty, document, or recipients after approval, the prior approval does not automatically authorize the changed proposal. A casual “yes” must resolve to a specific outstanding proposal.

At execution, revalidate rights, approval status, resource version, and relevant policy conditions. Use optimistic concurrency checks or locks where appropriate. If a human changes a purchase requisition while an agent reviews it, execution should detect the version conflict. Two humans editing text can often merge; two competing approvals for incompatible commercial terms need explicit conflict resolution, not automatic last-write-wins behavior.

Assign each business effect a stable idempotency key. Couple the approved intent and durable dispatch record transactionally where possible; use receiver-side deduplication when supported. Record the external object ID and outcome. If an API times out after accepting a request, reconcile its status before retrying blindly. A saved local checkpoint cannot prove whether a remote purchase order was created.

Distinguish cancellation from compensation. Stopping an agent prevents future work but does not unsend a message or undo a committed purchase. A recovery workflow needs permission and its own audit trail. Successful execution should emit a receipt: action, target, actor, authority, source versions, timestamps, external result, and remaining exceptions.

Scope intervention rights deliberately. Contributors can supply evidence; reviewers can request changes; an accountable owner resolves conflicting goals; authorized approvers permit effects. Delegating research to several agents does not give each of them authority to mutate shared business state. This is where organizational design and distributed-systems design meet.

## 11. Evaluation and operational economics

**[D]** LangSmith documents offline evaluation on datasets and online evaluation of production traces, with human, code, and model-based evaluators. Slack's developer governance guide likewise recommends observable task outcomes, actor/model attribution, retries, latency, and token usage. These are documented tools and recommendations, not evidence that any deployment achieves a particular quality level. [LangSmith evaluation][S26], [Slack governance][S27]

**[I]** Evaluate six layers separately: extraction and entity resolution; retrieval and freshness; answer grounding and citation correctness; authorization and audience isolation; action validity and recovery; and end-to-end business outcomes. Build cases for conflicting evidence, ambiguous entities, permission revocation during execution, stale approvals, duplicate events, provider timeouts, simultaneous human edits, and hostile instructions embedded in retrieved documents.

Report quality by domain and task type. A global synthesis benchmark cannot substitute for purchase-order precision. Pair model grading with deterministic checks and domain-expert review. Track abstention and escalation quality, including unnecessary escalations that consume human attention. Compare with a well-built hybrid-search baseline before accepting the graph's extra complexity.

Measure **cost per accepted business outcome**, including connector operations, indexing and re-indexing, graph maintenance, retrieval, model calls, retries, storage, observability, evaluation, human review, and incident recovery. Track median and tail latency plus human waiting time. Agent fan-out can reduce elapsed time while increasing total cost; global summaries amortize construction only when their useful lifetime and reuse justify it.

Keep economics empirical: run a representative workload with realistic access diversity and change rates. Separate setup costs from steady-state costs. Do not infer ROI from token savings alone, or from a vendor's “smarter and cheaper” positioning without workload measurements.

## 12. An organizational deployment path

**[I]** Start with one bounded workstream and an explicit owner. Agree on object definitions, authority, source coverage, and acceptance criteria. Deliver read-only evidence gathering first; then reviewed drafts; then approved writes; then bounded autonomy for operations whose failure and recovery behavior are understood. Expansion should follow measured outcomes and operational readiness.

Use a shared identity, evidence, policy, and action-record foundation across domains, while letting domain teams own schemas, evaluations, and exceptions. Treat connector health and knowledge stewardship as ongoing work. Appoint owners for conflicting data and stale policies. A central graph team cannot resolve every semantic disagreement by technical means.

**[U]** Deployment-specific evidence still needed: permissions on derived artifacts; deletion propagation; exportability of object IDs and histories; delegated identity behavior; action retry guarantees; data residency across model/tool routes; and actual review burden. These questions often distinguish a durable enterprise operating model from an impressive assistant demonstration.

## Source register

All sources accessed 2026-10-14. “Documentation” denotes first-party descriptions, not independent validation. Each URL is intentionally summarized briefly to leave room for synthesis elsewhere.

| ID | Primary source | Type / evidence scope |
|---|---|---|
| S1 | [Atlassian: What is Teamwork Graph?][S1] | Documentation; common objects and relationships |
| S2 | [Atlassian: connector types][S2] | Documentation; synced/direct/Smart Link behavior |
| S3 | [Atlassian: permission synchronization][S3] | Documentation; source access and deletion |
| S4 | [Atlassian: agent collaboration in Jira][S4] | Documentation; invocation and output sharing |
| S5 | [Notion: Custom Agents][S5] | Documentation; recurring shared workflows |
| S6 | [Notion: agent sharing and permissions][S6] | Documentation; agent versus caller authority |
| S7 | [Slack: work with agents][S7] | Documentation; conversational collaboration |
| S8 | [Slack: context management][S8] | Developer guide; structured context |
| S9 | [Slack: Real-time Search][S9] | API guide; audience and retention boundaries |
| S10 | [GraphRAG: indexing][S10] | Project documentation; extraction pipeline |
| S11 | [GraphRAG: query overview][S11] | Project documentation; retrieval modes |
| S12 | [GraphRAG: global search][S12] | Project documentation; aggregation tradeoffs |
| S13 | [GraphRAG research paper][S13] | Original research; scoped experimental claims |
| S14 | [Neo4j: GraphRAG retrievers][S14] | Library documentation; retrieval combinations |
| S15 | [Stardog: Virtual Graphs][S15] | Documentation; federation/mapping |
| S16 | [Stardog: inference engine][S16] | Documentation; configured rule semantics |
| S17 | [Stardog: named-graph security][S17] | Documentation; access and schema caveat |
| S18 | [Stardog: virtual-graph security][S18] | Documentation; security configuration |
| S19 | [LangGraph: persistence][S19] | Documentation; checkpoints versus stores |
| S20 | [LangGraph: checkpointers][S20] | Documentation; replay and durability modes |
| S21 | [LangGraph: interrupts][S21] | Documentation; resumption and side effects |
| S22 | [MCP: architecture][S22] | Versioned specification; host and server roles |
| S23 | [MCP: security guidance][S23] | Protocol guidance; token boundaries |
| S24 | [A2A: specification][S24] | Rolling specification; tasks and optional deduplication |
| S25 | [A2A: comparison with MCP][S25] | Project guide; complementary interfaces |
| S26 | [LangSmith: evaluation][S26] | Documentation; offline/online evaluation |
| S27 | [Slack: governance and trust][S27] | Developer guidance; observation and intervention |

[S1]: https://developer.atlassian.com/platform/teamwork-graph/what-is-teamwork-graph/
[S2]: https://support.atlassian.com/organization-administration/docs/teamwork-graph-connector-types/
[S3]: https://support.atlassian.com/organization-administration/docs/how-connector-permissions-are-kept-in-sync/
[S4]: https://support.atlassian.com/jira-software-cloud/docs/collaborate-on-work-items-with-ai-agents/
[S5]: https://www.notion.com/help/custom-agents
[S6]: https://www.notion.com/help/custom-agents-sharing-and-permissions
[S7]: https://slack.com/help/articles/33076000248851-Work-with-AI-agents-in-Slack
[S8]: https://docs.slack.dev/ai/agent-context-management/
[S9]: https://docs.slack.dev/apis/web-api/real-time-search-api/
[S10]: https://microsoft.github.io/graphrag/index/overview/
[S11]: https://microsoft.github.io/graphrag/query/overview/
[S12]: https://microsoft.github.io/graphrag/query/global_search/
[S13]: https://arxiv.org/abs/2404.16130
[S14]: https://neo4j.com/docs/neo4j-graphrag-python/current/user_guide_rag.html
[S15]: https://docs.stardog.com/virtual-graphs/
[S16]: https://docs.stardog.com/inference-engine/
[S17]: https://docs.stardog.com/operating-stardog/security/named-graph-security
[S18]: https://docs.stardog.com/operating-stardog/security/virtual-graph-security
[S19]: https://docs.langchain.com/oss/python/langgraph/persistence
[S20]: https://docs.langchain.com/oss/python/langgraph/checkpointers
[S21]: https://docs.langchain.com/oss/python/langgraph/interrupts
[S22]: https://modelcontextprotocol.io/specification/2025-11-25/architecture
[S23]: https://modelcontextprotocol.io/docs/2025-11-25/tutorials/security/security_best_practices
[S24]: https://a2a-protocol.org/latest/specification/
[S25]: https://a2a-protocol.org/latest/topics/a2a-and-mcp/
[S26]: https://docs.langchain.com/langsmith/evaluation
[S27]: https://docs.slack.dev/ai/agent-governance/
