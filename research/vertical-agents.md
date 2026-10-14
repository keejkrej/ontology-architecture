# Vertical enterprise AI: the architecture of governed work

Research date: **14 October 2026**. Scope: Harvey, Legora, Lio, Zip, Ironclad, Sierra, Decagon, and Hebbia. Sources are first-party engineering articles, product documentation, product announcements, and vendor-published customer accounts. This is an architectural comparison, not an independently tested product ranking.

Evidence labels: **D** = explicitly documented implementation or contractual product definition; **V** = vendor product/case-study claim; **I** = analytical inference or proposed design; **U** = not established by the reviewed public evidence. D still means vendor-disclosed, not independently audited. A named business object does not establish a graph database, formal ontology language, or knowledge-graph implementation. Live product pages were checked on the research date; dated engineering posts describe the implementation at publication.

## Main finding

**I:** The common architecture is an environment in which AI can interpret evidence, produce work, and sometimes change business state under organizational authority. The vertical specialization reaches much deeper than input/output formats. It specifies what counts as a valid object, which relationships change an answer, who may act, which state transitions require review, and what constitutes a successful outcome.

For example, a document passage is evidence. A proposed contract amendment is work product. An approved purchase request is authorized business state. These are different object categories even when an LLM represents all three as text. Combining them without explicit boundaries makes it difficult to distinguish a discovered fact, a suggestion, and a decision that binds an organization.

**I:** “Multiplayer” also has several meanings: people editing shared artifacts; agents dividing work; people delegating and reviewing agent work; and separate organizations exchanging governed resources. A system can implement one without the others. The strongest architectural evidence here concerns shared work state, preserved provenance, and constrained action, rather than a universal enterprise knowledge graph.

## Compact market schema

Family classifications are **I**; object labels are documented or product-described as marked. Sources are linked in the vendor sections below.

| Product | Architectural family | Core work object and evidence | Principal boundary | Public unknown |
|---|---|---|---|---|
| Harvey | Legal workbench with tool execution | D: versioned contract review; V: Vault and Space | Matter sharing; source ACLs; tool-call policy | Complete internal domain schema |
| Legora | Matter workspace with agent execution | D: project/matter; V: source-linked List item | Project/tenant isolation; ethical walls | Business knowledge-graph implementation |
| Lio | Procurement execution over incumbent systems | V: purchase request, supplier, approval | ERP authority and exception escalation | Retry/idempotency and agent topology |
| Zip | Procurement orchestration with task agents | V: request and approval node | Cross-functional approval workflow | Agent evaluation methodology |
| Ironclad | AI inside contract lifecycle management | D: workflow, contract record, clause/property | Configured roles and lifecycle stages | Broader agent coordination internals |
| Sierra | Customer interaction and action platform | V: customer memory and conversation | Policy supervisors and system integrations | Published customer/entity schema |
| Decagon | Customer-service procedures and execution | V: AOP, conversation, tool action | Configured guardrails and human handoff | Compiler/runtime internals |
| Hebbia | Collaborative analytical workbench | V: project, matrix, cited artifact | Source selection, shared work, data isolation | Full evaluation and permission semantics |

## Harvey: evidence, review state, and explicit action authority

**V — inputs and outputs.** Vault combines uploaded files, emails, and document-management content with structured review tables and cited analysis. It advertises integrations including iManage, SharePoint, and Google Drive, plus permissions for viewing, editing, and sharing. Its knowledge bases hold precedents, templates, and playbooks for reuse across work. These are concrete work surfaces; the page does not specify their database representation. [H1: Vault](https://www.harvey.ai/platform/vault)

**D — retrieval.** Harvey’s November 2024 retrieval article describes domain-aware preprocessing, metadata, relevance reasoning, and evaluation against annotated legal material. Contract cross-references, email metadata, jurisdiction, and recency matter beyond embedding similarity. Retrieval evaluation measures relevant material recovered within a fixed token budget. This is direct evidence of specialized RAG; it is not evidence of an enterprise knowledge graph. [H2: BigLaw Bench — Retrieval](https://www.harvey.ai/blog/biglaw-bench-retrieval)

**D — multi-agent work.** The September 2026 playbook-review implementation assigns rules to parallel workers. Document elements have stable identifiers; workers edit separate branches of a versioned document model; a lead agent reconciles collisions. Review state persists for follow-up changes. Evaluation distinguishes risk classification from lawyer-defined redline quality. Personalization from accepted/rejected edits is presented partly as future development, not an established universal learning loop. [H3: Rebuilding Playbook Review](https://www.harvey.ai/blog/rebuilding-playbook-review-as-a-multi-agent-system)

**D — integration authority.** The October 2026 connector design groups native and MCP capabilities under a registered connector. Personal-data calls use the requesting user’s own authorization, with the source enforcing its ACLs. Native retrieved documents receive inline citations; MCP responses enter context as text. The connector is therefore both a capability abstraction and a permission boundary. [H4: Connector Library engineering](https://www.harvey.ai/blog/how-we-built-harvey-connector-library)

**D — action policy.** Harvey documents per-call enforcement outside the model using Rego policies and Regorus. Policies examine Harvey-maintained tool annotations and call history, and may allow, deny, or require user approval; failed checks deny execution. The article explicitly recognizes that a nominally read-only search can disclose private material through query arguments. It does not claim prompt injection is solved. [H5: MCP Policy Engine](https://www.harvey.ai/blog/building-harveys-mcp-policy-engine)

**V — human collaboration.** Spaces shares Vaults, artifacts, workflows, and playbooks between firms, clients, and internal teams. Harvey describes resource-level permissions, administration from both organizations, guest access, audit events, and Intapp ethical-wall integration. This supports cross-organization work around a matter, not merely a shared chat. [H6: Spaces](https://www.harvey.ai/platform/spaces)

**D — feedback and evaluation.** BigLaw Bench Arena collects lawyers’ pairwise preferences plus explanations and analyzes preference drivers. Such evaluation complements retrieval and task rubrics; it is not an estimate of a deployment’s absolute error rate or a comparison with every current competitor. [H7: Arena](https://www.harvey.ai/blog/introducing-biglaw-bench-arena)

**I — inferred domain model.** A useful reconstruction is `matter → document version → proposed change → reviewer decision`, with evidence and organizational policy attached separately. The key distinction is between a proposition supported by a source and an edit authorized for a particular negotiation. **U:** the complete persisted schema, knowledge-graph backend, cross-product consistency model, and organization-specific outcome-learning mechanism remain undisclosed here.

## Legora: a matter is a retrieval partition and an execution environment

**D — search implementation.** Legora’s September 2026 engineering post says projects commonly correspond to legal matters. It combines keyword and vector retrieval, and describes migration from Elasticsearch through PostgreSQL/pgvector/DiskANN to Turbopuffer. Project namespaces exploit matter-local search and dormant projects; tenant storage and key configuration support isolation. An approximate-nearest-neighbor index may internally use graph algorithms: that is not a business knowledge graph. [G1: Scaling Search for Legal AI](https://legora.com/engineering/scaling-search-for-legal-ai)

**D — evaluation environment.** Legora evaluates its agent in reproducible “Eval Worlds” containing documents, database records, permissions, and blob state. Its described runtime includes document editing, search, PostgreSQL, authorization, and code sandboxes. Modal VM sandboxes and Temporal run isolated experiments; cases, configurations, and repeated trials support comparison. This documents testing of work in an environment, rather than only grading isolated answers. [G2: Evals infrastructure](https://legora.com/engineering/building-scalable-evals-infrastructure-for-legal-agents)

**D — coordination infrastructure.** A separate engineering post describes asynchronous uploads, integration syncs, reviews, and long-running agents. Backend authorization mints tokens for a separate WebSocket relay, with Dragonfly streams transporting updates. The disclosed design addresses connection lifecycle and authorization load. It does not establish a particular algorithm for simultaneous document editing. [G3: Authorized WebSocket relay](https://legora.com/engineering/a-type-safe-centralized-and-authorized-websocket-relay)

**V — product architecture.** Legora’s aOS describes a harness for routing tools, managing memory, selecting models, and deploying specialist agents. Firm playbooks, precedents, clause banks, negotiated positions, and matter history supply context; integrations include document management and MCP. Governance includes ethical walls and audit trails for file access, tool calls, and agent actions. [G4: Legora aOS](https://legora.com/product/aos)

**V — structured collaborative records.** Lists converts documents into items with source links, status, and assignee. Humans can comment, assign ownership, update state, and sign off while agents help maintain the list. Examples include closing checklists, chronologies, and verification logs. The launch article explicitly marks some extensions into other surfaces as future work. [G5: Introducing Lists](https://legora.com/blog/introducing-lists)

**V — cross-firm work.** Portal publishes selected documents, reviews, and workflows for clients. Legora describes role-based access, audit trails, joint editing, and workflows whose underlying firm prompts and logic remain hidden from guests. The permission to use institutional expertise can therefore differ from permission to inspect its implementation. [G6: Portal](https://legora.com/product/portal)

**I — architectural significance.** Matter scope is simultaneously a relevance boundary, a performance boundary, a collaboration boundary, and an execution context. That is a stronger form of organizational understanding than ingesting every firm document into one index. A closing condition needs an owner and completion state as well as its textual meaning. **U:** public evidence does not establish a formal enterprise ontology, cross-matter identity resolution, or exact access-revocation behavior across every derived artifact and cache.

## Lio: the organization as purchasing authority and operational procedure

The intended company is **Lio Technologies at [lio.ai](https://www.lio.ai/)**, which markets enterprise procurement agents. This is distinct from unrelated products sharing the Lio name.

**V — intake.** Lio describes guided buying inside Microsoft Teams and integration with Ariba/Coupa. Inputs include free text, catalog selections, uploaded quotes, and photographs; procurement-defined questions collect missing information. The aim is to map ordinary employee intent into procurement and accounting structure. [L1: Guided buying](https://www.lio.ai/newsroom/how-we-created-a-guided-buying-system-employees-actually-want-to-use)

**V — operational case.** Its tesa account describes context based on employee role, site, and approval level. Agents validate requests against company rules, contact requesters and suppliers for missing information, follow up, route completed requests to approvers, and surface exceptions for buyers. The story also describes tail-spend sourcing and negotiation. These are vendor-reported operating examples, not independent measurements of reliability. [L2: tesa customer account](https://www.lio.ai/customers/tesa)

**V — system of record.** Lio explicitly positions the ERP as authoritative and describes APIs/middleware connecting SAP, Ariba, or Coupa. It says it executes in existing systems without maintaining a shadow purchase-request record and synchronizes changes. This is a meaningful architectural claim, but public text does not prove atomic cross-system transactions or specify conflict resolution. [L3: Enterprise systems and execution](https://www.lio.ai/newsroom/enterprise-systems-aren-t-the-bottleneck-manual-execution-is)

**V — human/agent division.** Lio distinguishes leadership strategy, human translation into operating procedures, and agent execution. Human supervisors define negotiation parameters, approval rules, risk thresholds, supplier priorities, and escalation triggers. Agents perform operational tasks within those directions. The company’s vision is supervisory human involvement and exception handling, not a requirement for human approval of every action. [L4: Operational buyer to agent supervisor](https://www.lio.ai/newsroom/from-operational-buyer-to-agent-supervisor-the-procurement-workforce-of-the-future)

**V — controls.** Lio describes Azure hosting, isolated customer data, role-based access, least privilege, encrypted data, audited privileged access, and centralized logging. Its security page says customer data is not used for training shared AI models. These claims do not explain how any aggregate market intelligence is produced. [L5: Security](https://www.lio.ai/security)

**I — inferred business model.** The central semantic structure is approximately `employee requests item/service → supplier offers terms → policy constrains purchase → approver authorizes commitment → ERP records transaction`. Relationships carry decision rights: a person may request a service but lack authority to approve it; a supplier can be approved for one category or site without being acceptable everywhere. Durable waiting, reminders, and exception queues matter because a purchase can span days and involve external parties.

**U:** reviewed sources do not disclose a named graph backend, retrieval/ranking design, machine-readable procedure schema, agent messaging protocol, credential delegation details, idempotency, rollback, or a reproducible agent benchmark. None should be inferred from the phrase “multi-agent system.” Lio’s dated newsroom pages also show inconsistent original/effective dates; this note relies on checked content rather than inferring release timing from them.

## Contrasting architectures

### Zip: automate a step within a visible approval process

**V:** Zip’s 2025 launch places specialized agents at approval nodes. Examples validate intake against supplier records, uploaded documents, and policy, or trigger further due diligence. Vendor profiles, contracts, invoices, and integrations provide context. Numerical autonomy forecasts in that announcement are forecasts, not verified 2026 outcomes. [Z1: Agentic procurement orchestration](https://zip.com/blog/introducing-agentic-procurement-orchestration)

**V:** The workflow engine routes through cross-functional queues and user hierarchies, integrates ERP/CLM/GRC/ITSM systems, and lets participants approve in existing tools. [Z2: Workflow engine](https://zip.com/capabilities/workflow-engine)

**I:** Zip’s visible organizing unit is an approval process into which automation is inserted; Lio emphasizes agents performing operational work inside incumbent systems. Both can converge functionally, so this is positioning supported by published behavior, not a claim of exclusive capabilities. For deployment, evaluate who owns process state and how an agent recommendation becomes an approved state change. **U:** the inspected sources do not establish agent benchmarking, authorization internals, or exact recovery semantics.

### Ironclad: a lifecycle system supplies the domain model

**D:** Ironclad’s September 2026 product definitions explicitly describe contract records, configurable clauses/properties, counterparty and region inputs, workflow roles, approval routing, repository permissions, negotiation turns, and lifecycle stages through signature/archive. AI-suggested metadata is qualified by configuration, document quality, and human review. Integrations include storage, identity, and e-signature providers. [I1: Contractual product descriptions](https://legal.ironcladapp.com/fy2026-product-descriptions)

**V:** Contract Review Agent applies uploaded or CLM playbooks to produce reviewable redlines. Ironclad stresses clarifying implicit playbook assumptions. The announcement reports controlled testing and describes curated historical precedent as a next step, which should not be treated as generally available merely because it appears in the article. [I2: Contract Review Agent](https://ironcladapp.com/resources/articles/contract-review-agent-redlining-playbook)

**I:** Here the AI inherits a business lifecycle and permission model that exists beyond the chat. This can provide tighter links between drafting, approval, signature, and the resulting authoritative record. A negotiated exception still needs a reason and scope; treating every accepted clause as future policy would erase strategic judgment. **U:** the full agent runtime, model-selection logic, and graph storage are not established here.

### Sierra: customer context, action, and risk-dependent supervision

**D:** Sierra describes separate supervisory agents for input threats and action/response checking. Supervisors can intervene or escalate, and the design varies adherence requirements by instruction category. It combines operational reviews, red teaming, evaluations, and simulations. This is an explicit systems approach to bounded errors, not a guarantee of error-free conversation. [S1: Enterprise-grade agents](https://sierra.ai/blog/enterprise-grade-agents)

**V:** Context Engine links interactions to a person across channels, incorporates system-of-record customer history, and offers a permissioned, exportable memory layer. It describes reacting to fresh events and pursuing business outcomes within constraints. [S2: Context Engine](https://sierra.ai/product/context-engine)

**I:** The domain shifts to customer identity, service state, entitlement, and permitted intervention. A useful result may be a completed resolution rather than a document. Human collaboration includes supervising policies and receiving escalations; it need not mean co-editing an artifact. **U:** the precise memory schema, identity-resolution rules, connector-specific authorization, and storage technology are not established by these sources.

### Decagon: operating procedures become configurable agent behavior

**V:** AOPs let business teams describe procedures in natural language while engineering retains code ownership and Git-based versioning. The product exposes traces, rules for escalation, and connections to live tools. [D1: Agent Operating Procedures](https://decagon.ai/product/aop)

**V:** Integrations ingest knowledge articles, connect CRM/ticketing, call APIs/MCP tools, and transfer conversations to humans. Thus knowledge retrieval, record access, and consequential actions are separate capabilities within the support workflow. [D2: Integrations](https://decagon.ai/product/integrations)

**V:** Testing covers conversations and checkpoints for tool use, actions, data, and business logic. It includes repeated simulations, version testing, and alerting. [D3: Testing and QA](https://decagon.ai/product/testing-qa)

**I:** The distinctive semantic artifact is the operational procedure: when a situation arises, what evidence is needed, which branch is valid, what may change, and when to escalate. Procedure version should accompany the outcome so failures can be attributed to a rule, context, or execution error. **U:** these pages do not expose the exact compiler, deterministic guarantees, customer-role authorization matrix, or graph backend.

### Hebbia: analysis is a process that humans inspect

**V:** Matrix decomposes questions into agent-executable steps and exposes a grid in which users inspect and modify analytical work. It describes multimodal document processing and analysis across supplied collections. Claims of unlimited complexity or unique market firsts are marketing, not established capabilities. [B1: Introducing Matrix](https://www.hebbia.com/blog/introducing-matrix-the-interface-to-agi)

**V:** June 2026 updates describe shared-project publication controls, source review before agent execution, cited slide output, API/MCP access, financial/CRM data integrations, and a tick-and-tie agent for checking figures against sources. [B2: June release](https://www.hebbia.com/blog/whats-new-june-disclosure-2026)

**V:** Security claims include customer isolation, restricted production access, regional processing, and audit visibility. [B3: Security](https://www.hebbia.com/security/)

**I:** The useful work object is an analytical claim or metric linked to a source and intermediate transformation. A grid supports human comparison, correction, and synthesis before a consequential investment or business decision. The inspected evidence does not establish that such decisions themselves are autonomously committed. **U:** exhaustive extraction recall, quantitative reconciliation accuracy, and detailed inherited-source permission semantics require further validation.

## What these verticals teach about enterprise ontology

The following are **I: design conclusions**, not claims that every vendor already implements them.

1. **Model work objects before selecting storage.** A matter, purchase request, contract workflow, customer case, and analysis project have different lifecycles. Choose identifiers, allowed transitions, and ownership before deciding whether relational, document, vector, or graph storage is appropriate.
2. **Separate evidence, policy, and decision.** A past contract is evidence of what happened; a playbook expresses intended behavior; a signed approval authorizes an exception. Retrieval must preserve those roles instead of flattening all text into equally authoritative context.
3. **Attach authority to actions, not just documents.** Being able to read supplier data does not imply permission to select a supplier or commit spend. Authorization depends on actor, action, object, relationship, amount, and current process state.
4. **Persist the collaboration state.** Store which person or agent proposed a change, which version they saw, what evidence supported it, and who accepted it. Shared access alone cannot resolve competing edits or distinguish a draft from an approved result.
5. **Represent temporal context.** A policy may have changed since a prior contract; customer entitlements may expire; supplier approval may be conditional. The valid-at time of evidence and the execution-time state both matter.
6. **Evaluate transitions as well as text.** Test whether a blocked action stays blocked, a retry avoids duplicate commitments, and a handoff preserves context. Measure quality against the actual work object, with human review cost included.

## Practical validation questions and source quality

For any proposed large-enterprise deployment, request a demonstration in which the same user has different rights across two matters, departments, or subsidiaries; a policy changes mid-process; two agents propose conflicting changes; and an external API times out after accepting a write. Inspect the persisted evidence and recovery behavior. These exercises reveal architectural capabilities that a polished answer-generation demo cannot.

The most technically informative sources are H3–H5 and G1–G3. I1 is valuable because it precisely defines purchasable behavior and limitations. L1–L4, Z1–Z2, G4–G6, D1–D3, S2, and B1–B3 predominantly document vendor-described behavior. Customer stories remain vendor-published evidence. Public omission does not mean a capability is absent; it means this research cannot verify it.

### Short source register

All links above were checked on 14 October 2026. Each source is summarized conservatively to preserve room for cross-report synthesis.

| Group | Sources | Type/date |
|---|---|---|
| Harvey | H1 Vault; H6 Spaces | Live product descriptions |
| Harvey | H2 Retrieval; H7 Arena | Research, 13 Nov 2024 / 7 Nov 2025 |
| Harvey | H3 Playbook; H4 Connectors; H5 Policy | Engineering, 2 Sep / 1 Oct / 7 Oct 2026 |
| Legora | G1 Search; G2 Evals; G3 Relay | Engineering, 11 Sep 2026 |
| Legora | G4 aOS; G5 Lists; G6 Portal | Product/launch descriptions |
| Lio | L1 Guided buying; L3 ERP; L4 Supervision | Architecture/operating-model claims; date fields inconsistent |
| Lio | L2 tesa; L5 Security | Customer account / live controls page |
| Zip | Z1 Agents; Z2 Workflow | 10 Jun 2025 announcement / live product page |
| Ironclad | I1 Product definitions; I2 Review agent | Effective 2 Sep 2026 / product announcement |
| Sierra | S1 Supervisors; S2 Context | 2 Oct 2025 engineering / live product page |
| Decagon | D1 AOP; D2 Integrations; D3 QA | Live product descriptions |
| Hebbia | B1 Matrix; B2 June; B3 Security | 2024 launch / June 2026 release / live controls page |
