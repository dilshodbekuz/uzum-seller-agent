# Uzum seller plugins for Claude

Ask Claude about your Uzum Market shop — stock, sales, profit after commission, FBS orders, returns, invoices and expenses — in Uzbek, Russian or English.

Requires an account at **https://marketagent.uz** (free trial) with your Uzum API token connected.

## Claude Code

```
/plugin marketplace add GITHUB_USER/uzum-seller-plugins
/plugin install uzum-seller@uzum-seller-plugins
```

Then run `/mcp`, pick `uzum-seller` and log in with your Uzum Seller Agent account.

## claude.ai / Claude Desktop

Settings → Connectors → Add custom connector → URL `https://marketagent.uz/mcp`.

## Privacy

The plugin holds no secrets. Your Uzum token is stored encrypted on the Uzum Seller Agent server, used read-only, and can be disconnected at any time. Not affiliated with Uzum.
