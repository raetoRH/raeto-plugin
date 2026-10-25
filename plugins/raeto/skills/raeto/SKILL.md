---
name: raeto
description: Use Raeto's MCP tools to ask other AI models (second opinions, cheaper or specialised models), pay APIs that answer HTTP 402 with a Raeto Pay price, run agents with their own Raeto wallets and budgets, and check or add Raeto credits.
---

# Raeto

Raeto gives you 400+ AI models, paid tools and payments, all paid from the user's Raeto credits. The tools come from the `raeto` MCP server. If they are missing or answer "Sign in to Raeto", ask the user to run `/mcp`, pick the Raeto server and choose **Authenticate**. They approve the connection on raeto.cc, and Claude Code gets its own agent wallet with a daily limit.

## When to use what

- **Second opinion or delegation**: `ask_model`. Use `model: "raeto/auto"` to let Raeto pick the cheapest model that can do the job, or call `list_models` to find a specific id (for example `openai/gpt-5`, `google/gemini-2.5-pro`). Good for checking a plan, a long summary job or a cheap bulk task.
- **Paid APIs**: when an HTTP API answers `402 Payment Required` with Raeto Pay details (`payTo`, `amountUsd`), call `pay` with those values. Then repeat the request with the header `X-Raeto-Receipt: <receipt>`. A receipt works once, for that payee only. If the API never serves the call, the money comes back.
- **Paid tools**: other tools on the Raeto server, such as search or scraping when they are available. Each one's description gives its price per call.
- **Agents**: `create_agent` makes an agent with its own wallet, API key and limits (`daily_usd`, `per_payment_usd`, `models`). The key is shown once, so hand it to the agent or store it as a secret, never in code or logs. `fund_agent` moves credits to an agent, `pause_agent` is the kill switch, and `list_agents` shows them all.
- **Money**: `get_balance` shows what is left and the daily limit. `how_to_pay` shows how to add credits (USDG, rCREDIT, or vault interest).

## Rules

- Every paid call says what it cost. Mention the cost when it is more than a few cents.
- Stay within the user's limits. If a call fails with a daily limit or "out of credits", tell the user and point them to `how_to_pay` or their agent settings on raeto.cc. Don't try to get around the limit.
- Ask before paying an API the user didn't mention, and before creating or funding agents with more than $5.
