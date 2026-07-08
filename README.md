# Amazon Listing 审计与优化工具

> 基于亚马逊 AI 搜索时代逻辑，对产品 Listing 进行全面审计、评分和优化建议。

## 功能特性

- **14 维度评分体系** — 标题、Highlights、五点描述、图片、属性、搜索词等全方位打分
- **CDQ 评分** — Catalog Data Quality 量化评估，含红线检查
- **AI Shopping Checklist** — 适配 A10 / COSMO / Alexa for Shopping 三层架构
- **竞品深度分析** — 自动抓取 3-5 个竞品，生成对比矩阵
- **Review 语义聚类** — 6 大主题正面/负面高频词分析
- **批量审计** — 先共性后个性，单 ASIN 节省约 43% 步数
- **优化文案包** — 可直接复制到 Seller Central 的标题/Bullet/Search Terms
- **品类差异化** — 支持 6 个卫浴品类独立配置

## 支持站点

美国 🇺🇸 | 英国 🇬🇧 | 德国 🇩🇪 | 法国 🇫🇷 | 日本 🇯🇵 | 加拿大 🇨🇦 | 澳大利亚 🇦🇺 | 意大利 🇮🇹 | 西班牙 🇪🇸 | 墨西哥 🇲🇽

## 支持品类

| 品类 | 配置文件 |
|------|---------|
| 厨房水龙头 | `references/categories/kitchen-faucet.md` |
| 面盆水龙头 | `references/categories/basin-faucet.md` |
| 浴缸水龙头 | `references/categories/bathtub-faucet.md` |
| 花洒/淋浴系统 | `references/categories/shower-system.md` |
| 淋浴软管 | `references/categories/shower-hose.md` |
| 浴室挂件 | `references/categories/bathroom-accessories.md` |

> 通用模板：`references/categories/_template.md`，可适配其他品类。

## 目录结构
├── SKILL.md # 核心逻辑与完整工作流程
├── assets/
│ ├── report-template.html # HTML 报告模板（含样式）
│ └── report-template.md # Markdown 报告模板
└── references/
├── amazon-ai-features.md # 亚马逊 AI 搜索架构说明
├── audit-history-schema.md # 审计历史 JSON Schema
├── bathroom-faucet-keywords.md # 浴室水龙头关键词库
├── competitor-analysis.md # 竞品分析方法论
├── compliance-checklist.md # 合规检查清单 + CDQ 红线
├── scoring-rubric.md # 14 维度评分标准
└── categories/ # 品类配置目录
├── _template.md # 通用模板
├── kitchen-faucet.md
├── basin-faucet.md
├── bathtub-faucet.md
├── shower-system.md
├── shower-hose.md
└── bathroom-accessories.md

text

## 工作流程概览

## 工作流程概览
第零步 审计前数据准备（询问后台数据 + 品类识别）
第一步 获取 Listing 信息（7 级降级策略）
第二步 竞品深度分析
第三步 Review 深度分析
第四步 视频内容分析（如有）
第五步 逐维度审计评分（14 维度）
第六步 CDQ 评分量化
第七步 AI 改写风险评估
第八步 AI Shopping Checklist + Alexa 视角
第九步 生成报告
第十步 生成优化文案包
第十一步 FAQ / Q&A 问答库
第十二步 运营落地清单
第十三步 记录审计历史
第十四步 批量审计（团队场景）
第十五步 交付与跟进

text

## 输出示例

- **HTML 报告**：`listing-audit-{ASIN}-{date}.html`（含完整样式，可直接浏览器打开）
- **Markdown 报告**：`listing-audit-{ASIN}-{date}.md`（备用格式）
- **优化文案包**：标题 / Highlights / Bullet Points / Search Terms / A+ 建议

## 版本

当前版本：**V5.5.6**（2026-06-30）

详见 `SKILL.md` 中的 changelog。

## License

Private / Internal Use

## 输出示例

- **HTML 报告**：`listing-audit-{ASIN}-{date}.html`（含完整样式，可直接浏览器打开）
- **Markdown 报告**：`listing-audit-{ASIN}-{date}.md`（备用格式）
- **优化文案包**：标题 / Highlights / Bullet Points / Search Terms / A+ 建议

## 版本

当前版本：**V5.5.6**（2026-06-30）

详见 `SKILL.md` 中的 changelog。

## License

Private / Internal Use
