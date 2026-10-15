# Uzum Seller Agent — Claude plugin, ChatGPT and Codex connector

Ask Claude, ChatGPT or Codex about your Uzum Market shop — stock, sales, profit after commission, FBS orders, returns, invoices and expenses — in Uzbek, Russian or English.

Requires an account at **https://marketagent.uz** (free trial) with your Uzum API token connected.

## Claude Code

```
/plugin marketplace add dilshodbekuz/uzum-seller-agent
/plugin install uzum-seller@uzum-seller-agent
```

Then run `/mcp`, pick `uzum-seller` and log in with your Uzum Seller Agent account.

## claude.ai / Claude Desktop

Settings → Connectors → Add custom connector → URL `https://marketagent.uz/mcp`.

## ChatGPT

Paid plan (Plus, Pro or Business). Settings → Apps & Connectors → Advanced settings → turn on **Developer mode**.
Then Apps & Connectors → **Create**: MCP server URL `https://marketagent.uz/mcp`, authentication **OAuth**.
In a chat, press **+ → Developer mode** and enable the connector.

## Codex

```
codex mcp add uzum-seller --url https://marketagent.uz/mcp
codex mcp login uzum-seller
```

## Privacy

The plugin holds no secrets. Your Uzum token is stored encrypted on the Uzum Seller Agent server, used read-only, and can be disconnected at any time. Not affiliated with Uzum.
