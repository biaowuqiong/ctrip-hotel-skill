# 🏨 ctrip-hotel-price · 携程酒店查价

> AI Skill：通过 Playwright MCP 操控真实浏览器，在携程搜索任意地点周边酒店并提取双床房价格。
>
> 🔍 支持搜索**城市、景区、地标**等任意目的地 · ⭐ 舒适及以上档次（3~5钻全选） · 🛏️ 双床房精准筛选 · 📍 位置子区域百分比筛选 · 👻 无感模式

AI Skill for querying hotel prices on Ctrip via Playwright MCP with real browser automation. Search by city, scenic spot, or any location.

---

## 它能做什么 / What it does

- 🔍 按城市/景区/地标搜索酒店 / Search by city, scenic spot, or any POI
- ⭐ 同时筛选 3~5 钻（舒适/高档/豪华）/ Multi-select star ratings (3-5)
- 🛏️ 只看双床房 / Twin room filter
- 📍 位置子区域百分比分析（如「景区入口 15%」）/ Location sub-area percentage breakdown
- 💰 提取实时双床房价格 / Extract real-time twin room prices
- 👻 无感操控，不影响日常浏览器 / Invisible mode, zero interference

## 为什么不用 API / Why not an API

携程没有对个人开放的酒店价格 API。本 Skill 通过浏览器自动化，让 AI 像人一样操作携程网站，拿到完全相同的实时数据。

Ctrip has no public hotel price API. Use browser automation instead.

## 关键改进 / Key Features

| 特性 | 说明 |
|------|------|
| 任意目的地 | 「太白山」→ 自动解析为景区 District，不需手动选城市 |
| 1920×1080 窗口 | 确保携程筛选栏完整渲染，避免 `aria-hidden` 阻挡 |
| 位置百分比弹窗 | 点「位置 > 更多」查看各子区域酒店占比，精准锁定登山入口附近 |
| 独立配置目录 | `--user-data-dir=C:\temp\edge-debug`，与日常 Edge 完全隔离 |
| 星级多选 | 依次点击 3/4/5 钻，携程默认多选，覆盖全档次 |

## 依赖 / Requirements

- [Playwright MCP](https://github.com/executeautomation/mcp-playwright)
- Chrome 或 Edge / Chrome or Edge
- 携程账户（免费，扫码登录一次即可）/ Ctrip account (free)

## 快速开始 / Quick Start

```bash
# 无感模式（推荐）/ Invisible mode
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','--window-size=1920,1080','--window-position=-2000,0','https://www.ctrip.com'"
```

```bash
# 普通模式（首次登录/录屏）/ Normal mode
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','--window-size=1920,1080','https://www.ctrip.com'"
```

完整流程见 [SKILL.md](./SKILL.md)。

## 演示 / Demo

[![自动化酒店查询Skill](https://img.shields.io/badge/bilibili-演示视频-00A1D6?logo=bilibili)](https://www.bilibili.com/video/BV1xCJc6hEAz/)

> AI 全程操控携程：搜索 → 星级筛选 → 双床房筛选 → 位置百分比分析 → 查看实时价格。

## 许可 / License

MIT
