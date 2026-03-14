# 🔄 Amazon Batch Scraper - 完整工作流程

**版本:** v2.5 | **日期:** 2026-03-15

---

## 📋 目录

1. [技能安装流程](#1-技能安装流程)
2. [技能触发流程](#2-技能触发流程)
3. [数据采集流程](#3-数据采集流程)
4. [数据处理流程](#4-数据处理流程)
5. [报告生成流程](#5-报告生成流程)
6. [用户交互流程](#6-用户交互流程)

---

## 1. 技能安装流程

### 1.1 安装方式

**方式 1: 自动安装（通过 ClawHub）**

```
用户：安装亚马逊采集技能

OpenClaw: 
  1. 调用 clawhub 技能
  2. 搜索 amazon-batch-scraper
  3. 下载到 ~/.openclaw/workspace/skills/amazon-batch-scraper/
  4. 安装依赖 (npm install exceljs axios)
  5. 验证安装
  6. 提示安装完成
```

**方式 2: 手动安装**

```bash
# 1. 复制技能文件夹
cp -r /path/to/amazon-batch-scraper \
      ~/.openclaw/workspace/skills/

# 2. 进入技能目录
cd ~/.openclaw/workspace/skills/amazon-batch-scraper

# 3. 安装依赖
npm install exceljs axios

# 4. 验证安装
openclaw skills list
```

### 1.2 安装后验证

```
OpenClaw 自动:
  1. 扫描技能目录
  2. 读取 SKILL.md
  3. 解析 front matter 元数据
  4. 读取 _meta.json
  5. 检查依赖是否安装
  6. 更新技能列表
  7. 标记为 ✓ ready
```

---

## 2. 技能触发流程

### 2.1 触发条件

**OpenClaw 读取 SKILL.md 中的 `read_when` 字段:**

```yaml
read_when:
  - 用户需要采集亚马逊商品数据
  - 用户需要做市场调研或竞品分析
  - 用户需要做选品决策
  - 用户说"采集亚马逊"、"亚马逊商品"等关键词
```

### 2.2 触发流程

```
用户输入: "我想采集亚马逊商品"
  ↓
OpenClaw:
  1. 分析用户意图
  2. 匹配技能的 read_when 条件
  3. 找到 amazon-batch-scraper 技能
  4. 加载技能上下文
  5. 准备执行采集流程
  ↓
OpenClaw 回复: "请告诉我搜索关键词"
```

### 2.3 关键词匹配

| 用户输入 | 匹配结果 |
|----------|----------|
| "我想采集亚马逊商品" | ✅ 匹配 |
| "亚马逊选品" | ✅ 匹配 |
| "帮我采集商品数据" | ✅ 匹配 |
| "市场调研" | ✅ 匹配 |
| "天气怎么样" | ❌ 不匹配 |

---

## 3. 数据采集流程

### 3.1 准备阶段

```
OpenClaw:
  1. 确认采集需求
     - 搜索关键词
     - 采集数量
     - 目标市场
     - 是否下载图片
  ↓
  2. 检查前提条件
     - Chrome 是否安装
     - 亚马逊是否登录
     - 依赖是否安装
  ↓
  3. 启动浏览器
     - 打开 Chrome
     - 配置 CDP 端口
     - 设置用户数据目录
```

### 3.2 搜索阶段

```
OpenClaw (使用 agent-browser):
  1. 打开亚马逊首页
     agent-browser open "https://www.amazon.com"
  ↓
  2. 输入搜索关键词
     agent-browser fill "搜索框" "无线耳机"
  ↓
  3. 提交搜索
     agent-browser click "搜索按钮"
  ↓
  4. 等待页面加载
     agent-browser wait --load networkidle
  ↓
  5. 获取商品列表
     agent-browser eval "提取商品 ASIN 列表"
  ↓
  6. 保存商品列表
     保存到：amazon-product-list.json
```

### 3.3 逐个采集阶段

```
对每个商品 (循环):
  
  3.3.1 打开商品页面
    agent-browser open "https://www.amazon.com/dp/B0XXX"
    ↓
  3.3.2 等待页面加载
    agent-browser wait --load networkidle
    sleep 3
    ↓
  3.3.3 采集基本信息
    agent-browser eval "采集 ASIN、标题、品牌、价格等"
    ↓
  3.3.4 采集图片
    agent-browser eval "提取主图和附图 URLs"
    下载图片到：amazon-images/
    ↓
  3.3.5 采集商品详情
    agent-browser eval "采集描述、特性要点、规格参数"
    ↓
  3.3.6 采集销售排名
    agent-browser eval "提取 BSR 排名和分类"
    ↓
  3.3.7 滚动到评论区
    agent-browser scroll down 800
    sleep 2
    ↓
  3.3.8 采集评论数据
    agent-browser eval "提取最多 50 条评论"
    ↓
  3.3.9 保存商品数据
    追加到：amazon-products.json
    ↓
  3.3.10 返回搜索结果
    agent-browser open "搜索页面 URL"
    sleep 2
    ↓
  3.3.11 继续下一个商品
```

### 3.4 采集字段详情

**每个商品采集以下数据:**

```json
{
  "basic": {
    "asin": "B0XXX",
    "title": "商品标题",
    "brand": "品牌",
    "price": "$15.99",
    "listPrice": "$35.99",
    "discount": "56%",
    "rating": 4.5,
    "reviewCount": 8421,
    "ratingDistribution": {...},
    "availability": "In Stock",
    "isPrime": true,
    "deliveryDate": "2026-03-20"
  },
  "seller": {
    "soldBy": "卖家名称",
    "shipsFrom": "发货地点",
    "isFBA": true,
    "sellerRating": 4.8
  },
  "details": {
    "description": "商品描述",
    "bulletPoints": ["要点 1", "要点 2", ...],
    "specifications": {...}
  },
  "ranking": {
    "bsr": 306,
    "category": "Beauty & Personal Care",
    "subcategories": [...]
  },
  "media": {
    "mainImage": "https://...",
    "images": ["https://...", ...],
    "videos": ["https://...", ...],
    "localImages": ["amazon-images/B0XXX_1.jpg", ...]
  },
  "reviews": {
    "total": 8421,
    "distribution": {...},
    "topPositive": {...},
    "topCritical": {...},
    "list": [...]
  }
}
```

---

## 4. 数据处理流程

### 4.1 数据清洗

```
OpenClaw:
  1. 验证数据完整性
     - 检查必填字段
     - 填补缺失值
     - 格式化数据
  ↓
  2. 数据标准化
     - 价格转换为数字
     - 日期格式化
     - 评分标准化
  ↓
  3. 数据验证
     - 价格范围检查
     - 评分范围检查 (0-5)
     - ASIN 格式验证
```

### 4.2 图片处理

```
OpenClaw:
  1. 下载主图
     axios.get(imageUrl) → amazon-images/B0XXX_main.jpg
  ↓
  2. 下载附图
     循环下载所有附图 → amazon-images/B0XXX_1.jpg, 2.jpg...
  ↓
  3. 图片重命名
     格式：ASIN_序号.jpg
  ↓
  4. 生成图片索引
     保存到：amazon-images/index.json
```

### 4.3 数据保存

```
保存位置:
  - JSON: ~/.openclaw/workspace/amazon-products.json
  - 图片：~/.openclaw/workspace/amazon-images/
  - 临时：~/.openclaw/workspace/amazon-product-list.json
```

---

## 5. 报告生成流程

### 5.1 Excel 报告生成

```
OpenClaw (使用 exceljs):
  
  5.1.1 创建工作簿
    const workbook = new ExcelJS.Workbook();
  ↓
  5.1.2 创建工作表 1: 商品详情
    - 设置表头样式
    - 设置列宽
    - 填充数据
    - 设置条件格式
    - 嵌入图片
  ↓
  5.1.3 创建工作表 2: 品牌分析
    - 统计品牌数据
    - 计算平均值
    - 生成数据条
  ↓
  5.1.4 创建工作表 3: 价格分析
    - 价格区间分组
    - 计算占比
    - 生成图表
  ↓
  5.1.5 创建工作表 4: 评分分布
    - 评分区间分组
    - 统计分析
    - 生成图表
  ↓
  5.1.6 创建工作表 5: 评论摘要
    - 汇总评论数据
    - 计算评分分布
    - 提取热门评论
  ↓
  5.1.7 创建工作表 6: 图片集
    - 嵌入所有主图
    - 每行 5 张
    - 标注 ASIN
  ↓
  5.1.8 保存文件
    workbook.xlsx.writeFile('amazon-data.xlsx')
```

### 5.2 分析报告生成

```
OpenClaw:
  
  5.2.1 市场概况分析
    - 计算平均价格
    - 计算平均评分
    - 统计评论数
    - 分析价格分布
  ↓
  5.2.2 竞争分析
    - 品牌集中度
    - 价格竞争程度
    - 进入壁垒评估
  ↓
  5.2.3 选品建议
    - 推荐价格区间
    - 必备功能分析
    - 差异化机会
  ↓
  5.2.4 机会分析
    - 价格空白点
    - 功能空白点
    - 评论痛点分析
  ↓
  5.2.5 图片分析
    - 主图质量评估
    - 图片数量统计
    - 改进建议
  ↓
  5.2.6 保存报告
    保存到：amazon-analysis.md
```

---

## 6. 用户交互流程

### 6.1 完整对话流程

```
用户：我想采集亚马逊商品
  ↓
OpenClaw: 请告诉我搜索关键词
  ↓
用户：无线耳机
  ↓
OpenClaw: 请设置采集数量（默认 20，最大 100）
  ↓
用户：20
  ↓
OpenClaw: 请确认目标市场
  1️⃣ 美国 (amazon.com)
  2️⃣ 英国 (amazon.co.uk)
  3️⃣ 德国 (amazon.de)
  4️⃣ 日本 (amazon.co.jp)
  ↓
用户：1
  ↓
OpenClaw: 是否需要下载商品图片？
  ↓
用户：是
  ↓
OpenClaw: ✅ 开始采集...
  ↓
[采集进行中，每 5 个商品汇报一次进度]
  📈 进度：5/20 (25%)
  📈 进度：10/20 (50%)
  📈 进度：15/20 (75%)
  📈 进度：20/20 (100%)
  ↓
OpenClaw: ✅ 采集完成！
  
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
  
  📈 关键发现:
  - 价格区间：$8.99 - $59.99
  - 品牌数量：12 个
  - 市场集中度：中等
  
  💡 建议:
  - 推荐价格区间：$15-25
  - 必备功能：长续航、降噪
  - 注意：评论数少于 1000 难以竞争
```

### 6.2 进度汇报机制

```
采集进度:
  - 每采集 5 个商品汇报一次
  - 显示百分比
  - 显示已用时间
  - 预计剩余时间
  
异常处理:
  - 商品页面无法访问 → 跳过并记录
  - 图片下载失败 → 继续采集其他数据
  - 网络超时 → 重试 3 次后跳过
```

### 6.3 完成通知

```
OpenClaw 发送完成通知:
  1. 显示文件保存位置
  2. 显示采集统计
  3. 显示关键发现
  4. 提供简要建议
  5. 询问是否需要进一步分析
```

---

## 📊 流程图总结

```
┌─────────────────┐
│   用户安装技能   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  OpenClaw 扫描   │
│   并加载技能     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   用户触发技能   │
│  (对话关键词)    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  OpenClaw 确认   │
│   采集需求       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   检查前提条件   │
│  (Chrome/登录)   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   启动浏览器     │
│   (agent-browser)│
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   搜索关键词     │
│   获取商品列表   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   逐个采集商品   │
│   (循环执行)     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   保存采集数据   │
│   (JSON+ 图片)    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   生成 Excel     │
│   (6 个工作表)    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   生成分析报告   │
│   (5 个分析维度)  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   通知用户完成   │
│   显示文件位置   │
└─────────────────┘
```

---

## 🔧 技术栈

| 组件 | 用途 |
|------|------|
| **OpenClaw** | 技能框架、对话管理 |
| **agent-browser** | 浏览器自动化 |
| **exceljs** | Excel 生成 |
| **axios** | 图片下载 |
| **Node.js** | 运行环境 |
| **Google Chrome** | 浏览器 |

---

**版本:** v2.5 | **最后更新:** 2026-03-15
