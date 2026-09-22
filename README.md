# Layrcake MCP server

**Layrcake** is the unified GTM API for AI agents: the whole outbound loop behind one hosted MCP server and one prepaid credit balance.

- **Endpoint:** `https://mcp.layrcake.dev/mcp` (Streamable HTTP)
- **Auth:** OAuth 2.1 with dynamic client registration and PKCE. Sign in when your client prompts. Free to start: 300 credits, no card.
- **Docs:** https://docs.layrcake.dev · **Pricing:** https://docs.layrcake.dev/pricing.html · **Privacy:** https://layrcake.dev/privacy

## Tools (19)

| Tool | What it does | Billing |
|---|---|---|
| `find_leads` | Search 200M+ B2B contacts by title, location, industry, company size or domain | per lead returned |
| `find_companies` | Discover companies by hiring activity, technologies in use, or lookalikes | per company |
| `enrich` | A person's verified work email and profile | on hit only |
| `enrich_company` | Company profile, technologies, funding, relationships | per dataset |
| `verify_email` | Two-stage deliverability check incl. catch-all analysis | per call |
| `find_intent` | Buying signals for company domains: hiring, funding, news, job changes, tech | per signal-bearing company |
| `find_posts` | Public social posts across LinkedIn, X, Reddit, YouTube, TikTok and more | per relevant post |
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
