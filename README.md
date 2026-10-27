<p align="center"><img src="logo.png" width="96" alt="Record Meeting logo"></p>

# Record Meeting MCP server

[Record Meeting](https://recordmeeting.com) records your Google Meet, Zoom, Microsoft Teams and other online meetings, transcribes them with speaker names and writes AI meeting notes. Its hosted MCP server lets your AI assistant work with those recordings: ask what a team decided, who owns which action item, or what a customer asked for, and the assistant finds the right meeting and answers from its notes and transcript.

**Server URL:** `https://api.recordmeeting.com/mcp` (Streamable HTTP, OAuth 2.1 with dynamic client registration)

There is nothing to install or run. Point your client at the URL, sign in to Record Meeting in the browser window that opens, and approve the scopes on the consent page. You can revoke access at any time in Record Meeting under Settings, Connected agents.

## Tools

| Tool | What it does |
| --- | --- |
| `list_recordings` | Browse and filter your personal or team recordings |
| `search_recordings` | Find recordings by title |
| `get_recording_by_date` | Recordings from a given day or range, in your time zone |
| `get_recording` | Details, AI notes, participants and sharing state of a recording |
| `get_transcript` | Speaker-labelled transcript, page by page |
| `get_share_link` | Read the existing public share link of a recording |
| `update_recording` | Rename a recording or replace its notes |
| `delete_recording` | Permanently delete a recording (asks first) |
| `create_share_link` | Create or rotate the public share link of a recording |
| `list_organizations` | Teams you belong to |
| `list_folders` | Folders of a team workspace |
| `list_members` | Members of a team workspace |

The server only reaches the recordings your Record Meeting account can open. It does not start recordings: you record with the Record Meeting Chrome extension, the Google Meet add-on or the web app.

## Connect

**Claude.ai, Claude Desktop and Cowork:** install it from the [Claude connectors directory](https://claude.ai/directory/recordmeeting), or add a custom connector with the server URL.

**ChatGPT:** search for Record Meeting in the ChatGPT apps directory, or add the server URL as a connector in developer mode.

**Claude Code**

```bash
claude mcp add --transport http recordmeeting https://api.recordmeeting.com/mcp
```

Or install this repository as a plugin:

```bash
claude plugin marketplace add Qualtir/RecordMeetingMCP
claude plugin install recordmeeting@recordmeeting
```

**Cursor, VS Code, Windsurf and other clients that read `mcp.json`**

```json
{
  "mcpServers": {
    "recordmeeting": {
      "url": "https://api.recordmeeting.com/mcp"
    }
  }
}
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/Qualtir/RecordMeetingMCP
```

**Codex:** add to `~/.codex/config.toml`

```toml
[mcp_servers.recordmeeting]
url = "https://api.recordmeeting.com/mcp"
```

Clients without OAuth support can send a Record Meeting API key instead, as `Authorization: Bearer sk_rm_...`. Create one at [recordmeeting.com/app/settings](https://recordmeeting.com/app/settings), in the API keys section.

Step-by-step setup for every client: [recordmeeting.com/agent-setup](https://recordmeeting.com/agent-setup).

## Example prompts

- What did we decide about pricing in last week's product sync?
- What are the next steps from my call with Harbor Logistics?
- Which meetings did I record yesterday?
- Show me the transcript of the Sprint 42 planning meeting.
- Create a share link for the weekly product sync recording.

## About this repository

This repository holds the client manifests for the hosted server: `server.json` for the [official MCP Registry](https://registry.modelcontextprotocol.io), `.claude-plugin/` for Claude Code, `.cursor-plugin/` and `mcp.json` for Cursor, and `gemini-extension.json` for Gemini CLI. The server itself runs at `api.recordmeeting.com` and is not part of this repository.

## Links

- [Documentation](https://support.recordmeeting.com/user-guide/mcp-server/)
- [Support](https://support.recordmeeting.com) or support@recordmeeting.com
- [Privacy policy](https://recordmeeting.com/privacy)
- [Terms](https://recordmeeting.com/terms)
