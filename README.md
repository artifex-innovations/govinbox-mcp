# GovInbox MCP

GovInbox is a daily watch on U.S. federal set-aside contract opportunities. It pulls new set-aside notices from the official SAM.gov API every 4 hours, matches them to your programs, NAICS codes, keywords and states, and writes a plain-English brief for each match. Requires a GovInbox subscription. Checkout is open at https://getgovinbox.com

## Connect your agent

Remote MCP endpoint: `https://mcp.getgovinbox.com/mcp` (Streamable HTTP).

If your client supports OAuth discovery, it logs in on its own. Copy-paste config:

```json
{
  "mcpServers": {
    "govinbox": {
      "url": "https://mcp.getgovinbox.com/mcp"
    }
  }
}
```

If your client cannot run the OAuth flow, use your access token as a bearer header:

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

Login details: OAuth 2.1 with PKCE at `https://mcp.getgovinbox.com/oauth/authorize`, discovery at `https://mcp.getgovinbox.com/.well-known/oauth-authorization-server`. Scopes: `govinbox:read` (search and read), `govinbox:write` (manage watchlists).

## Tools

- `search_opportunities` — search set-aside contracts by keyword, program, NAICS, agency, deadline
- `get_opportunity` — full record for one notice (brief, deadline, place of performance, links)
- `search_grants` — federal grant postings
- `search_savings` — DOGE-reported terminated contracts and cancelled grants (recompete signals)
- `list_watchlist` / `manage_watchlist` — pinned notices

## Also available

- REST API: `https://api.getgovinbox.com` (Bearer token). Full machine docs: https://getgovinbox.com/for-ai
- CLI: `pip install govinbox`, then `govinbox login` (https://pypi.org/project/govinbox/)
- Machine-readable server card: this repo's `server.json`, also served at `https://mcp.getgovinbox.com/.well-known/mcp.json`

## Support

Email support@getgovinbox.com. See SECURITY.md for vulnerability reports.
