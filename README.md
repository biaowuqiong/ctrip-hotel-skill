# 🏨 ctrip-hotel-price · 携程酒店查价

> AI Skill：通过 Playwright MCP 操控真实浏览器，在携程搜索酒店并提取双床房价格。

AI Skill for querying hotel prices on Ctrip via Playwright MCP and real browser automation.

---

## 它能做什么 / What it does

- 🔍 在携程按城市搜索酒店 / Search hotels by city on Ctrip
- ⭐ 筛选舒适及以上档次 / Filter by comfort level (3-star+)
- 🛏️ 只看双床房 / Twin room only
- 💰 提取实时价格 / Extract real-time prices

## 为什么不用 API / Why not an API

携程没有对个人开放的酒店价格 API。本 Skill 通过浏览器自动化，让 AI 像人一样操作携程网站，拿到完全相同的价格数据。

Ctrip has no public hotel price API. This skill uses browser automation to access the same data you'd see manually — but driven by AI.

## 依赖 / Requirements

- [Playwright MCP](https://github.com/executeautomation/mcp-playwright)
- Chrome 或 Edge 浏览器 / Chrome or Edge
- 携程账户（免费）/ A Ctrip account (free)

## 快速开始 / Quick Start

```bash
# 1. 以调试模式启动浏览器 / Start browser with debug port
chrome --remote-debugging-port=9222 https://www.ctrip.com

# 2. 手动登录携程 / Log into Ctrip manually

# 3. 让 AI 执行本 Skill / Ask your AI agent to run the skill
```

完整流程见 [SKILL.md](./SKILL.md) / Full workflow in [SKILL.md](./SKILL.md).

## 许可 / License

MIT
