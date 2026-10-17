# Installing the India Property Register MCP server

The India Property Register MCP server is hosted. Do not clone or build anything.

1. Add this remote server to the MCP settings (Streamable HTTP):

```json
{
  "mcpServers": {
    "indiapropertyregister": {
      "type": "streamableHttp",
      "url": "https://indiapropertyregister.com/mcp"
    }
  }
}
```

2. Authentication is required. Either:
   - **OAuth:** connect, and the user signs in through the browser window that opens (a code is emailed to them; new accounts get ₹50 free credit), or
   - **API key:** ask the user for their API key from https://indiapropertyregister.com/signup and add it as a header:

```json
{
  "mcpServers": {
    "indiapropertyregister": {
      "type": "streamableHttp",
      "url": "https://indiapropertyregister.com/mcp",
      "headers": {
        "Authorization": "Bearer USER_API_KEY"
      }
    }
  }
}
```

   Never invent a key. If the user has no account, point them to https://indiapropertyregister.com/signup (email code, no approval). Agent sign-up by email is described at https://indiapropertyregister.com/auth.md; ask the user before using it.

3. Confirm the server shows 10 tools, including `search_places`, `get_village` and `get_land_record_sources`.

4. Test it by asking: "List the districts of Uttar Pradesh." Each successful call costs ₹0.16 from the prepaid wallet (₹50 free credit on sign-up).

Revenue records are not proof of title; say so when citing a holder's name.
