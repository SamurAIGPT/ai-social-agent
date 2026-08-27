---
name: Social Project Setup
slug: social-project-setup
version: 1.0.0
category: social
description: Establish reusable brand, account, platform, content, approval, and measurement context for social workflows.
status: ready
muapi_capabilities: []
required_connections: []
permissions:
  - read-only
  - workspace-write
---

# Social Project Setup

## Mission

Create a small, explicit project context so listening, creator research,
trend analysis, content adaptation, publishing, and performance reporting use
the correct brand, accounts, platforms, markets, and measurement scope. This
is setup and intake, not a publishing run.

## Required inputs

- Canonical brand or organization name and products/services.
- Official handles, profile URLs, and owned account labels for each platform.
- Target platforms, countries/languages, audiences, and communities.
- Campaign or business goal and success metrics.
- Content sources, media assets, brand voice, claims, and restricted topics.
- Approval owners, publishing permissions, preferred timezone, and cadence.
- Optional competitors, reference creators, hashtags, keywords, and date range.

## Workflow

1. Confirm the canonical identity and record supplied handles and URLs. Do not
   infer an official account from a similar name.
2. Inventory owned accounts and their status through the host's secure Muapi
   connection when available. Record the account ID, platform, label,
   `connected` state, and owner; do not copy tokens.
3. Define the audience, market, language, content formats, campaign objective,
   approval owner, and reporting timezone.
4. Separate research scope from publishing scope. A public competitor or
   creator profile is not an owned publishing account.
5. Inventory measurement sources. Ask whether the host can supply public
   retrieval data, platform-native account analytics, GA4/other analytics,
   server analytics, or user-provided exports. Record each as `connected`,
   `user-supplied`, `partial`, or `unavailable` with date coverage, filters,
   sampling, attribution, and privacy constraints.
6. Explain that public post counts can support comparative content analysis,
   while reach, impressions, audience data, conversions, and revenue require
   the relevant host-supplied analytics source.
7. Save `.social/project.md` only when the user asks to retain the context.

## Secure host boundary

The host owns Muapi/API credentials, platform OAuth, analytics connectors, and
file access. Never request or store API keys, OAuth tokens, cookies, private
audience data, or customer identifiers in the project file or chat.

## Suggested project file

~~~markdown
# Social project

## Identity
- Canonical brand:
- Products/services:
- Brand voice:
- Restricted claims/topics:

## Owned accounts
- Platform:
- Handle/profile URL:
- Account label/ID:
- Connection status:
- Owner:

## Audience and market
- Audience/personas:
- Countries:
- Languages:
- Communities:

## Campaign and content
- Objective:
- Success metrics:
- Content sources/assets:
- Formats:
- Approval owner:
- Publishing timezone:

## Measurement
- Public retrieval sources:
- Platform-native analytics source/status:
- GA4 or other analytics source/status:
- Server analytics source/status:
- Date range:
- Attribution window:
- Privacy/consent constraints:
~~~

## Failure behavior

If identity, account ownership, or publishing scope is ambiguous, stop before
any write call and ask for the specific missing value. If measurement access
is unavailable, preserve the project context and mark the affected metrics
unavailable rather than estimating them.
