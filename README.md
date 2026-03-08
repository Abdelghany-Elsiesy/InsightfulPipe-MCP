# InsightfulPipe MCP Configuration

Connect [InsightfulPipe](https://main.insightfulmcp.com) to the Claude Code Desktop App using MCP (Model Context Protocol).

## Setup

1. Copy `.mcp.json` into the root of the folder you use for your Scheduled Task
2. When creating or editing a Scheduled Task in the **Claude Code Desktop App**, select that folder
3. Claude automatically detects `.mcp.json` when the task runs and connects to InsightfulPipe

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

## Requirements

- **macOS** (Linux also supported)
- [Node.js](https://nodejs.org/) installed (provides `npx`)

## What is InsightfulPipe?

A marketing analytics platform that gives Claude access to data from 30+ platforms including:

Google Ads, Facebook Ads, Google Analytics, Shopify, HubSpot, Instagram, LinkedIn, TikTok, Klaviyo, Mailchimp, Stripe, and more.

Once connected, you can ask Claude to pull reports, analyze performance, and audit campaigns directly from your workspace data.
