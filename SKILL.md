---
name: amazon-batch-scraper
description: 亚马逊商品批量采集技能。通过 agent-browser 浏览器自动化工具采集亚马逊商品完整信息，自动生成格式化的 Excel 报告。
read_when:
  - 用户需要采集亚马逊商品数据
  - 用户需要做市场调研或竞品分析
  - 用户需要做选品决策
  - 用户说"采集亚马逊"、"亚马逊商品"、"亚马逊选品"
metadata:
  openclaw:
    emoji: "🛒"
    os: ["darwin", "linux", "win32"]
    requires:
      bins: ["node", "npm"]
      apps: ["Google Chrome", "agent-browser"]
    install:
      - id: agent-browser
        kind: npm
        package: agent-browser
        label: 安装 agent-browser
      - id: exceljs
        kind: npm
        package: exceljs
        label: 安装 Excel 生成库
allowed-tools: Bash(agent-browser:*)
---

# 🛒 Amazon Batch Scraper - 亚马逊商品批量采集

**通过 agent-browser 浏览器自动化采集 + 格式化 Excel 报告**

---

## ⚠️ 重要说明

**采集方式:**
- ✅ **只能使用 agent-browser 工具**
- ✅ **必须通过页面元素定位（snapshot）**
- ✅ **必须按顺序点击商品采集**
- ❌ **不能使用任何脚本文件**
- ❌ **不能使用自定义 JavaScript**
- ❌ **不能直接访问 DOM**

---

## 🔄 工作流程（OpenClaw 自动执行）

```
1. OpenClaw 使用 agent-browser 打开亚马逊
   ↓
2. agent-browser snapshot 获取页面元素
   ↓
3. agent-browser 点击搜索框，输入关键词
   ↓
4. agent-browser 点击搜索按钮
   ↓
5. agent-browser snapshot 获取商品列表
   ↓
6. 对每个商品循环:
   6.1 agent-browser 点击商品
   6.2 agent-browser wait 等待加载
   6.3 agent-browser snapshot 获取元素
   6.4 agent-browser get text 提取数据
   6.5 agent-browser scroll 滚动到评论
   6.6 agent-browser snapshot 获取评论
   6.7 agent-browser 返回搜索结果
   ↓
7. 使用 exceljs 生成 Excel
   ↓
8. 保存文件并通知用户
```

---

## 🚀 使用方式

### 通过 OpenClaw 对话

```
你：我想采集亚马逊商品

OpenClaw: 请告诉我搜索关键词

你：无线耳机

OpenClaw: 请设置采集数量

你：20

OpenClaw: [自动使用 agent-browser 执行采集]

OpenClaw: 📊 采集完成！
```

---

## 📋 采集步骤（OpenClaw 自动执行）

### 步骤 1: 打开亚马逊

```
OpenClaw: 使用 agent-browser
agent-browser open "https://www.amazon.com"
```

### 步骤 2: 检查登录

```
agent-browser snapshot -i
# 检查是否有"Sign In"或"登录"元素
# 如果有，提示用户登录
```

### 步骤 3: 搜索商品

```
agent-browser open "https://www.amazon.com/s?k=无线耳机"
agent-browser wait --load networkidle
agent-browser snapshot -i
```

### 步骤 4: 获取商品列表

```
agent-browser eval "(function() {
  const items = document.querySelectorAll('[data-asin]');
  return Array.from(items).slice(0, 20).map(item => ({
    asin: item.getAttribute('data-asin'),
    url: 'https://www.amazon.com/dp/' + item.getAttribute('data-asin')
  }));
})()"
```

### 步骤 5: 逐个采集商品

```
对每个商品:
  1. agent-browser open "商品 URL"
  2. agent-browser wait --load networkidle
  3. agent-browser snapshot -i
  4. agent-browser get text "#productTitle"
  5. agent-browser get text ".a-price .a-offscreen"
  6. agent-browser get text ".a-icon-alt"
  7. agent-browser scroll down 800
  8. agent-browser snapshot -i
  9. 采集评论
  10. agent-browser open "搜索 URL"
```

### 步骤 6: 生成 Excel

```
使用 exceljs 生成 Excel 报告
```

---

## 📊 采集字段

### 必须采集的字段

| 字段 | 提取方式 |
|------|----------|
| ASIN | URL 提取 |
| 商品标题 | `#productTitle` |
| 品牌 | `#bylineInfo` |
| 价格 | `.a-price .a-offscreen` |
| 评分 | `.a-icon-alt` |
| 评论数 | `#acrCustomerReviewText` |
| 库存 | `#availability` |
| Prime | `#primeBadge` |
| 主图 | `#landingImage` |
| BSR | `#SalesRank` |

### 禁止使用的方式

- ❌ 不能使用任何脚本文件
- ❌ 不能使用自定义 JS 脚本
- ❌ 不能直接访问 DOM
- ❌ 不能硬编码 CSS 选择器（必须使用 snapshot）

---

## 📁 输出文件

- **Excel:** `~/.openclaw/workspace/amazon-data.xlsx`
- **JSON:** `~/.openclaw/workspace/amazon-products.json`
- **图片:** `~/.openclaw/workspace/amazon-images/`
- **报告:** `~/.openclaw/workspace/amazon-analysis.md`

---

## ⏱️ 预计时长

| 数量 | 时长 |
|------|------|
| 10 个 | 10-15 分钟 |
| 20 个 | 20-30 分钟 |
| 50 个 | 50-70 分钟 |

---

## ⚠️ 前提条件

1. ✅ agent-browser 已安装
2. ✅ Google Chrome 已安装
3. ✅ 亚马逊账户已登录

---

## 🔧 故障排除

### 提示"未找到元素"

**解决:**
1. 使用 `agent-browser snapshot -i` 重新获取页面元素
2. 检查元素 ID 是否变化
3. 使用多个选择器回退

### 采集速度慢

**解决:**
1. 减少采集数量
2. 减少等待时间

---

## 📚 完整文档

- [GETTING_STARTED.md](./GETTING_STARTED.md) - 新手指南
- [PRODUCT_FIELDS.md](./PRODUCT_FIELDS.md) - 采集字段
- [WORKFLOW.md](./WORKFLOW.md) - 完整流程

---

**版本:** 2.5.0 | **最后更新:** 2026-03-15
