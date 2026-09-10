# 财务 Skills

本目录收录当前已实现的 14 个财务技能指令，适用于对冲基金管理公司的经营财务（FP&A）场景，覆盖数据接入、修复、质量检查、独立总账核对、指标分析、看板和交付。

这是技能指令集。文件中引用的财务工具由配套应用提供；仅复制这些 Markdown 文件不会安装工具或计算引擎。

## 技能目录

下表按常见工作阶段排列。实际只执行用户要求的阶段，不把目录顺序视为必须跑完的流程。

| Skill | 能力 | 依赖工具 |
| --- | --- | --- |
| [finance-data-intake](finance-data-intake/SKILL.md) | 建立来源快照与任务范围 | `parse_finance_task` → `inspect_sources` → `profile_dataset` |
| [finance-domain-fpa](finance-domain-fpa/SKILL.md) | 确定管理公司财务语义 | `resolve_metric` |
| [finance-data-preprocess](finance-data-preprocess/SKILL.md) | 形成可复核的数据修复计划 | `normalize_table` → `match_master_data` → `preview_repairs` → `commit_repairs` |
| [finance-data-quality](finance-data-quality/SKILL.md) | 检查财务数据质量 | `validate_dataset` |
| [finance-data-reconcile](finance-data-reconcile/SKILL.md) | 对独立总账做控制核对 | `reconcile_dataset` |
| [finance-metric-query](finance-metric-query/SKILL.md) | 执行受控指标计算 | `resolve_metric` → `execute_metric_query` |
| [finance-trend-analysis](finance-trend-analysis/SKILL.md) | 形成月度经营趋势 | `compute_trend` |
| [finance-variance-driver](finance-variance-driver/SKILL.md) | 解释金额和百分点贡献 | `compute_variance` → `compute_driver_bridge` |
| [finance-exception-analysis](finance-exception-analysis/SKILL.md) | 发现有证据的费用异常 | `detect_exception` |
| [finance-chart-design](finance-chart-design/SKILL.md) | 生成固定模板图表 | `build_chart_spec` |
| [finance-dashboard-compose](finance-dashboard-compose/SKILL.md) | 组织财务看板 | `render_dashboard` |
| [finance-management-commentary](finance-management-commentary/SKILL.md) | 生成绑定证据的经营说明 | `render_dashboard` → `collect_evidence` |
| [finance-result-assurance](finance-result-assurance/SKILL.md) | 独立复核与最终门禁 | `verify_finance_result` → `export_deliverables` |
| [finance-deliverable-package](finance-deliverable-package/SKILL.md) | 生成可复核交付包 | `verify_finance_result` → `collect_evidence` → `export_deliverables` |

## 运行依赖与接入

- 技能原始实现来自 [Financial-Agent-DS](https://github.com/Leonard8818/Financial-Agent-DS/tree/742f42f9ad90dc5c51104307a0b067123a5aeecc)，本次同步基于提交 `742f42f9ad90dc5c51104307a0b067123a5aeecc`；14 个 `SKILL.md` 保留原内容。
- [工具契约](https://github.com/Leonard8818/Financial-Agent-DS/tree/742f42f9ad90dc5c51104307a0b067123a5aeecc/harness/contracts.mjs)定义 20 个财务工具；[Harness 插件](https://github.com/Leonard8818/Financial-Agent-DS/tree/742f42f9ad90dc5c51104307a0b067123a5aeecc/harness/plugin.mjs)负责工具与技能集成；[财务引擎](https://github.com/Leonard8818/Financial-Agent-DS/tree/742f42f9ad90dc5c51104307a0b067123a5aeecc/finance)执行计算、核对、工作流和交付。
- 运行现有配套应用，请按[原项目说明](https://github.com/Leonard8818/Financial-Agent-DS/tree/742f42f9ad90dc5c51104307a0b067123a5aeecc/README.md)配置环境。迁移至其他 Agent 时，需要提供相应工具实现或适配层，并由宿主加载所需的 `SKILL.md`。
- 本次仅同步 skills 及目录说明。财务引擎、模型接入、运行时数据库和演示数据不包含在这次提交中。

## 使用约束

- 同一任务共用 `run_id`，保留来源哈希、行号、政策与预算版本。
- 仅准备数据材料时不自动执行数据处理；仅处理数据时不自动扩展为经营分析或正式交付。
- 修复必须通过配套应用记录的可信人工确认；模型不能自行构造批准。
- 独立总账核对失败、结果复核失败时，按各技能规则阻断正式结果或导出。
- 本技能集面向管理公司经营财务，不用于基金净值、投资交易或生产财务核算。缺少输入或工具能力时，应明确说明限制。

## 本次同步验证

2026-09-10 已检查 14 个技能的名称、描述与章节结构，确认其引用工具均在原项目工具契约中，并对复制前后文件逐字节比对。此检查验证的是指令文件同步与工具名称对应关系；不代表已经在本仓库接通财务工具或完成真实模型运行验收。
