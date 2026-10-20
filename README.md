# Layrcake MCP server

**Layrcake** is go-to-market infrastructure for AI agents: one MCP server and API that lets Claude, ChatGPT, Cursor and Codex find leads, verify emails, read buying signals and run approved campaigns, behind one prepaid credit balance.

- **Endpoint:** `https://mcp.layrcake.dev/mcp` (Streamable HTTP)
- **Auth:** OAuth 2.1 with dynamic client registration and PKCE. Sign in when your client prompts. Free to start: 300 credits, no card.
- **Docs:** https://docs.layrcake.dev · **Pricing:** https://docs.layrcake.dev/pricing.html · **Privacy:** https://layrcake.dev/privacy

## Tools (22)

| Tool | What it does | Billing |
|---|---|---|
| `find_leads` | Search 200M+ B2B contacts by title, location, industry, company size or domain | per lead returned |
| `find_companies` | Discover companies by hiring activity, technologies in use, or lookalikes | per company |
| `enrich` | A person's verified work email and profile | on hit only |
| `enrich_company` | Company profile, technologies, funding, relationships | per dataset |
| `verify_email` | Two-stage deliverability check incl. catch-all analysis | per call |
| `find_intent` | Buying signals for company domains: hiring, funding, news, job changes, tech | per signal-bearing company |
| `find_posts` | Public social posts across LinkedIn, X, Reddit, YouTube, TikTok and more | per relevant post |
| `check_companies` | Answer a yes/no question about each company from its own website, with the quoted evidence | per company |
| `research_company` | Dated recent moves for one company, with sources, ranked for your goal | per call |
| `prospect_picture` | One picture of a person, their company, or both: role, recent activity, signals | per call |
| `setup_sending` | Provision warmed sending domains and mailboxes (quote → human approval) | credits, approved in console |
| `create_campaign` | Draft a sequence with variables and recipients; drafts never send | free |
| `add_leads` | Add recipients to a draft campaign through the suppression-safe importer | free |
| `launch_campaign` | Preview → human approval in console → real sends | free |
| `get_replies` / `get_reply` | Read inbound replies, classified | free |
| `set_lead_status` | Record interest; `not_interested` suppresses workspace-wide | free |
| `reply_to_thread` | Preview → human approval → send an in-thread reply | free |
| `get_me` / `get_usage` / `get_operation` / `get_request` | Identity, balance and usage, job and request status | free |

Every tool returns the outcome and the credits it charged. Free reads run without prompting; tools that spend credits or change campaign data are annotated so hosts ask first; anything that sends email or buys capacity always needs a signed-in human to approve at a link the tool returns.

## Connect

```bash
# Claude Code
claude mcp add --transport http layrcake https://mcp.layrcake.dev/mcp
```

```json
{ "mcpServers": { "layrcake": { "type": "http", "url": "https://mcp.layrcake.dev/mcp" } } }
```

Also listed on the [official MCP Registry](https://registry.modelcontextprotocol.io) as `dev.layrcake/layrcake`, [Glama](https://glama.ai/mcp/connectors/dev.layrcake.mcp/layrcake) and [Smithery](https://smithery.ai/servers/layrcake/layrcake).

This repository holds the listing manifest for directories; the server itself is hosted and closed source. Questions: founders@layrcake.dev

## Grok Build

Open `/marketplace` in Grok Build, find **Layrcake**, and install it. On first connection, complete the Layrcake sign-in and consent flow in your browser; new accounts are free with 300 credits and no card. The plugin contains no API key or local executable.

### Network access and permissions

- `https://mcp.layrcake.dev/mcp` — Layrcake's hosted Streamable HTTP MCP endpoint. The same host serves OAuth discovery metadata at `/.well-known/oauth-protected-resource`.
- `https://api.layrcake.dev` — Layrcake's OAuth authorization server (dynamic client registration, token issuance, refresh), discovered from the MCP metadata.
- `https://app.layrcake.dev` — the browser sign-in and consent page, and the console where launches, replies and purchases are approved.

Authentication uses your Layrcake account through browser-based OAuth 2.1 with PKCE. Grok sends the resulting bearer token to the hosted server; the server scopes every tool to your workspace. Six tools are read-only (`get_me`, `get_usage`, `get_operation`, `get_request`, `get_replies`, `get_reply`). The other thirteen are annotated destructive: seven spend prepaid credits against live data providers, three change campaign data, and three (`setup_sending`, `launch_campaign`, `reply_to_thread`) only return a preview and an approval link — nothing is bought or sent until a signed-in human approves in the console. No token or credential is bundled with this plugin.

## License

Proprietary. Use of the hosted service is governed by [Layrcake's terms](https://layrcake.dev/terms) and [privacy policy](https://layrcake.dev/privacy).
