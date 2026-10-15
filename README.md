# Uzum seller plugins for Claude

Ask Claude about your Uzum Market shop — stock, sales, profit after commission, FBS orders, returns, invoices and expenses — in Uzbek, Russian or English.

Requires an account at **https://BRAND.uz** (free trial) with your Uzum API token connected.

## Claude Code

```
/plugin marketplace add BRAND-dev/uzum-seller-plugins
/plugin install uzum-seller@uzum-seller-plugins
```

Then run `/mcp`, pick `uzum-seller` and log in with your BRAND account.

## claude.ai / Claude Desktop

Settings → Connectors → Add custom connector → URL `https://BRAND.uz/mcp`.

## Privacy

The plugin holds no secrets. Your Uzum token is stored encrypted on BRAND's server, used read-only, and can be disconnected at any time. Not affiliated with Uzum.
