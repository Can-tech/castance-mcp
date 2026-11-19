<p align="center">
  <img src="./assets/logo-mark.svg" alt="Castance" width="64" height="64" />
</p>

<h1 align="center">Castance MCP Server</h1>

<p align="center">
  Post, schedule and measure on 12 social networks, with human approval before anything goes live.
</p>

<p align="center">
  <a href="https://castance.com/ai-agents">Overview</a> ·
  <a href="https://castance.com/integrations">Integrations</a> ·
  <a href="https://castance.com/docs/mcp">MCP Docs</a> ·
  <a href="https://castance.com/docs/permissions">Permissions</a>
</p>

---

**Remote MCP endpoint:** `https://castance.com/mcp` (Streamable HTTP)  
**Authentication:** OAuth 2.1 (with PKCE, Dynamic Client Registration, and Client ID Metadata Documents) or Castance API key (`Authorization: Bearer <key>`)

This public repository contains the official MCP Registry manifest (`server.json`), Gemini CLI extension manifest (`gemini-extension.json`), documentation, and brand icons for the hosted Castance MCP server.

## Supported Social Networks

Instagram, Facebook, Threads, X (Twitter), LinkedIn, TikTok, YouTube, Pinterest, Tumblr, Telegram, Discord, and Google Business Profile.

## Safety & Human-in-the-Loop Approvals

Every MCP connection is scoped to one of three permission levels in Castance:

- **Posts need approval (default for new OAuth connections):** `create_post` proposes posts into your Castance Approvals queue and returns a `reviewUrl`. Nothing is published until a person approves it.
- **Read only:** Read accounts, posts, inbox threads, and analytics without publishing or changing anything.
- **Full access:** Publish, schedule, reply, and manage posts directly.

## Quick Setup

### Claude (Web, Desktop, Mobile)

1. Open Claude's settings and go to **Connectors**.
2. Add a custom connector named **Castance** with URL `https://castance.com/mcp`.
3. Click **Connect**, sign in to Castance, and choose the connection's permission level.

### ChatGPT

1. Open ChatGPT settings → **Apps & Connectors** (enable developer mode if required by your plan).
2. Create a connector with MCP server URL `https://castance.com/mcp` and OAuth sign-in.
3. Sign in to Castance when prompted.

### Claude Code

```bash
claude mcp add --transport http castance https://castance.com/mcp
```

Then run `/mcp` inside Claude Code and select **Castance** to sign in.

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "castance": {
      "url": "https://castance.com/mcp"
    }
  }
}
```

### VS Code (GitHub Copilot)

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "castance": {
      "type": "http",
      "url": "https://castance.com/mcp"
    }
  }
}
```

### Gemini CLI

Install directly as a Gemini CLI extension:

```bash
gemini extensions install https://github.com/Can-tech/castance-mcp
```

Or add Castance to `~/.gemini/settings.json` and run `/mcp auth castance` in Gemini CLI:

```json
{
  "mcpServers": {
    "castance": {
      "httpUrl": "https://castance.com/mcp"
    }
  }
}
```

### Any Agent with an API Key

Create an API key in Castance (choose **Posts need approval** or **Read only** for agents) and pass it as `Authorization: Bearer YOUR_CASTANCE_API_KEY` (or `X-API-Key`).

## Available MCP Tools

| Tool | Description |
| --- | --- |
| `get_context` | Check the connected Castance account, permission level, daily limits, and reachable accounts |
| `list_accounts` / `get_account` | List connected social accounts with `accountId`, platform, and status |
| `list_posts` / `get_post` | Read posts made through Castance or synced from platforms |
| `get_post_status` | Check per-account delivery status, published URLs, or failure reasons |
| `get_analytics` | Read account analytics (followers, reach, views, engagement) |
| `get_usage` | Check Castance balance, monthly posts, and storage |
| `list_approvals` / `get_approval` | Inspect posts waiting for human approval and their status |
| `validate_post` | Run all publishing checks (accounts, platform rules, media, limits) without publishing |
| `create_post` | Publish, schedule, or propose a post for approval |
| `upload_media_from_url` | Store an image, video, or document (up to 100 MB) on Castance media hosting |
| `withdraw_approval` | Withdraw a pending proposed post |
| `update_post` / `delete_post` | Edit or delete a draft or scheduled post (full access) |
| `connect_account` | Generate a browser link for the user to connect another social account |
| `search_api` / `call_api` | Discover and call any of Castance's 790+ REST API operations (comments, DMs, insights, ads, webhooks) |

## Links & Support

- **Overview:** https://castance.com/ai-agents
- **Client Guides:** https://castance.com/integrations
- **Documentation:** https://castance.com/docs/mcp · https://castance.com/docs/permissions
- **Privacy Policy:** https://castance.com/privacy
- **Terms of Service:** https://castance.com/terms
- **Support:** contact@castance.com
