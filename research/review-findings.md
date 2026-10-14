# Research review findings

Reviewed 14 October 2026: the main report, its added 23-product comparison and feature-boundary paragraph, and all four evidence notes. Selected primary pages were reopened for Glean, Claude, Databricks, Workday, Harvey, Legora, Microsoft, and Palantir. This was a targeted factual and architectural review, not a full audit of every source. The final visual was not part of this review.

## Corrections identified and verified

Both corrections below were applied by the report author and verified in the current main report. No material unresolved factual issue was identified in this review.

1. **Resolved — duplicate protection.** The supplier walkthrough now specifies receiver-enforced idempotency where supported and reconciliation, and explicitly rejects the implication that a locally generated key alone provides protection. This aligns the main report with the infrastructure note. The issue concerned proposed architecture, not a vendor allegation.

2. **Resolved — Harvey policy scope.** The main report now scopes policy mediation to partner MCP tool calls, matching the [disclosure](https://www.harvey.ai/blog/building-harveys-mcp-policy-engine), while keeping the broader connector-registry claim separate.

The initially missing `sources.md` has now been created, resolving that completion issue. The new product comparison introduces no further material factual issues identified in this review.

## Source-word-budget hotspots

No clear per-URL excess above 200 source-derived words was identified in the reviewed Markdown, including the product comparison. Counts below are conservative working estimates, not exact copyright accounting; they include some surrounding interpretation and exclude bare URLs. The visual and final reply still consume the same per-source allowance.

| URL / source | Current approximate reuse | Guidance for remaining artifacts |
|---|---:|---|
| Legora, `scaling-search-for-legal-ai` | Roughly 145–165 words across note, main examples, and classifications | Keep new detail very short; move existing detail instead of repeating it |
| Glean, `user-guide/assistant/team-chat` | Roughly 130–155 words across note, main paragraph, and permissions table | Use a short map label; avoid another full explanation in the visual |
| Claude, `12489464-use-enterprise-search` | Roughly 95–120 words | Room remains, but indexing and retention are distinct |
| Workday agent security / Databricks Genie Ontology | Individually roughly 75–105 words | Existing qualifications can fit in compact rows |

Do not count the same document as a new source merely because a URL has a fragment, locale variant, or redirect. Shortening a citation label alone does not reduce source-derived substance. Most other notes deliberately distribute claims across separate primary pages and leave substantial headroom.

## Scope and evidence assessment

The combined package substantially covers the user's request: organizational meaning, RAG and graphs, vertical work, multiplayer collaboration, enterprise platforms, and deployment at scale. Proprietary schemas are generally marked unknown, and hypothetical domain models are clearly identified. No unsupported universal graph-backend assertion was found.

The reviewed qualification of Glean Team chat and Databricks Genie Ontology matches current documentation. The Microsoft connector contradiction is properly reported rather than converted into an availability claim. Palantir's external-side-effect boundary and the differing permission models are also preserved correctly.

The added market comparison resolves the original gap between broad architectural families and concrete product placement. It includes Atlassian, Notion, and Slack; its evidence labels and feature boundaries are appropriately qualified. The report also distinguishes infrastructure libraries from end-user products. Keep those distinctions in the visual.

The review recommended a short **proposed ontology lifecycle** joining domain ownership, inferred-assertion acceptance, versioned mappings, dependent-view invalidation, correction, and retirement. **Author follow-up:** this is now included in section 3 of the main report, explicitly labeled as a proposed design.

For Claude, retain the feature-specific no-indexing qualification: the same [source](https://support.claude.com/en/articles/12489464-use-enterprise-search) says results remain with their chats. The current text does not assert zero retention; the market map should not introduce that implication.

## Final artifact validation

Author validation after the factual review: the explorer rendered at 728px in light mode and 360px in dark mode without console errors. Browser checks exercised all 23 product cards, all eight populated family filters, six architecture layers, six query examples, four sharing modes, five scenario steps, changed-approval behavior, and keyboard tab navigation. No horizontal overflow was found in those states at 360px. All local Markdown links resolve; the main report's 47 directly cited source URLs and the explorer's 54 source URLs are present in the 111-URL source index. These are artifact checks, not tests of the vendors' products.
