# How to connect Faire to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your Faire account.** Faire's own ChatGPT app is for discovering wholesale products, not for managing your orders. Cotlet.dev connects your own signed-in Faire account to any AI agent, so you can ask in plain words and the AI lists your orders and updates your inventory for you.

## What you can ask

> List all new Faire orders from this week that I haven't accepted yet, with the retailer name and order total.

> Set inventory for the Lavender Soy Candle 8 oz to 120 units and mark the 4 oz size as out of stock.

> Which orders have to ship by Friday? Sort them by ship date and show the item count for each.

> Show me every order from The Corner Shop in Portland since January 1 and their total spend.

> Lower stock on the Linen Tote in Natural to 15 and tell me which open orders include it.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Faire tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"faire":{"command":"uvx","args":["faire-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t faire-mcp .
docker run -i --rm -e COTLET_API_KEY faire-mcp
```

Tools: `faire_guide`, `faire_status`, `faire_open`, `faire_read`, `faire_click`, `faire_type`, `faire_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install faire-mcp        # or run it once: uvx faire-mcp connect
faire-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 faire_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 faire_agent.py status    # is Faire ready in your Cotlet.dev account
python3 faire_agent.py guide     # Faire screens and sign-in link
python3 faire_agent.py read      # open Faire, read the page, close the browser
python3 faire_agent.py tools     # list Cotlet.dev tools
python3 faire_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Faire users

**Does Faire have an API?**

Yes, but only part of it: Faire has an External API for brands that covers products, orders and inventory, and a single brand can generate its own access token in the brand portal (checked 11 Oct 2026). We found no API for Messages, Campaigns, your Faire Direct link or your customer list. Cotlet.dev works in your own signed-in Faire account, so your AI agent can list orders and update inventory with no API key and no code.

**How do I connect Faire to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to Faire once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. The Faire Wholesale app in ChatGPT is for product discovery. Cotlet.dev works with your orders and inventory.

**Is there a way to use Claude with Faire?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own Faire account.

**Is there a Faire MCP server?**

Cotlet.dev is a hosted MCP server that works in Faire for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [Faire on Cotlet.dev](https://cotlet.dev/integrations/faire-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=faire&utm_content=find)
- [PyPI package faire-mcp](https://pypi.org/project/faire-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-faire-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/faire-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=faire

Start free: https://cotlet.dev/signup?app=faire&utm_source=github&utm_medium=readme&utm_campaign=faire
