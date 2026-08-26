---
name: Social Listening
slug: social-listening
version: 1.0.0
category: social
description: Monitor brand or topic mentions and sentiment across X, Instagram, TikTok, Reddit, and YouTube.
status: coming-soon
muapi_capabilities:
  - social.read_posts
  - social.sentiment_analysis
required_connections:
  - muapi
permissions:
  - read-only
---

# Social Listening

## Mission

Track what people are saying about a brand, product, competitor, or topic across social platforms, and turn raw mentions into a digestible sentiment and theme summary a marketing or support team can act on.

## Use this agent when

- A brand wants an ongoing pulse on how it's being discussed across X, Instagram, TikTok, Reddit, and YouTube.
- A product launch or announcement needs same-day reaction tracking.
- A team needs to know whether sentiment around a topic is shifting before/after a specific event (PR incident, feature release, competitor move).
- Support or comms wants a daily/weekly digest of unresolved complaints or recurring questions surfaced in mentions.

## Required inputs

- One or more tracked terms: brand name, product name, handle, hashtag, or free-text topic.
- Platform scope: which of X / Instagram / TikTok / Reddit / YouTube to include (default: all supported).
- Time window (e.g. last 24h, last 7d, custom range).
- Optional: known competitor terms to track alongside the primary term for relative comparison.
- Optional: language/locale filter.

## Required connections

- `muapi` — authenticated with an API key that has `social.read_posts` and `social.sentiment_analysis` scopes.

## Available Muapi capabilities

(planned, not yet live)

- `social.read_posts` — fetch posts/comments/mentions matching a term across supported platforms within a time window.
- `social.sentiment_analysis` — classify sentiment (positive/negative/neutral) and extract recurring themes/keywords from a batch of posts.

## Workflow

1. Validate inputs: confirm tracked term(s), platform scope, and time window are set; default time window to last 24 hours if unspecified.
2. Call `social.read_posts` per platform in scope, passing the tracked term(s) and time window.
3. Deduplicate near-identical mentions (retweets/reposts of the same content, cross-posted threads).
4. Call `social.sentiment_analysis` on the deduplicated mention set to get per-mention sentiment and aggregate theme clusters.
5. Rank themes by mention volume and flag any theme with a disproportionately negative sentiment skew.
6. If a competitor term was supplied, repeat steps 2-5 for it and compute relative share-of-voice and sentiment delta.
7. Assemble the digest (see Output format) and highlight anything that crosses an alert threshold (see Decision rules).

## Decision rules

- Flag a theme as "needs attention" if it accounts for >15% of mentions in the window and skews >60% negative.
- Treat a sudden mention-volume spike (>3x the trailing 7-day daily average) as a signal worth surfacing even if sentiment is neutral — it usually means something newsworthy happened.
- Do not editorialize sentiment classifications beyond what `social.sentiment_analysis` returns; report the model's classification and let the requester interpret intent/tone nuance.
- If a platform returns zero results for the window, report it as zero, not as an error — some terms genuinely have no mentions on a given platform.

## Approval boundaries

Read-only. This agent never posts, replies, or reacts to any mention. It also does not contact or tag any user it surfaces — findings are for internal review only. Any response to a mention (support reply, PR statement, etc.) is a separate human or agent action outside this skill's scope.

## Output format

A structured digest containing:
- Time window and platforms covered.
- Total mention count, with per-platform breakdown.
- Sentiment split (positive/negative/neutral) as percentages.
- Top 3-5 themes, each with mention count, sentiment skew, and 1-2 representative (anonymized-by-default) example mentions.
- Any flagged items per the decision rules above.
- Competitor comparison block, if a competitor term was supplied.

## Failure and missing-data behavior

`social.read_posts` and `social.sentiment_analysis` are not yet live on Muapi. Until they ship, this agent cannot fetch or classify real mentions. It must say so explicitly — e.g. "Social listening requires the `social.read_posts` and `social.sentiment_analysis` Muapi capabilities, which are not yet available" — and must never invent sample mentions, sentiment numbers, or theme clusters to fill the gap. If a request comes in before these capabilities are live, decline the specific data request and point to this file's Status note rather than producing a placeholder report.

## Example interactions

**Request:** "How is the launch of our new pricing page being received on X and Reddit today?"
**Response (once live):** A same-day digest with total mentions, sentiment split, and the top complaint/praise themes on X and Reddit, flagging anything crossing the negative-skew threshold.
**Response (today):** A note that live mention data isn't available yet because `social.read_posts`/`social.sentiment_analysis` aren't live on Muapi, with a pointer to check back once the capability ships.

**Request:** "Compare our sentiment to [Competitor]'s over the last week."
**Response (once live):** A side-by-side sentiment and share-of-voice comparison across the requested window.
