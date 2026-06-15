# 🏨 ctrip-hotel-price · 携程酒店查价

> AI Skill：通过 Playwright MCP 操控真实浏览器，在携程搜索酒店并提取双床房价格。
>
> 🔌 支持**无感模式**（窗口移至屏幕外，不遮挡工作区）和**普通模式**（窗口可见，适合录屏）。

AI Skill for querying hotel prices on Ctrip via Playwright MCP and real browser automation, with optional headless-like invisible mode.

---

## 它能做什么 / What it does

- 🔍 在携程按城市搜索酒店 / Search hotels by city on Ctrip
- ⭐ 筛选舒适及以上档次（3~5钻） / Filter by comfort+ (3-5 star)
- 🛏️ 只看双床房 / Twin room only
- 💰 提取实时价格 / Extract real-time prices
- 👻 无感操控，不遮挡屏幕 / Invisible mode: window off-screen

## 为什么不用 API / Why not an API

携程没有对个人开放的酒店价格 API。本 Skill 通过浏览器自动化，让 AI 像人一样操作携程网站。

Ctrip has no public hotel price API. This skill uses browser automation to access the same data you'd see manually — but driven by AI.

## 依赖 / Requirements

- [Playwright MCP](https://github.com/executeautomation/mcp-playwright)
- Chrome 或 Edge / Chrome or Edge
- 携程账户（免费）/ Ctrip account (free)

## 快速开始 / Quick Start

```bash
# 无感模式（推荐日常用）/ Invisible mode (recommended)
powershell -Command "taskkill /f /im msedge.exe"; sleep 2
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--window-position=-32000,-32000','https://www.ctrip.com'"
```

```bash
# 普通模式（录屏/调试用）/ Normal mode (for recording)
powershell -Command "taskkill /f /im msedge.exe"; sleep 2
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','https://www.ctrip.com'"
```

完整流程见 [SKILL.md](./SKILL.md)。

## 演示 / Demo

[演示视频] · AI 全程操控携程：搜索 → 筛选档次 → 筛选双床房 → 提取实时价格，无需手动操作。

## 许可 / License

MIT
