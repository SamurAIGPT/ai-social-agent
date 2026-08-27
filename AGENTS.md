# AI social capability instructions

This repository contains instruction-only social workflows. The host
assistant supplies reasoning, approvals, file access, the secure Muapi MCP or
REST connection, and any web, platform-analytics, or export access. The
skills do not contain a social API client or credential store.

When this package is available in a project:

1. Read `references/muapi-social-tools.md` before selecting a Muapi task.
2. Read `.social/project.md` and prior `.social/reports/` or
   `.social/sources/` files when they exist.
3. Confirm the brand, handles, owned accounts, target platforms, audience,
   country/language, content scope, date range, timezone, and success metric.
4. Verify a capability with a successful host/Muapi response before calling it.
   A task name, catalog entry, or planned capability is not proof that it is
   available in the current host.
5. Announce potentially expensive work before large post samples, repeated
   snapshots, creator sweeps, or broad platform coverage.
6. Preserve task/provider names, request IDs, timestamps, billing, filters,
   raw results, and exact errors in reports when the host makes them available.
7. Keep public post metrics, owned-account analytics, web evidence, and
   assistant-derived analysis as separate evidence types.
8. Treat unsupported scope as unknown, not zero. Never invent posts, creators,
   followers, engagement, reach, sentiment, trends, conversions, or platform
   availability.
9. Keep Muapi keys, OAuth tokens, platform secrets, and private customer data
   in the host's secure settings. Never request them in chat or save them in
   `.social/` or repository files.
10. Publishing, scheduling, editing, and deleting are write actions. Present
    the complete platform-specific draft and require explicit human approval
    before any write call. Re-check the target account immediately before
    publishing.

Use the smallest skill that answers the request. Use `social-project-setup`
for reusable brand/account/measurement context, `multi-platform-publishing`
for approved writes, and the research skills only for the platform scope they
can actually cover.

## Local artifact convention

When the user asks to save work, use:

~~~text
.social/
  project.md
  reports/YYYY-MM-DD/<run-slug>.md
  sources/YYYY-MM-DD/<run-slug>/<tool-name>.json
  snapshots/YYYY-MM-DD/<run-slug>.json
~~~

Keep raw supplied exports separate from calculated tables and drafted copy.
