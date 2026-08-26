# AI Social Agent

An AI agent for social media management — listening, creator discovery, multi-platform publishing, and trend research across X, Instagram, TikTok, Reddit, and YouTube — backed by real social-data APIs.

Part of [Agency Agents OS](https://github.com/Anil-matcha/agency-agents-os), an open ecosystem of specialized AI agents for real business work.

## What this covers

This repo is the umbrella for anything an agency or in-house team would call "the AI social agent": knowing what's being said about a brand or topic, finding the right creators to work with, adapting one piece of content for each platform's format, and understanding what's currently working in a niche — without manually monitoring five different apps.

## Sub-agents

| Agent | Does | Status |
|---|---|---|
| [Social Listening](agents/social-listening/SKILL.md) | Monitor brand/topic mentions and sentiment across platforms | Coming Soon |
| [Creator Discovery](agents/creator-discovery/SKILL.md) | Find relevant creators/influencers for a campaign by niche and audience fit | Coming Soon |
| [Multi-Platform Publishing](agents/multi-platform-publishing/SKILL.md) | Adapt and schedule one piece of content across multiple platforms with platform-appropriate formatting | Coming Soon |
| [Trend Discovery](agents/trend-discovery/SKILL.md) | Surface what's currently working/trending in a niche to inform content strategy | Coming Soon |
| [Platform Research](agents/platform-research/SKILL.md) | Deep research on a platform's community/subreddit/audience before launching content there | Coming Soon |

## Required Muapi APIs

- `social.read_posts` — pull posts/mentions/comments for a brand, topic, or account across supported platforms.
- `social.publish_post` — publish or schedule a post to a connected platform account.
- `social.search_creators` — search creators/accounts by niche, audience size, and engagement signals.
- `social.sentiment_analysis` — classify sentiment and surface themes across a set of posts/mentions.

See each sub-agent's `SKILL.md` for the specific capabilities it uses.

## Setup

1. Create a Muapi account and API key at [muapi.ai](https://muapi.ai).
2. Review the [Muapi API quickstart](https://muapi.ai) and [OpenAPI schema](https://api.muapi.ai/openapi.json) for the social-data endpoints.
3. Load the `SKILL.md` for the sub-agent you need into your agent runtime (hosted agent, MCP client, or custom LLM app), or follow it manually.

## Read-only vs. write actions

Social listening, creator discovery, trend discovery, and platform research are `read-only` — they surface information, they don't post anything. Multi-platform publishing is `requires-approval-to-publish` — a draft is prepared for each platform, but nothing goes out until a human explicitly approves it.

## Status and limitations

All five sub-agents are Coming Soon. They depend on the `social.*` capabilities above, which are not yet live on Muapi. Each `SKILL.md` documents the intended workflow and API surface so integration can start as soon as those capabilities ship, and explains exactly how the agent should fail (not fabricate data) until then.

## Contributing

See [Agency Agents OS CONTRIBUTING.md](https://github.com/Anil-matcha/agency-agents-os/blob/main/CONTRIBUTING.md).

## License

[MIT](LICENSE)
