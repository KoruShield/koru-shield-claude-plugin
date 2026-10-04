# Koru Shield Plugin for Claude Code

Manage Koru Shield DNS filtering and parental controls from Claude Code.

## Install

In Claude Code, add the marketplace and install the plugin:

```text
/plugin marketplace add KoruShield/koru-shield-claude-plugin
/plugin install koru-shield@koru-shield-marketplace
```

## Configure authentication

Create an API key in the dashboard at [my.korushield.com](https://my.korushield.com) under **API Keys**. Configure the Koru Shield MCP server with the key using your MCP client's secure environment configuration. For the local server, set `KORU_SHIELD_API_KEY` and run `npx -y @korushield/mcp-server`. The hosted MCP endpoint is `https://mcp.korushield.com/mcp` and uses a Bearer token. Never commit your API key or paste it into shared source files.

The MCP server source and setup details are available at [github.com/KoruShield/koru-shield-mcp](https://github.com/KoruShield/koru-shield-mcp).

## Usage examples

Ask Claude Code to:

- "Block TikTok on my kids profile"
- "Show me what was blocked today"
- "Would youtube.com be blocked right now?"
- "Turn on adult content filtering"
- "Add a bedtime schedule 9pm to 7am on weekdays"

The bundled skill explains all available Koru Shield tools and their safe use.
