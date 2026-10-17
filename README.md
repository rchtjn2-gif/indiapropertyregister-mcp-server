<p align="center"><img src="logo-400.png" alt="India Property Register MCP server logo" width="120"></p>

# India Property Register MCP Server: every state, district, tehsil and village in India for AI agents

> Look up any Indian state, district, tehsil or village with its LGD code, boundary and pincodes, and find which government portals hold its land records, from Claude, ChatGPT, Cursor, Cline or any MCP client. For property due diligence, lending, proptech and research.

**MCP endpoint:** `https://indiapropertyregister.com/mcp` · **Transport:** Streamable HTTP · **Auth:** OAuth 2.1 or API key · **Tools:** 10 · **Website:** [indiapropertyregister.com](https://indiapropertyregister.com)

This repository is the public listing for the **hosted** India Property Register MCP server: connection instructions, the registry manifest (`server.json`) and client config files. There is nothing to install or self-host; the server runs at the URL above.

## Connect in one step

Add this URL to any MCP client that supports remote servers:

```
https://indiapropertyregister.com/mcp
```

Clients with OAuth support open a browser sign-in on first connect (sign in with a code emailed to you, or create an account with ₹50 free credit). Clients without OAuth can send an API key instead (see [Authentication](#authentication)).

### Cline
Open Cline → MCP Servers → **Remote Servers**, name it `indiapropertyregister`, paste the URL above and click Add. Or add this to `cline_mcp_settings.json`, with an API key from [indiapropertyregister.com/signup](https://indiapropertyregister.com/signup):
```json
{
  "mcpServers": {
    "indiapropertyregister": {
      "type": "streamableHttp",
      "url": "https://indiapropertyregister.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

### Claude (claude.ai, Claude Desktop, Claude mobile)
Settings → Connectors → **Add custom connector** → paste the URL above → Connect, then sign in.

### Claude Code
```bash
claude mcp add --transport http indiapropertyregister https://indiapropertyregister.com/mcp
```
Then run `/mcp` to sign in. Or pass a key: `--header "Authorization: Bearer YOUR_API_KEY"`.

### ChatGPT
Settings → Apps & Connectors → Advanced → enable Developer mode → **Create** a connector → paste the URL above → choose OAuth.

### Cursor, Windsurf and other JSON-config clients
```json
{
  "mcpServers": {
    "indiapropertyregister": {
      "url": "https://indiapropertyregister.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```
Clients that support OAuth can leave out `headers` and sign in on connect.

### VS Code (GitHub Copilot)
Add to `.vscode/mcp.json`:
```json
{
  "servers": {
    "indiapropertyregister": {
      "type": "http",
      "url": "https://indiapropertyregister.com/mcp"
    }
  }
}
```

### Gemini CLI
```bash
gemini extensions install https://github.com/rchtjn2-gif/indiapropertyregister-mcp-server
```

### Clients that only support stdio
Bridge the remote URL with `mcp-remote` (it handles the OAuth sign-in):
```json
{
  "mcpServers": {
    "indiapropertyregister": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://indiapropertyregister.com/mcp"]
    }
  }
}
```

## Authentication
Every call needs an India Property Register account. Two ways:
1. **OAuth 2.1** (authorization code + PKCE, scope `api`): MCP clients do this automatically when given the URL. You sign in with a code emailed to you.
2. **API key:** sign up at [indiapropertyregister.com/signup](https://indiapropertyregister.com/signup) (email code, no approval) and send `Authorization: Bearer <key>`. AI agents can also create a key by email verification, as described in [auth.md](https://indiapropertyregister.com/auth.md). Keys can be revoked at [indiapropertyregister.com/account/keys](https://indiapropertyregister.com/account/keys).

Without a credential, calls return 401; with an empty wallet, 402.

## What data it covers
- **36 states, 783 districts, 6,360 tehsils and 5,86,031 villages**, with Local Government Directory (LGD) codes, Survey of India village boundaries and India Post pincode areas
- How each state keeps its land records (record names such as khatauni, 7/12, RTC, patta, jamabandi; admin hierarchy; plot identifiers) and which government portals hold them
- Plot records are added state by state; see [coverage](https://indiapropertyregister.com/coverage) for what is loaded

Revenue records are not proof of title, and nothing here is a certified copy. India Property Register is independent and not a government website.

## Tools (10)
| Group | Tools |
|---|---|
| Places | `search_places`, `list_states`, `list_districts`, `list_tehsils`, `list_villages`, `get_village` |
| Land records | `get_land_record_sources` |
| Wallet and billing | `get_wallet`, `top_up_wallet`, `get_payment` |

## Example prompts
- "What is the LGD code of Rampur village in this tehsil, and which pincode is it in?"
- "List the tehsils of Pune district."
- "Where are land records for villages in Uttar Pradesh kept, and what is the record called?"
- "Find villages named Sonipat across India."
- "How much credit is left in my India Property Register wallet?"

## Pricing
Prepaid. New accounts get **₹50 free credit**, then **₹0.16 per successful call**; errors are free. Top-ups of ₹500, ₹5,000 or ₹50,000 of credit, plus 18% GST.

## Links
- [API overview](https://indiapropertyregister.com/api)
- [API reference](https://indiapropertyregister.com/api/docs)
- [OpenAPI](https://indiapropertyregister.com/api/v1/openapi.json)
- [auth.md (for AI agents)](https://indiapropertyregister.com/auth.md)
- [llms.txt](https://indiapropertyregister.com/llms.txt)
- [Server card](https://indiapropertyregister.com/.well-known/mcp.json)
- [Coverage](https://indiapropertyregister.com/coverage)
- [Privacy](https://indiapropertyregister.com/privacy)
- [Terms](https://indiapropertyregister.com/terms)

## About this repository
This repo holds listing and configuration files only. The India Property Register MCP server is a hosted service operated by India Property Register; its use is governed by the terms linked above. The files in this repository are released under the MIT licence.
