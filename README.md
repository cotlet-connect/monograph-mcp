# Monograph API and MCP server for Claude and ChatGPT

**Yes, ChatGPT, Claude and other AI agents can work with your Monograph account.** Monograph has no open API or official MCP server. Cotlet.dev connects your own signed-in Monograph account to AI agents for project, staffing, budget, time and billing work, with confirmation before sensitive actions.

## What you can ask

> Review project budgets against contracts and flag variances.

> Show unbilled time by project and draft invoices for my approval.

> Find staffing gaps and propose assignments for next week.

> List overdue consultant bills and prepare follow-up notes.

> Summarize utilization and project profitability for this month.

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

This repo is a real MCP server. It speaks MCP over stdio, lists its Monograph tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"monograph":{"command":"uvx","args":["monograph-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t monograph-mcp .
docker run -i --rm -e COTLET_API_KEY monograph-mcp
```

Tools: `monograph_guide`, `monograph_status`, `monograph_open`, `monograph_read`, `monograph_click`, `monograph_type`, `monograph_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install monograph-mcp        # or run it once: uvx monograph-mcp connect
monograph-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 monograph_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 monograph_agent.py status    # is Monograph ready in your Cotlet.dev account
python3 monograph_agent.py guide     # Monograph screens and sign-in link
python3 monograph_agent.py read      # open Monograph, read the page, close the browser
python3 monograph_agent.py tools     # list Cotlet.dev tools
python3 monograph_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Monograph users

**Does Monograph have an API?**

Monograph does not offer an open API. QuickBooks Online and Stripe are built-in integrations, according to its account FAQ.

**How do I connect Monograph to ChatGPT?**

Sign up at https://cotlet.dev/signup?app=monograph, enable Monograph and sign in at app.monograph.com/login in your Cotlet.dev Cloud Browser. Add https://cotlet.dev/mcp/v1/connect to ChatGPT with OAuth.

**Can I use Monograph with Claude?**

Yes. Add https://cotlet.dev/mcp/v1/connect as a custom connector in Claude and sign in to Cotlet.dev.

**Is this an official Monograph MCP server?**

No. Cotlet.dev is independent and is not affiliated with Monograph. The hosted integration works in your own signed-in Monograph account.

## Find it on

- [Monograph on Cotlet.dev](https://cotlet.dev/integrations/monograph-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=monograph&utm_content=find)
- [PyPI package monograph-mcp](https://pypi.org/project/monograph-mcp/)
- [Odel](https://odel.app/modules/cotlet/monograph)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/monograph/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-monograph-to-ai-agents-guide)

## Also works with


- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/monograph-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=monograph

Start free: https://cotlet.dev/signup?app=monograph&utm_source=github&utm_medium=readme&utm_campaign=monograph
