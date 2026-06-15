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

提供两种模式，按需选择：

**普通模式**（窗口可见，适合录屏/调试）：
```bash
powershell -Command "taskkill /f /im msedge.exe"; sleep 2
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','https://www.ctrip.com'"
```

**无感模式**（窗口移到屏幕外，不遮挡工作区，推荐日常使用）：
```bash
powershell -Command "taskkill /f /im msedge.exe"; sleep 2
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--window-position=-32000,-32000','https://www.ctrip.com'"
```

> `--window-position=-32000,-32000` 将窗口移到屏幕外。浏览器正常运行，完全不受影响，只是你看不到 UI。如需登录或调试，切换回普通模式重启即可。登录态保留。

Chrome / macOS 同理，加上 `--window-position=-32000,-32000` 即可。

### 3. 确认端口就绪

```bash
curl http://127.0.0.1:9222/json/version
```

### 4. 登录携程

在浏览器中手动登录。

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
- 档次筛选多选：依次点击 3/4/5 钻
- 启动前完全关闭浏览器进程
