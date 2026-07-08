# 审计历史数据结构定义

> 文件路径：`memory/listing-audit-history.json`
> 用途：记录历次 Listing 审计结果，支持查询、对比、团队汇总

## Schema 定义

```json
{
  "$schema": "listing-audit-history-v1",
  "audits": [
    {
      "id": "audit_{YYYYMMDD}_{序号}",
      "asin": "B0XXXXXXXX",
      "marketplace": "US",
      "product_title": "完整产品标题",
      "brand": "品牌名",
      "category": "类目路径",
      "audit_date": "YYYY-MM-DD",
      "audit_version": "V5.2.0",
      "fetch_method": "web_fetch desktop | web_fetch mobile | agent-browser | 用户提供",
      "user_provided_data": ["CVR", "CTR", "Search Terms"],
      "missing_fields": ["BSR", "广告数据"],

      "scores": {
        "total": 7.2,
        "cdq": 6.8,
        "ai_readiness_level": "中",
        "dimensions": {
          "d1_title": { "score": 8, "weight": 0.11, "weighted": 0.9 },
          "d2_highlights": { "score": 6, "weight": 0.07, "weighted": 0.4 },
          "d3_bullets": { "score": 7, "weight": 0.09, "weighted": 0.6 },
          "d4_description": { "score": 5, "weight": 0.05, "weighted": 0.3 },
          "d5_search_terms": { "score": 6, "weight": 0.05, "weighted": 0.3 },
          "d6_entity_seo": { "score": 7, "weight": 0.09, "weighted": 0.6 },
          "d7_attributes": { "score": 8, "weight": 0.09, "weighted": 0.7 },
          "d8_images": { "score": 9, "weight": 0.12, "weighted": 1.1 },
          "d9_pricing": { "score": 5, "weight": 0.05, "weighted": 0.3 },
          "d10_reviews": { "score": 6, "weight": 0.07, "weighted": 0.4 },
          "d11_competitors": { "score": 4, "weight": 0.03, "weighted": 0.1 },
          "d12_category": { "score": 7, "weight": 0.03, "weighted": 0.2 },
          "d13_compliance": { "score": 8, "weight": 0.05, "weighted": 0.4 },
          "d14_performance": { "score": 5, "weight": 0.10, "weighted": 0.5 }
        },
        "extras": {
          "video": 7,
          "review_deep": 6,
          "conversion": 5,
          "scenario": 4,
          "compat": 8
        }
      },

      "cdq_detail": {
        "total": 6.8,
        "structured_attr": { "score": 8, "weight": 0.30 },
        "title_quality": { "score": 8, "weight": 0.25 },
        "bullets": { "score": 7, "weight": 0.15 },
        "image_quality": { "score": 9, "weight": 0.15 },
        "other_content": { "score": 5.5, "weight": 0.15 },
        "redlines_passed": 5,
        "redlines_total": 6,
        "redline_failures": ["标题与属性不一致"]
      },

      "top3_issues": [
        "标题超75字符（当前89字符）",
        "Search Terms未填",
        "缺A+内容"
      ],
      "top3_actions": [
        "精简标题至75字符内",
        "填写Search Terms 250字节",
        "创建A+内容"
      ],

      "report_path": "listing-audit-B0XXXXXXXX-2026-06-27.md",
      "competitors_analyzed": ["B0YYYYYYYY", "B0ZZZZZZZZ"],
      "notes": "用户未提供后台数据，维度14按默认5分处理"
    }
  ],

  "team_summary": {
    "last_updated": "YYYY-MM-DD",
    "total_audits": 0,
    "avg_score": 0,
    "avg_cdq": 0,
    "common_issues": []
  }
}
```

## 字段说明

### 必填字段
| 字段 | 类型 | 说明 |
|------|------|------|
| id | string | 审计唯一ID，格式 `audit_{YYYYMMDD}_{序号}` |
| asin | string | 10位 ASIN |
| marketplace | string | 站点代码 |
| audit_date | string | YYYY-MM-DD |
| scores.total | number | 加权总分，保留1位小数 |
| scores.cdq | number | CDQ 总分，保留1位小数 |
| scores.dimensions | object | 14个维度的评分详情 |
| top3_issues | string[] | 3个核心问题 |
| report_path | string | 完整报告文件名 |

### 可选字段
| 字段 | 类型 | 说明 |
|------|------|------|
| user_provided_data | string[] | 用户提供的数据类型列表 |
| missing_fields | string[] | 无法获取的字段 |
| competitors_analyzed | string[] | 分析的竞品 ASIN 列表 |
| notes | string | 备注 |

## 查询场景

### 1. 单 ASIN 历次评分变化
```json
// 按 asin 过滤，按 audit_date 排序
// 输出：date → total/cdq 的趋势
```

### 2. 团队汇总（多 ASIN 最新一次）
```json
// 每个 asin 取最新记录
// 按 scores.total 排名
// 提取共性 top3_issues
```

### 3. 维度对比
```json
// 同一 asin 两次审计的 dimensions 逐项对比
// 输出：每个维度的分数变化（+1 / -1 / 不变）
```

## 写入规则

1. **每次审计完成后写入**（第十三步）
2. **不覆盖历史记录**，只追加新条目
3. **同一 ASIN 同一天多次审计**，序号递增（audit_20260627_001, _002）
4. **team_summary 随时更新**（每次写入后重新计算）

<!-- SKILL V5.4.0 -->
