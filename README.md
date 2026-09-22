# GovInbox MCP

This repo is the public server card and connect notes for GovInbox. The MCP server is hosted. There is nothing to run locally.

GovInbox is a daily watch on U.S. federal set-aside contract opportunities. It pulls new set-aside notices from the official SAM.gov API every 4 hours, matches them to your programs, NAICS codes, keywords and states, and writes a plain-English brief for each match. The digest is pull-only: you or your AI agent opens it on demand. No email delivery, no scheduled push.

Requires a GovInbox subscription. Checkout is open at https://getgovinbox.com

## Pricing

- Core: $19/mo or $190/yr
- Pro: $49/mo or $470/yr
- Team: $99/mo or $990/yr
- 7-day no-card Core trial, one per person or business. The trial starts on first use.
- Cancel anytime; access runs to the end of the paid period.

## Get your access token

Subscribe or start the trial at https://getgovinbox.com. Your access token is issued after checkout or trial confirmation. The CLI stores it for you (`govinbox login`). Use your GovInbox token, not a SAM.gov API key. Never paste the token into a chat. Treat your MCP client config as a secret.

## Connect your agent

Remote MCP endpoint: `https://mcp.getgovinbox.com/mcp` (Streamable HTTP).

The reliable path is a bearer header:

```json
{
  "mcpServers": {
    "govinbox": {
      "url": "https://mcp.getgovinbox.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_GOVINBOX_TOKEN" }
    }
  }
}
```

If your client supports OAuth 2.1 discovery (Claude, Cursor, most MCP hosts), it can log in on its own:

```json
{
  "mcpServers": {
    "govinbox": {
      "url": "https://mcp.getgovinbox.com/mcp"
    }
  }
}
```

OAuth flow: register with `POST https://mcp.getgovinbox.com/oauth/register`, approve at `https://mcp.getgovinbox.com/oauth/authorize` (sign in with your GovInbox token), tokens from `POST https://mcp.getgovinbox.com/oauth/token`. Discovery: `https://mcp.getgovinbox.com/.well-known/oauth-authorization-server` and `https://mcp.getgovinbox.com/.well-known/oauth-protected-resource`. PKCE S256 with dynamic client registration.

Scopes: `govinbox:read` (search and read), `govinbox:write` (manage watchlists). A 401 means the token is missing, expired, or revoked: get a fresh token and try again.

## Tools

Each tool costs 1 quota unit.

- `search_opportunities` — search set-aside contracts by keyword, program, NAICS, agency, deadline
- `get_opportunity` — full record for one notice id (brief, deadline, place of performance, links)
- `search_grants` — federal grant postings from Simpler.Grants.gov (assistance, not contracts)
- `search_savings` — DOGE-reported terminated contracts and cancelled grants (recompete signals)
- `list_watchlist` — pinned notices as cards
- `manage_watchlist` — `add` / `remove` / `clear` pins

Registry name: `com.getgovinbox/govinbox`. Machine-readable server card: `server.json` in this repo, also served at `https://mcp.getgovinbox.com/.well-known/mcp.json`. Full machine docs: https://getgovinbox.com/for-ai

## Also available

- REST API: `https://api.getgovinbox.com` (Bearer token)
- CLI: `pip install govinbox`, then `govinbox login` (https://pypi.org/project/govinbox/, needs Python 3.10+)

## Support

Email support@getgovinbox.com. See SECURITY.md for vulnerability reports and token-handling rules.
