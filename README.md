# AI Social Agent

An AI agent for social media management — listening, creator discovery, multi-platform publishing, and trend research across X, Instagram, TikTok, Reddit, YouTube, Facebook, LinkedIn, Threads, and Pinterest — backed by real social-data APIs.

Part of [Agency Agents OS](https://github.com/Anil-matcha/agency-agents-os), an open ecosystem of specialized AI agents for real business work.

## Related Projects

- [Agency Agents OS](https://github.com/Anil-matcha/agency-agents-os) — the central catalog this repo is part of.
- [ai-youtube-agent](https://github.com/SamurAIGPT/ai-youtube-agent) — uses this repo's `social.publish` capability to actually upload optimized videos to YouTube.
- [ai-content-repurposing-agent](https://github.com/SamurAIGPT/ai-content-repurposing-agent) — feeds this repo's multi-platform-publishing sub-agent with clipped video.
- [ai-image-agent](https://github.com/SamurAIGPT/ai-image-agent) — supplies image posts for this repo to publish.
- [ai-marketing-agent](https://github.com/SamurAIGPT/ai-marketing-agent) — plans the campaigns this repo publishes and monitors.
- [ai-reputation-agent](https://github.com/SamurAIGPT/ai-reputation-agent) — shares this repo's sentiment/listening data sources.
- [MuAPI MCP docs](https://muapi.ai/docs/mcp) — connect this repo's `SKILL.md` files via MCP.
- [MuAPI API reference](https://muapi.ai/docs/api-reference) — request/poll pattern used by the live `social.publish` endpoint.
- [MuAPI access keys](https://muapi.ai/access-keys) — create the API key this agent needs.

## What this covers

This repo is the umbrella for anything an agency or in-house team would call "the AI social agent": knowing what's being said about a brand or topic, finding the right creators to work with, adapting one piece of content for each platform's format, and understanding what's currently working in a niche — without manually monitoring five different apps.

## Sub-agents

| Agent | Does | Status |
|---|---|---|
| [Social Listening](agents/social-listening/SKILL.md) | Monitor brand/topic mentions and sentiment across platforms | Coming Soon |
| [Creator Discovery](agents/creator-discovery/SKILL.md) | Find relevant creators/influencers for a campaign by niche and audience fit | Coming Soon |
| [Multi-Platform Publishing](agents/multi-platform-publishing/SKILL.md) | Adapt and schedule one media post across YouTube, TikTok, Instagram, Facebook, LinkedIn, X, Threads, and Pinterest | Blueprint |
| [Trend Discovery](agents/trend-discovery/SKILL.md) | Surface what's currently working/trending in a niche to inform content strategy | Coming Soon |
| [Platform Research](agents/platform-research/SKILL.md) | Deep research on a platform's community/subreddit/audience before launching content there | Coming Soon |

## Required Muapi APIs

Live today:

- `social.list_accounts` (`GET /social/accounts`) — list the user's connected social accounts.
- `social.publish` (`POST /social/publish`) — publish or schedule a media post (image/video required) to a connected account on YouTube, TikTok, Instagram, Facebook, LinkedIn, X, Threads, or Pinterest.
- Scheduled-post management: `GET /social/posts`, `PATCH /social/posts/{id}`, `DELETE /social/posts/{id}`.

Not yet live (needed by the other four sub-agents):

- `social.read_posts` — pull posts/mentions/comments for a brand, topic, or account.
- `social.search_creators` — search creators/accounts by niche, audience size, and engagement signals.
- `social.sentiment_analysis` — classify sentiment and surface themes across a set of posts/mentions.

See each sub-agent's `SKILL.md` for the specific capabilities it uses.

## Setup

1. Create a Muapi account and API key at [muapi.ai](https://muapi.ai).
2. Review the [Muapi API quickstart](https://muapi.ai) and [OpenAPI schema](https://api.muapi.ai/openapi.json) for the social-data endpoints.
3. Load the `SKILL.md` for the sub-agent you need into your agent runtime (hosted agent, MCP client, or custom LLM app), or follow it manually.


## Using with an AI agent

Every sub-agent's `SKILL.md` is model- and runtime-agnostic — it's plain Markdown, so it works with any LLM agent, not just Claude. Two integration paths:

**As an MCP connection (the agent gets live Muapi tools):**

Muapi runs an MCP server at `https://api.muapi.ai/mcp` that any MCP-compatible client can connect to — Cursor, Windsurf, Claude, or your own custom agent.

- **Cursor / Windsurf / other clients with a header field:** connect to `https://api.muapi.ai/mcp` with an `Authorization: Bearer YOUR_MUAPI_KEY` header.
- **claude.ai / Claude Cowork / other connector UIs with no header field:** use the URL-embedded key form instead, `https://api.muapi.ai/mcp/YOUR_MUAPI_KEY`, via Settings → Connectors → Add custom connector.
- **Claude Code / Claude Desktop:** `claude mcp add muapi -e MUAPI_API_KEY=YOUR_MUAPI_KEY -- muapi mcp serve` (uses the muapi CLI's stdio transport — Claude Code's HTTP MCP client doesn't reliably inject tools).

Full setup details for every client: [muapi.ai/docs/mcp](https://muapi.ai/docs/mcp).

**As agent instructions (any LLM follows the workflow directly):**

Drop a sub-agent's `SKILL.md` into a Claude Code project's `.claude/skills/` directory, paste it into a custom-GPT/Project's system instructions, hand it to an autonomous agent framework as a tool spec, or attach it directly in a chat conversation — then ask the agent to follow it.

## Read-only vs. write actions

Social listening, creator discovery, trend discovery, and platform research are `read-only` — they surface information, they don't post anything. Multi-platform publishing is `requires-approval-to-publish` — a draft is prepared for each platform, but nothing is published or scheduled until a human explicitly approves it.

## Status and limitations

Multi-Platform Publishing is **Blueprint** — built on `social.list_accounts` and `social.publish`, both live on Muapi today, but not yet verified end-to-end from inside this repo. Note it publishes to eight platforms, not Reddit (Reddit isn't a supported publish target on Muapi's social API — it's still useful for Platform Research). The other four sub-agents are **Coming Soon** — they depend on `social.read_posts`, `social.search_creators`, and `social.sentiment_analysis`, none of which are live yet.

## Contributing

See [Agency Agents OS CONTRIBUTING.md](https://github.com/Anil-matcha/agency-agents-os/blob/main/CONTRIBUTING.md).

## License

[MIT](LICENSE)
