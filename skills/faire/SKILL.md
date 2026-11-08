---
name: faire-cotlet
description: Connect Faire to Claude Code, ChatGPT and any AI agent through Cotlet.dev, so the agent can list orders and update inventory in your own signed-in Faire account.
---

# Faire through Cotlet.dev

## What it does

Cotlet.dev runs your own Chrome in the cloud. The agent works in Faire (www.faire.com) there, signed in as you.

## Setup

1. Get an API key at https://cotlet.dev/app.
2. Add the MCP server `https://cotlet.dev/mcp/v1` with header `Authorization: Bearer <your key>`.

## Working rules

- First call `cotlet_app_guide` with app "faire".
- Then use `cotlet_browser_open`, `cotlet_browser_read` and `cotlet_browser_click`, one call at a time. Wait for each answer.
- At a sign-in page or CAPTCHA, stop and give the user the browser link.
- Ask the user before sending, publishing, deleting or paying.
- Close the browser with `cotlet_browser_close` when done.

More: https://cotlet.dev/integrations/faire-api-mcp-server?utm_source=clawhub&utm_medium=skill&utm_campaign=faire
