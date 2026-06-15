---
name: ctrip-hotel-price
description: 通过 Playwright MCP 操控浏览器，在携程搜索酒店并提取双床房价格。
---

# 携程酒店查价

通过 Playwright MCP 操控浏览器，在携程搜索酒店并提取双床房价格。

## 前置条件

### 1. 安装 Playwright MCP

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp", "--cdp-endpoint", "http://127.0.0.1:9222"]
    }
  }
}
```

### 2. 启动浏览器调试模式

调试 Edge 使用**独立配置目录**（`C:\temp\edge-debug`），与日常 Edge 互不干扰。

**无感模式**（推荐日常使用，窗口在屏幕外）：

```bash
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','--window-position=-32000,-32000','https://www.ctrip.com'"
```

**普通模式**（窗口可见，适合录屏/调试/首次登录）：

```bash
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','https://www.ctrip.com'"
```

> **为什么用独立配置目录？** 如果共用默认配置，你日常打开的新 Edge 窗口会附加到调试实例，继承其窗口位置（屏幕外）。独立配置彻底隔离两个环境：调试窗口移出屏幕操控，日常窗口正常工作。
>
> **首次使用**：先用普通模式启动一次，在可见窗口中登录携程（扫码即可）。之后切换无感模式，登录态永久保留。

Chrome / macOS 同理，替换浏览器路径和参数即可。

### 3. 确认端口就绪

```bash
curl http://127.0.0.1:9222/json/version
```

## 查价流程

### Step 1：导航 → 搜索城市

```
mcp__playwright__browser_navigate → https://www.ctrip.com/
mcp__playwright__browser_type → target="#hotels-destination" → text="目的地"
mcp__playwright__browser_click → target="getByText('搜索', { exact: true })"
```

### Step 2：筛选（舒适及以上 + 双床房）

```
mcp__playwright__browser_click → target="text=3钻/星"
mcp__playwright__browser_click → target="text=4钻/星"
mcp__playwright__browser_click → target="text=5钻/星"
mcp__playwright__browser_click → target="getByRole('radio', { name: '双床房' })"
```

### Step 3：点进详情看价格

```
mcp__playwright__browser_click → target="text=酒店名称"
mcp__playwright__browser_tabs → action="select", index=1
mcp__playwright__browser_evaluate → function="() => document.body.innerText.substring(0, 5000)"
```

## 注意事项

- `#hotels-destination` 是携程酒店搜索框唯一 ID
- `{ exact: true }` 避免匹配多余元素
- 双床房筛选按钮用 `getByRole('radio', { name: '双床房' })`
- 档次需多选（3/4/5 钻依次点击）
- 启动前必须 `Stop-Process` 杀死所有 Edge 进程
- `--disable-background-mode` 防止后台进程复活
- 调试 Edge 重启后 MCP 需重连（`install_source` 重新安装一次即可）
