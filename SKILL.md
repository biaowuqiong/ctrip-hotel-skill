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

**Edge（Windows）：**
```bash
powershell -Command "taskkill /f /im msedge.exe"; sleep 2
powershell -Command "Start-Process 'C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe' -ArgumentList '--remote-debugging-port=9222','https://www.ctrip.com'"
```

**Chrome（Windows）：**
```bash
powershell -Command "taskkill /f /im chrome.exe"; sleep 2
powershell -Command "Start-Process 'chrome' -ArgumentList '--remote-debugging-port=9222','https://www.ctrip.com'"
```

**Chrome（macOS）：**
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --remote-debugging-port=9222 https://www.ctrip.com
```

确认端口就绪：
```bash
curl http://127.0.0.1:9222/json/version
```

### 3. 登录携程

在打开的浏览器窗口中手动登录携程账户。

## 查价流程

### Step 1：导航

```
mcp__playwright__browser_navigate → https://www.ctrip.com/
```

### Step 2：搜索城市

```
mcp__playwright__browser_type → target="#hotels-destination" → text="目的地城市名"
mcp__playwright__browser_click → target="getByText('搜索', { exact: true })"
```

### Step 3：筛选

```
mcp__playwright__browser_click → target="text=3钻/星"       # 舒适及以上
mcp__playwright__browser_click → target="text=双床房"       # 只要双床
```

### Step 4：查看详情并提取价格

```
mcp__playwright__browser_click → target="text=酒店名称"     # 点进详情
mcp__playwright__browser_tabs → action="select", index=1    # 切到新标签
mcp__playwright__browser_evaluate → function="() => document.body.innerText.substring(0, 5000)"
```

## 注意事项

- `#hotels-destination` 是携程酒店搜索框的唯一 CSS ID
- `text=搜索` 需用 `{ exact: true }` 避免匹配其他含「搜索」的元素
- 浏览器启动前须完全关闭所有进程，否则调试端口参数不生效
- 使用正常用户数据目录才能复用已登录的携程账户
