# Marginrule pricing agent

Price, fee, discount and plan math for Etsy, Shopify Basic, Payhip, Gumroad and Ko-fi. US sellers.

This is a public placeholder repository for the official MCP Registry and the GitHub MCP Registry. The server source code is not published here.

- Official registry name: `com.marginrule/pricing`
- Endpoint: `https://mcp.marginrule.com/mcp`
- Transport: streamable HTTP
- Authentication: none. The tools are free to use and need no account.
- Website: https://marginrule.com/agent/
- Contact: help@marginrule.com

## What it does

The server works out fees and prices from dated, sourced fee rows. You can ask what to charge to keep a target profit margin after a platform's fees, what a platform takes from one sale and what you keep, what a discount does to fees and profit, or which selling plan keeps the most at a price and monthly sales volume.

Every rate and margin the tools accept is a fraction (`0.30` means 30%). Money is USD. Every answer carries the date each fee was checked, its source URL, and the assumptions behind it. Check the platform's own fee page before you rely on a rate. These are calculators, not tax or accounting advice. Marginrule is not affiliated with any platform named here.

Fees shown are for US-based sellers selling to US buyers with domestic cards.

## Tools

- `price_for_margin`: lowest whole-cent price that keeps a target profit margin after a platform's fees
- `fees_breakdown`: fees a platform takes from one sale at a given price, and what the seller keeps
- `discount_impact`: effect of a discount on fees and profit
- `compare_plans`: which selling plan keeps the most at a price and monthly sales volume
- `list_platforms`: platforms and fee presets this server knows
- `data_version`: fee data version, dates and source URLs

All six tools are read-only. They do not place listings, change prices, or sign in to a selling platform.

## Supported platforms

Per-sale pricing covers Etsy, Shopify Basic, Payhip Free, Plus and Pro, Gumroad direct and Discover, Ko-fi Shop, Notion Marketplace, and Square online or in person.

Plan comparisons (`compare_plans`) cover Payhip Free, Plus and Pro, Gumroad direct and Discover, Ko-fi Shop and Ko-fi Gold, and Shopify Basic billed monthly or yearly. Ko-fi Gold is a plan option, so it appears in `compare_plans` rather than as its own per-sale platform in `list_platforms`. Etsy, Notion Marketplace and Square have no plan choice in the fee data; use `fees_breakdown` for those.

The server does not cover sellers outside the US, Amazon FBA, competitor repricing, or VAT.

## How to configure it

No API key, token or sign-in is required. Use the endpoint `https://mcp.marginrule.com/mcp`.

### VS Code and GitHub Copilot

With Copilot selected, open the Command Palette, run the Open Customizations command for Chat, then select MCP Servers and Add Server. Choose HTTP, paste `https://mcp.marginrule.com/mcp`, and give it an ID such as `marginrule`. To use it in all your workspaces, select Global, then Copilot Global. Review the trust prompt before you accept it.

You can also add it by hand. For Copilot across workspaces, put this in `~/.copilot/mcp-config.json` (or `$COPILOT_HOME/mcp-config.json` if that variable is set). For one workspace, put the same object in `.mcp.json` at the workspace root:

```json
{
  "mcpServers": {
    "marginrule": {
      "type": "http",
      "url": "https://mcp.marginrule.com/mcp"
    }
  }
}
```

No `headers` field is needed. The tools are free and need no account.

### Claude (web, desktop or mobile)

In Claude, go to Customize, then Connectors. Click + Add, then Add custom connector. Give it a name such as Marginrule, paste `https://mcp.marginrule.com/mcp`, and click Continue. Review the authentication settings Claude detected and click Continue. Under Authentication, choose No sign in, then click Add. To use it in a chat, click the + button, choose Connectors and turn it on.

Claude's Free plan allows one custom connector. On Team and Enterprise plans an owner adds it first, in Organization settings under Connectors.

Do not put this URL in `claude_desktop_config.json`. That file is for local stdio servers. Remote servers are added as custom connectors, as above.

### Cursor, Claude Code, and other apps

Any app that can add a remote MCP server over streamable HTTP can use the same address.

Cursor: add this to `~/.cursor/mcp.json` to use it in every project, or to `.cursor/mcp.json` in one project:

```json
{
  "mcpServers": {
    "marginrule": {
      "url": "https://mcp.marginrule.com/mcp"
    }
  }
}
```

Claude Code, in a terminal:

```bash
claude mcp add --transport http marginrule https://mcp.marginrule.com/mcp
```

## Example prompts

- I sell a digital download on Etsy that costs me $6 to make. What should I charge to keep a 30% margin?
- What do I keep from a $25 sale on Payhip Free?
- If I take 20% off a $30 Gumroad listing, what happens to my fees and profit?
- At $17 and 80 sales a month, which Payhip plan keeps the most?

## Privacy

The tool server at mcp.marginrule.com works out fees and prices from the numbers an assistant sends, such as a price, a cost, monthly sales, a target margin and a platform. It answers and keeps none of those numbers. We don't log or store them, and we don't link them to you.

To see whether the tools are used, we keep one count per tool for each day. That count holds nothing else, so no IP address, no numbers or words from the request, and no details of the assistant or device. An answer can include one link to a matching calculator on marginrule.com. The link carries a tag naming the tool that gave it. The tag says nothing about you.

Cloudflare runs the server and processes basic technical data such as your IP address to deliver answers and protect it from attacks, under its own privacy policy. The assistant you use has its own privacy terms for what you tell it.

The full notice is at https://marginrule.com/privacy/.

## Source code and licence

This repository is a placeholder so the official MCP Registry entry can point at a public GitHub URL. It does not contain the server source code. We have not published a separate open-source licence for the server code.

## Contact

Questions about the server: help@marginrule.com
