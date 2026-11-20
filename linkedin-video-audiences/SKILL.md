---
name: linkedin-video-audiences
description: Build and verify LinkedIn Campaign Manager video-retargeting audiences separated by positioning theme. Use for actual audience creation from existing video ads, not just diagrams or campaign launch.
---

# LinkedIn Video Audiences

Create saved video-engagement audiences that support ongoing follow-up around the positioning theme a viewer watched. Audience creation is the core outcome; attaching audiences, changing ads, budgets or delivery requires the corresponding user scope.

## Establish inputs and authorization

Use supplied context and inspect the account before asking for information already available. Establish:

- The intended advertiser account and its visible identifier.
- A theme-to-source map: positioning statement, source video ads and source ad sets, with identifiers when available.
- Watch threshold, lookback window and audience naming convention.
- Whether the user requests a proposal, saved audiences or additional targeting changes.

Request missing rules before saving audiences if the user has not delegated those choices. You may propose 50% watched and a 90-day lookback as a starting point, but do not treat these as universally optimal or silently use them as approved settings.

A request to build audiences authorizes creating the scoped audiences. Do not ask again merely because Create is an external write. Writing this skill, reviewing a plan or supplying screenshots does not itself authorize live audience creation.

## Choose the available execution path

Before repetitive browser work, use the installed workflow-discovery skill if available to search for LinkedIn video-audience creation. Assess intent and required inputs, not just domain matches. A recording for adding ads is not an audience-creation workflow.

Prefer a connected tool that actually supports audience writes. A reporting connector is not a write integration. Otherwise use supported browser automation in the user's authenticated session. Inspect current page state and use observed controls; do not invent selectors or assume a saved recording can execute itself.

If neither path is available, prepare the exact audience specification and manual steps, then report that creation remains pending. Never claim saved audiences from a draft or diagram.

## Verify source separation before creating anything

Inspect what the current video-audience form allows you to select: individual video ads, ad sets or another source grouping. Confirm the selected source actually corresponds to the intended theme.

LinkedIn's help guide describes choosing source ad sets. If one selectable ad set contains multiple themes and individual ads cannot be isolated, do not label its audience as viewers of one specific theme. Record the limitation and prepare a proposal for theme-separated source ad sets. Do not restructure or launch them under audience-creation authorization alone.

Use existing source objects; do not invent videos or infer their positioning from names alone when content or reliable mapping is available. If source identity is ambiguous, resolve it before saving the affected audience.

## Create one audience per theme

1. Open the confirmed advertiser account in Campaign Manager and navigate to its Audiences area, typically under Plan.
2. Inspect existing audiences for an exact equivalent: account, source identifiers, engagement threshold and lookback. Reuse an equivalent audience and report it rather than creating a duplicate. A matching name alone is insufficient.
3. Follow the observed create path. Screenshots supplied with this workflow show **Create audience → Retargeting audience → Video → Next**. Older help documentation calls the menu option **Matched Audience**. Prefer the current observed interface.
4. Set a clear name, such as `Video | {theme} | {threshold}pct | {lookback}d | {stage}`. Adapt to the user's convention and naming limits.
5. Set the authorized watch threshold and lookback. Select only the verified source objects for this theme.
6. Review the configured rule and save the audience.
7. Read back its detail or rule view and verify its name, sources, threshold, lookback, status and identifier when exposed. Repeat for each theme.

If a save has an ambiguous result, inspect the audience list and details before retrying. Stop the affected action at access failures, unresolvable source ambiguity or an inability to reconcile the save. Preserve verified progress on other audiences.

## Preserve the difference between audiences and delivery

Separate theme audiences can overlap. Watching video A does not establish that the person prefers A over B. Do not promise exclusive theme membership or access to individual viewer identities.

When also asked to configure follow-up targeting, establish which ad sets should include each audience and which should exclude other stages. Explain how exclusions affect people who qualify for multiple themes. Verify the saved targeting after changes.

For later video stages, repeat the source-mapping process using the relevant follow-up video sources. A chain of audiences does not automatically deliver ads in order. Do not claim sequential delivery without verifying the actual targeting and exclusions. Do not activate delivery or change spend unless included in the user's authorization.

Describe the strategy as ongoing or always-on, subject to lookback, eligibility and delivery constraints, rather than permanent individual retention. Created, processing, eligible and delivering are different states.

## Evidence and delivery

Keep private account IDs, captures and execution records in an authorized private location. In an existing private pipeline handoff, record `workflow_lookup`: query, site, decision, selected path/hash if reused and observed outcome.

Report each theme's audience name, source objects, threshold, lookback, saved status and verification result. Distinguish created audiences from reused equivalents, pending processing and unresolved items. Include identifiers only in the user's private context. Never infer audience size from video-view totals.

Before relying on numerical limits or detailed platform mechanics, verify the current official guide and the live interface:

[LinkedIn: Create a video audience](https://www.linkedin.com/help/lms/answer/a427086).

At the November 6, 2026 documentation check, the guide listed 25%, 50%, 75% and 97% watch thresholds; 30, 60, 90, 180 and 365-day lookbacks; and at least 300 matched member accounts to use an audience in targeting. These are dated reference values, not guaranteed future capabilities. Follow observed supported settings and surface discrepancies.

Use no em dashes in user-facing copy.
