# 📋 Amazon 商品页面完整信息清单

**版本:** v2.3 | **日期:** 2026-03-15

---

## 🎯 亚马逊商品页面显示的所有信息

### 1. 商品基本信息 (Product Basic Info)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **ASIN** | ASIN | 商品详情表格 | ✅ 必填 |
| **商品标题** | Product Title | 页面顶部 H1 | ✅ 必填 |
| **品牌** | Brand | 标题下方/品牌链接 | ✅ 必填 |
| **当前价格** | Price | 价格区域 | ✅ 必填 |
| **原价/List Price** | List Price | 价格区域 | ✅ 推荐 |
| **折扣金额** | Savings | 价格区域 | ✅ 推荐 |
| **折扣百分比** | Discount % | 价格区域 | ✅ 推荐 |
| **评分** | Star Rating | 评分区域 | ✅ 必填 |
| **评论数** | Review Count | 评分区域 | ✅ 必填 |
| **评分分布** | Rating Distribution | 评论页面 | ✅ 推荐 |

---

### 2. 库存与配送 (Availability & Shipping)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **库存状态** | Availability | 购买框 | ✅ 必填 |
| **Prime 资格** | Prime Eligible | 购买框 | ✅ 必填 |
| **配送信息** | Shipping Info | 购买框 | ✅ 推荐 |
| **到货日期** | Delivery Date | 购买框 | ✅ 推荐 |
| **库存数量** | Quantity Available | 购买框 (部分商品) | ⚠️ 可选 |

---

### 3. 卖家信息 (Seller Info)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **卖家名称** | Sold by | 购买框 | ✅ 推荐 |
| **发货方** | Ships from | 购买框 | ✅ 推荐 |
| **卖家评分** | Seller Rating | 卖家页面 | ⚠️ 可选 |
| **是否自营** | Fulfilled by Amazon | 购买框 | ✅ 推荐 |

---

### 4. 商品详情 (Product Details)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **商品描述** | Product Description | 描述区域 | ✅ 推荐 |
| **特性要点** | Bullet Points / About this item | 要点区域 | ✅ 必填 |
| **规格参数** | Product Details | 详情表格 | ✅ 推荐 |
| **材质** | Material | 规格参数 | ⚠️ 可选 |
| **颜色** | Color | 规格参数 | ⚠️ 可选 |
| **尺寸** | Size | 规格参数 | ⚠️ 可选 |
| **重量** | Weight | 规格参数 | ⚠️ 可选 |
| **生产日期** | Date First Available | 详情表格 | ⚠️ 可选 |
| **制造商** | Manufacturer | 详情表格 | ⚠️ 可选 |
| **产品型号** | Model Number | 详情表格 | ⚠️ 可选 |

---

### 5. 销售排名 (Sales Rank)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **BSR 排名** | Best Sellers Rank | 详情表格 | ✅ 推荐 |
| **分类路径** | Category | 页面顶部/BSR | ✅ 推荐 |
| **子类目排名** | Subcategory Rank | BSR 详情 | ⚠️ 可选 |

---

### 6. 媒体内容 (Media Content)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **主图 URL** | Main Image | 图片区域 | ✅ 必填 |
| **附图 URLs** | Additional Images | 图片区域 | ✅ 推荐 |
| **视频 URLs** | Videos | 视频区域 | ⚠️ 可选 |
| **360 度视图** | 360 View | 图片区域 | ❌ 不采集 |

---

### 7. 评论数据 (Reviews)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **评论列表** | Review List | 评论区域 | ✅ 推荐 |
|  - 作者 | Reviewer Name | 每条评论 | ✅ 采集 |
|  - 评分 | Star Rating | 每条评论 | ✅ 采集 |
|  - 标题 | Review Title | 每条评论 | ✅ 采集 |
|  - 内容 | Review Text | 每条评论 | ✅ 采集 |
|  - 日期 | Review Date | 每条评论 | ✅ 采集 |
|  - 验证购买 | Verified Purchase | 每条评论 | ✅ 采集 |
|  - 有用数 | Helpful Count | 每条评论 | ⚠️ 可选 |
| **评分分布** | Rating Breakdown | 评论页面 | ✅ 推荐 |
|  - 5 星数量 | 5 Star | 评分分布 | ✅ 采集 |
|  - 4 星数量 | 4 Star | 评分分布 | ✅ 采集 |
|  - 3 星数量 | 3 Star | 评分分布 | ✅ 采集 |
|  - 2 星数量 | 2 Star | 评分分布 | ✅ 采集 |
|  - 1 星数量 | 1 Star | 评分分布 | ✅ 采集 |
| **热门好评** | Top Positive Review | 评论区域 | ⚠️ 可选 |
| **热门差评** | Top Critical Review | 评论区域 | ⚠️ 可选 |

---

### 8. 关联商品 (Related Products)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **经常一起购买** | Frequently bought together | 关联区域 | ⚠️ 可选 |
| **相似商品** | Similar items | 关联区域 | ⚠️ 可选 |
| **赞助商品** | Sponsored products | 关联区域 | ❌ 不采集 |
| **看了又看** | Customers who viewed also viewed | 关联区域 | ❌ 不采集 |

---

### 9. 促销信息 (Promotions)

| 字段 | 英文字段名 | 页面位置 | 是否采集 |
|------|-----------|----------|----------|
| **优惠券** | Coupon | 价格区域 | ⚠️ 可选 |
| **促销活动** | Promotion | 促销区域 | ⚠️ 可选 |
| **限时优惠** | Deal of the Day | 促销区域 | ⚠️ 可选 |
| **订阅折扣** | Subscribe & Save | 价格区域 | ⚠️ 可选 |

---

## 📊 采集字段优先级

### P0 - 必填字段 (核心数据)

```json
{
  "asin": "商品 ASIN",
  "title": "商品标题",
  "brand": "品牌",
  "price": "当前价格",
  "rating": "评分",
  "reviewCount": "评论数",
  "availability": "库存状态",
  "isPrime": "Prime 资格 (boolean)",
  "mainImage": "主图 URL"
}
```

### P1 - 推荐字段 (重要数据)

```json
{
  "listPrice": "原价",
  "discount": "折扣金额",
  "discountPercent": "折扣百分比",
  "bulletPoints": "特性要点 (数组)",
  "soldBy": "卖家名称",
  "shipsFrom": "发货方",
  "isFBA": "是否 FBA (boolean)",
  "bsr": "BSR 排名",
  "category": "分类路径",
  "ratingDistribution": "评分分布",
  "additionalImages": "附图 URLs (数组)"
}
```

### P2 - 可选字段 (扩展数据)

```json
{
  "description": "商品描述",
  "specifications": "规格参数 (对象)",
  "reviews": "评论列表 (数组)",
  "videos": "视频 URLs (数组)",
  "coupon": "优惠券信息",
  "deliveryDate": "到货日期"
}
```

---

## 🎯 完整数据采集模板

```json
{
  "collectionInfo": {
    "task": "Amazon Product Scraper",
    "collectedAt": "2026-03-15T04:30:00+08:00",
    "marketplace": "US",
    "version": "2.3"
  },
  "products": [
    {
      "basic": {
        "asin": "B0BYNYWKC7",
        "title": "商品完整标题",
        "brand": "品牌名称",
        "price": "$15.99",
        "listPrice": "$35.99",
        "discount": "$20.00",
        "discountPercent": "56%",
        "rating": 4.5,
        "reviewCount": 8421,
        "availability": "In Stock",
        "isPrime": true
      },
      "seller": {
        "soldBy": "卖家名称",
        "shipsFrom": "发货地点",
        "isFBA": true
      },
      "details": {
        "bulletPoints": ["要点 1", "要点 2", "要点 3"],
        "description": "商品描述",
        "specifications": {
          "Material": "材质",
          "Color": "颜色",
          "Size": "尺寸"
        }
      },
      "ranking": {
        "bsr": 306,
        "category": "Beauty & Personal Care",
        "subcategory": "Fingernail & Toenail Clippers"
      },
      "media": {
        "mainImage": "https://...",
        "additionalImages": ["https://...", "https://..."],
        "videos": ["https://..."]
      },
      "reviews": {
        "ratingDistribution": {
          "5star": 70,
          "4star": 20,
          "3star": 5,
          "2star": 3,
          "1star": 2
        },
        "topReviews": [
          {
            "author": "评论作者",
            "rating": 5,
            "title": "评论标题",
            "text": "评论内容",
            "date": "2026-03-01",
            "verified": true,
            "helpful": 100
          }
        ]
      }
    }
  ]
}
```

---

## 📝 采集说明

### 必须采集 (P0)
- 所有 P0 字段必须采集
- 如果某个字段不存在，记录为 `null` 或 `"N/A"`
- 不能跳过整个商品

### 推荐采集 (P1)
- 尽可能采集所有 P1 字段
- 如果页面没有该信息，可以跳过
- 不影响整体采集

### 可选采集 (P2)
- 根据时间和需求决定是否采集
- 快速模式下可以跳过
- 完整模式下建议采集

---

**此清单用于指导采集脚本开发，确保采集所有重要信息！** 🦞
