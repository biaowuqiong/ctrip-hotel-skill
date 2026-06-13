# 🏨 ctrip-hotel-price

AI Skill for querying hotel prices on [Ctrip](https://www.ctrip.com) via Playwright MCP and real browser automation.

## What it does

- Opens Ctrip in your own browser (with your login state)
- Searches hotels by city name
- Filters by comfort level (3-star+) and twin rooms
- Extracts real-time prices

## Why not an API?

Ctrip has no public hotel price API. This skill uses browser automation to access the same data you'd see manually — but driven by AI.

## Requirements

- [Playwright MCP](https://github.com/executeautomation/mcp-playwright) installed
- Chrome or Edge browser
- A Ctrip account (free)

## Quick Start

```bash
# 1. Start browser with debug port
chrome --remote-debugging-port=9222 https://www.ctrip.com

# 2. Log into Ctrip manually

# 3. Ask your AI agent to run the skill
```

See [SKILL.md](./SKILL.md) for the full workflow.

## License

MIT
