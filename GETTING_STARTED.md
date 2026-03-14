# 🎓 Amazon Batch Scraper - 新手完全指南

**适合人群:** 零基础新手小白  
**预计时间:** 15 分钟完成第一次采集

---

## 📋 第一步：检查前提条件

### 1. 检查 OpenClaw 版本

打开终端（Mac）或命令提示符（Windows），输入：

```bash
openclaw --version
```

**预期输出:**
```
OpenClaw 2026.x.x
```

**如果未安装:**
1. 访问 https://openclaw.ai
2. 下载并安装 OpenClaw
3. 重启终端

---

### 2. 检查 Google Chrome

打开终端，输入：

**Mac:**
```bash
ls -la /Applications/Google\ Chrome.app
```

**Windows:**
```cmd
where chrome
```

**预期输出:**
```
/Applications/Google Chrome.app  (Mac)
或
C:\Program Files\Google\Chrome\Application\chrome.exe  (Windows)
```

**如果未安装:**
1. 访问 https://www.google.com/chrome/
2. 下载并安装 Chrome
3. 重启终端

---

### 3. 检查 Node.js

打开终端，输入：

```bash
node --version
npm --version
```

**预期输出:**
```
v18.x.x 或更高
9.x.x 或更高
```

**如果未安装:**
1. 访问 https://nodejs.org/
2. 下载并安装 LTS 版本
3. 重启终端

---

### 4. 准备亚马逊账户

1. 打开 Chrome 浏览器
2. 访问 https://www.amazon.com
3. 登录你的亚马逊账户
4. **保持登录状态，不要关闭浏览器**

---

## 📦 第二步：安装技能

### 方式 1: 自动安装（推荐）

在 OpenClaw 对话框中输入：

```
安装亚马逊采集技能
```

OpenClaw 会自动安装并提示：

```
✅ amazon-batch-scraper 技能已安装
```

### 方式 2: 手动安装

1. 打开终端
2. 进入技能目录：
   ```bash
   cd ~/.openclaw/workspace/skills/
   ```
3. 检查技能是否存在：
   ```bash
   ls -la amazon-batch-scraper/
   ```
4. 安装依赖：
   ```bash
   cd amazon-batch-scraper
   npm install exceljs axios
   ```

---

## ✅ 第三步：验证安装

### 1. 检查技能列表

在 OpenClaw 中输入：

```
查看已安装的技能
```

**预期输出:**
```
已安装的技能:
- amazon-batch-scraper (v2.5.0)
...
```

### 2. 测试技能

在 OpenClaw 中输入：

```
amazon-batch-scraper 帮助
```

**预期输出:**
```
🛒 Amazon Batch Scraper - 亚马逊商品批量采集

使用方式:
openclaw skill run amazon-batch-scraper --keyword "关键词" --limit 20

参数:
--keyword     搜索关键词 (必填)
--limit       采集数量 (默认 20)
--marketplace 目标市场 (默认 US)
...
```

---

## 🚀 第四步：第一次采集

### 1. 告诉 OpenClaw 你想采集

在 OpenClaw 对话框中输入：

```
我想采集亚马逊商品
```

### 2. 回答 OpenClaw 的问题

**OpenClaw:** 请告诉我搜索关键词

**你输入:** 无线耳机

**OpenClaw:** 请设置采集数量（默认 20，最大 100）

**你输入:** 20

**OpenClaw:** 请确认目标市场

**你输入:** 美国

**OpenClaw:** 是否需要下载商品图片？

**你输入:** 是

---

### 3. 等待采集完成

OpenClaw 会显示进度：

```
🔍 正在搜索：无线耳机
📦 找到 20 个商品
📊 开始采集...

📈 进度：1/20 (5%)
📈 进度：5/20 (25%)
📈 进度：10/20 (50%)
📈 进度：15/20 (75%)
📈 进度：20/20 (100%)

✅ 采集完成！
```

**预计时间:** 20-30 分钟

---

### 4. 查看采集结果

OpenClaw 会告诉你：

```
📁 文件已保存:
- Excel 报告：~/.openclaw/workspace/amazon-data.xlsx
- JSON 数据：~/.openclaw/workspace/amazon-products.json
- 图片文件夹：~/.openclaw/workspace/amazon-images/
- 分析报告：~/.openclaw/workspace/amazon-analysis.md

📊 采集统计:
- 总商品数：20
- 平均价格：$25.99
- 平均评分：4.5⭐
- 总评论数：125,678
```

---

## 📊 第五步：查看 Excel 报告

### 1. 打开 Excel 文件

**Mac:**
```bash
open ~/.openclaw/workspace/amazon-data.xlsx
```

**Windows:**
```cmd
start %USERPROFILE%\.openclaw\workspace\amazon-data.xlsx
```

### 2. 查看工作表

Excel 包含 6 个工作表：

1. **商品详情** - 所有商品的完整信息
2. **品牌分析** - 品牌统计
3. **价格分析** - 价格区间分布
4. **评分分布** - 评分统计
5. **评论摘要** - 评论数据汇总
6. **图片集** - 所有商品图片

### 3. 理解数据格式

**商品详情工作表:**

| 列 | 内容 | 说明 |
|---|------|------|
| A | 序号 | 1, 2, 3... |
| B | ASIN | 商品唯一标识 |
| C | 商品标题 | 完整标题 |
| D | 品牌 | 品牌名称 |
| E | 价格 | 当前售价 |
| F | 原价 | List Price |
| G | 折扣 | 折扣百分比 |
| H | 评分 | 1-5 星 |
| I | 评论数 | 总评论数 |
| J | 库存 | 有货/缺货 |
| K | Prime | ✅/❌ |
| L | BSR 排名 | 销售排名 |
| M | 主图 | 商品图片 |
| ... | ... | ... |

---

## 📈 第六步：查看分析报告

### 1. 打开分析报告

**Mac:**
```bash
open ~/.openclaw/workspace/amazon-analysis.md
```

**Windows:**
用文本编辑器打开：
```cmd
notepad %USERPROFILE%\.openclaw\workspace\amazon-analysis.md
```

### 2. 理解分析内容

报告包含：

1. **市场概况** - 价格、评分、评论数分布
2. **竞争分析** - 品牌集中度、价格竞争
3. **选品建议** - 推荐价格区间、功能
4. **机会分析** - 市场空白点
5. **图片分析** - 图片质量分析

---

## ❓ 常见问题

### Q1: 提示"未登录亚马逊"

**原因:** 亚马逊账户未登录

**解决:**
1. 打开 Chrome 浏览器
2. 访问 https://www.amazon.com
3. 点击右上角"Sign In"
4. 登录账户
5. 回到 OpenClaw，输入"已登录"

---

### Q2: Chrome 无法启动

**原因:** Chrome 未安装或路径错误

**解决:**
1. 检查 Chrome 是否安装
2. 重新安装 Chrome
3. 重启终端

---

### Q3: 采集速度慢

**原因:** 网络慢或商品页面加载慢

**解决:**
1. 检查网络连接
2. 减少采集数量（如 10 个）
3. 使用快速模式（不下载图片）

---

### Q4: Excel 打不开

**原因:** 没有安装 Excel

**解决:**
1. 安装 Microsoft Excel
2. 或使用 WPS Office
3. 或使用 Google Sheets 在线打开

---

### Q5: 图片没有下载

**原因:** 网络问题或磁盘空间不足

**解决:**
1. 检查网络连接
2. 检查磁盘空间
3. 重新采集

---

## 🎯 进阶使用

### 采集更多商品

```
采集 50 个无线耳机商品
```

### 指定价格区间

```
采集$20-50 的无线耳机
```

### 指定评分

```
采集 4.5 星以上的无线耳机
```

### 指定市场

```
采集英国站的无线耳机
```

---

## 📚 完整文档

- [SKILL.md](./SKILL.md) - 技能主文档
- [PRODUCT_FIELDS.md](./PRODUCT_FIELDS.md) - 采集字段清单
- [EXCEL_FORMAT.md](./EXCEL_FORMAT.md) - Excel 格式规范

---

## 🆘 需要帮助？

1. 查看 [SKILL.md](./SKILL.md) 故障排除章节
2. 访问 GitHub: https://github.com/957662/amazon-batch-scraper
3. 提交 Issue

---

**祝你采集愉快！** 🦞

**版本:** 2.5.0 | **最后更新:** 2026-03-15
