# Security Policy

## Reporting a vulnerability

Use GitHub's private vulnerability reporting on this repo (Security tab, then Report a vulnerability). Or email support@getgovinbox.com with the subject "Security". Include a description of the issue, steps to reproduce, and the impact.

We aim to acknowledge reports within 48 hours. Please do not disclose the issue publicly until we have had a chance to fix it.

## Token and secret handling

- Never commit your GovInbox token to git, and never paste it into a chat.
- Keep your MCP client config file readable only by you (file mode 600).
- One token per user. If a token leaks, revoke it and get a new one.
- GovInbox tokens are user-scoped API keys. They are not OAuth client secrets and they are not SAM.gov API keys.

## Scope

This policy covers the hosted GovInbox MCP endpoint at mcp.getgovinbox.com and the connect notes in this repo. It also covers api.getgovinbox.com, checkout and token issuance, and the CLI token store.
