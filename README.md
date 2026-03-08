# InsightfulPipe MCP Configuration

Connect [InsightfulPipe](https://main.insightfulmcp.com) to the Claude Code Desktop App using MCP (Model Context Protocol).

## Setup

1. Copy `.mcp.json` into the root of the folder you use for your Scheduled Task
2. When creating or editing a Scheduled Task in the **Claude Code Desktop App**, select that folder
3. Claude automatically detects `.mcp.json` when the task runs and connects to InsightfulPipe

> **Important:** The file must be named `.mcp.json` (with the leading dot). A file named `mcp.json` will not be detected.

## `.mcp.json`

```json
{
  "mcpServers": {
    "insightfulpipe": {
      "command": "/bin/sh",
      "args": ["-l", "-c", "npx -y mcp-remote https://main.insightfulmcp.com"]
    }
  }
}
```

This uses `mcp-remote` to bridge the remote InsightfulPipe MCP server into Claude Code. The `/bin/sh -l` ensures your shell profile is loaded so `npx` is found regardless of how Node.js was installed.

## `.claude/settings.local.json`

This file pre-approves the InsightfulPipe MCP tools so Claude can use them without prompting for permission each time. Place it at `.claude/settings.local.json` in the same folder.

```json
{
  "permissions": {
    "allow": [
      "mcp__insightfulpipe__query_contexts",
      "mcp__insightfulpipe__query_data",
      "mcp__insightfulpipe__execute_action"
    ]
  },
  "enableAllProjectMcpServers": true,
  "enabledMcpjsonServers": [
    "insightfulpipe"
  ]
}
```

> This is especially important for Scheduled Tasks, which run without user interaction and cannot prompt for tool permissions.

## First-Time Authentication

Before using in a Scheduled Task, you must authenticate once by running this in your terminal or CMD:

```bash
npx -y mcp-remote https://main.insightfulmcp.com
```

A browser window will open for OAuth login. Complete the login, then press `Ctrl+C` to stop the server. Tokens are cached locally and future connections (including Scheduled Tasks) will authenticate automatically.

## Requirements

- **macOS** (Linux also supported)
- [Node.js](https://nodejs.org/) installed (provides `npx`)

## What is InsightfulPipe?

A marketing analytics platform that gives Claude access to data from 30+ platforms including:

Google Ads, Facebook Ads, Google Analytics, Shopify, HubSpot, Instagram, LinkedIn, TikTok, Klaviyo, Mailchimp, Stripe, and more.

Once connected, you can ask Claude to pull reports, analyze performance, and audit campaigns directly from your workspace data.
