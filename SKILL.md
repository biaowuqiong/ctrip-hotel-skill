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

调试 Edge 使用独立配置目录，与日常 Edge 互不干扰。**必须设置 1920×1080 窗口大小**，否则携程筛选面板可能折叠。

**无感模式**（日常使用，窗口移到屏幕左侧外）：

```bash
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','--window-size=1920,1080','--window-position=-2000,0','https://www.ctrip.com'"
```

> `--window-size=1920,1080` 确保携程筛选栏完整渲染，避免 `aria-hidden` 导致点击超时。
> `--window-position=-2000,0` 将窗口移到屏幕左侧外（适配 1920 宽度）。

**普通模式**（首次登录/录屏）：

```bash
powershell -Command "Stop-Process -Name msedge -Force -ErrorAction SilentlyContinue"
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','--user-data-dir=C:\temp\edge-debug','--disable-background-mode','--no-first-run','--window-size=1920,1080','https://www.ctrip.com'"
```

### 3. 确认端口就绪

```bash
curl http://127.0.0.1:9222/json/version
```

### 4. 玩法：目的地输入技巧

- 城市搜索：直接输入城市名（如「宝鸡」）
- 景区周边：直接输入景区名（如「太白山」），携程自动解析为对应 District
- 搜索后先 `browser_resize` 到 1920×1080 确保筛选栏可见

## 查价流程

### Step 1：导航 → 搜索

```
mcp__playwright__browser_resize → 1920×1080
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

### Step 3：查看详情

```
mcp__playwright__browser_click → target="text=酒店名称"
mcp__playwright__browser_tabs → action="select", index=1
mcp__playwright__browser_evaluate → function="() => document.body.innerText.substring(0, 5000)"
```

## 注意事项

- `#hotels-destination` 是携程酒店搜索框唯一 ID
- 端口启动前必须杀死所有 Edge 进程
- `--user-data-dir=C:\temp\edge-debug` 隔离调试/日常配置
- `--window-size=1920,1080` 必须设置，小窗口会导致筛选栏 `aria-hidden`
- `--disable-background-mode` 防止后台进程复活
