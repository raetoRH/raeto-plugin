# Raeto plugin for Claude Code

Connects Claude Code to [Raeto](https://raeto.cc). Claude can then ask any of 400+ AI models, use paid tools, pay APIs with Raeto Pay and run agents with their own wallets and budgets, all paid from your Raeto credits.

## Install

```
claude plugin marketplace add raetoRH/raeto-plugin
claude plugin install raeto@raeto
claude
```

Then run `/mcp`, pick **raeto** and choose **Authenticate**. Sign in on raeto.cc with your wallet and pick a daily limit. Claude Code gets its own agent wallet under your account: it tops itself up from your balance and never spends more than the daily limit. You can pause it, change its limits or close it on raeto.cc with your other agents.

## What's included

- **MCP server** `https://api.raeto.cc/mcp` with these tools: `ask_model`, `list_models`, `get_balance`, `how_to_pay`, `pay`, `list_payments`, `create_agent`, `fund_agent`, `pause_agent`, `list_agents`, plus any paid tools Raeto adds.
- **Skill** `raeto`: tells Claude when to use these tools and how to stay within your limits.
- **Command** `/raeto:balance`: your credits, today's spending and how to add more.

## Without the plugin

```
claude mcp add --transport http raeto https://api.raeto.cc/mcp
```

Then run `/mcp` and choose Authenticate, as above. To use an API key instead of signing in, add `--header "Authorization: Bearer YOUR_RAETO_KEY"`. You can create a key at raeto.cc/developers.
