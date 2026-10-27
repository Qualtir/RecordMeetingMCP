# Installing the Record Meeting MCP server

Record Meeting is a hosted MCP server. There is nothing to clone, build or run locally.

1. Add this entry to the client's MCP settings. For Cline, that is `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "recordmeeting": {
      "type": "streamableHttp",
      "url": "https://api.recordmeeting.com/mcp"
    }
  }
}
```

2. The first request returns a 401 that points the client to the OAuth metadata (`https://api.recordmeeting.com/.well-known/oauth-protected-resource/mcp`). The client registers itself (dynamic client registration) and opens a browser window. The user signs in to Record Meeting and clicks Allow on the consent page.

3. If the client cannot do OAuth, ask the user for a Record Meeting API key instead. They create one at https://recordmeeting.com/app/settings, in the API keys section (it is shown once). Then send it as a header:

```json
{
  "mcpServers": {
    "recordmeeting": {
      "type": "streamableHttp",
      "url": "https://api.recordmeeting.com/mcp",
      "headers": { "Authorization": "Bearer sk_rm_..." }
    }
  }
}
```

4. Check the connection by calling `list_recordings`. An empty list means the account has no completed recordings yet, and the connection still works.

Full setup guide for every client: https://recordmeeting.com/agent-setup/prompt.md
