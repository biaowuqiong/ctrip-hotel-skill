# 🏨 ctrip-hotel-price · 携程酒店查价

> AI Skill：通过 Playwright MCP 操控真实浏览器，在携程搜索酒店并提取双床房价格。
>
> 🔌 支持**无感模式**（窗口移至屏幕外，不遮挡工作区）和**普通模式**（窗口可见，适合录屏）。

AI Skill for querying hotel prices on Ctrip via Playwright MCP and real browser automation, with invisible mode.

---

## 它能做什么 / What it does

- 🔍 在携程按城市搜索酒店 / Search hotels by city on Ctrip
- ⭐ 筛选舒适及以上档次（3~5钻） / Filter by comfort+ (3-5 star)
- 🛏️ 只看双床房 / Twin room only
- 💰 提取实时价格 / Extract real-time prices
- 👻 无感操控，不影响日常使用 / Invisible mode, doesn't interfere with daily browsing

## 为什么不用 API / Why not an API

携程没有对个人开放的酒店价格 API。本 Skill 通过浏览器自动化，让 AI 像人一样操作携程网站。

Ctrip has no public hotel price API. Use browser automation instead.

## 依赖 / Requirements

- [Playwright MCP](https://github.com/executeautomation/mcp-playwright)
- Chrome 或 Edge / Chrome or Edge
- 携程账户（免费，扫码登录一次即可）/ Ctrip account (free)

## 快速开始 / Quick Start

首次使用：普通模式登录一次。日常使用：无感模式。

```bash
# 无感模式（推荐）/ Invisible mode (recommended)
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','--window-position=-32000,-32000','https://www.ctrip.com'"
```

```bash
# 普通模式（首次登录/录屏）/ Normal mode (first login / recording)
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','https://www.ctrip.com'"
```

> 调试 Edge 使用独立配置目录 (`C:\temp\edge-debug`)，与你日常的 Edge 完全隔离。日常开新窗口不受任何影响。

## 演示 / Demo

[![自动化酒店查询Skill](https://img.shields.io/badge/bilibili-演示视频-00A1D6?logo=bilibili)](https://www.bilibili.com/video/BV1xCJc6hEAz/)

> AI 全程操控携程：搜索 → 筛选档次 → 筛选双床房 → 查看实时价格。

## 许可 / License

MIT
