# 共享契约 — Schema 与产物参考

> **状态**：v1.2 候选文档。校验前，核验当前安装团队的六份 Schema 身份与哈希，以及匹配 Evidence 发行版的代码、公开 Skill/文档、已审依赖锁和已初始化运行时回执。前提缺失或不匹配时阻断校验；历史结果不能证明当前安装具备运行能力。

## 概述

`shared/contracts/` 目录包含 `tender-review` 团队的权威 v1.2 契约 Schema 和配套文档。所有审查产物必须符合这些 Schema。

## 目录结构

```
shared/contracts/
├── schemas/
│   ├── project-profile.schema.json
│   ├── file-manifest.schema.json
│   ├── requirements.schema.json
│   ├── coverage.schema.json
│   ├── findings.schema.json
│   └── review-report.schema.json
├── report-template.md
├── report-template.zh-CN.md
├── CONTRACT-MANIFEST.md
├── README.md
└── README.zh-CN.md  ← 本文件
```

## 契约版本

- **当前版本**：v1.2
- **Schema 标准**：JSON Schema Draft-07（`http://json-schema.org/draft-07/schema#`）
- **版本身份**：每份 Schema 的 `$id` 为 `tender-review/contracts/v1.2/schemas/<name>.schema.json`
- **产品身份**：每份产物必填 `contract_version`，值为 `v1.2`

## 版本绑定

- `manifest_id` 是 `file-manifest.json` 携带的不可变版本键。
- `requirements.json`、`coverage.json` 和 `findings.json` 各自携带 `manifest_id`——同一审查周期内必须与台账的 `manifest_id` 一致。
- `review-report.json` 的 `inputs_version.manifest_id` 也必须匹配。
- 材料变化时生成新 `manifest_id`；绑定旧版本的产物全部失效，必须重新检查。

## 六份必填产物

| # | 产物 | 文件 | 根级必填字段（contract_version 除外） |
|---|------|------|--------------------------------------|
| 1 | 项目画像 | `project-profile.json` | project_id、procurement_program、classification_basis |
| 2 | 文件台账 | `file-manifest.json` | manifest_id、files |
| 3 | 条款矩阵 | `requirements.json` | matrix_id、manifest_id、requirements |
| 4 | 覆盖台账 | `coverage.json` | coverage_id、manifest_id、coverage_closed、planned_items、completed_items、failed_items、unchecked_items、coverage_file_ids、items |
| 5 | 发现 | `findings.json` | findings_id、manifest_id、findings |
| 6 | 审查报告 | `review-report.json` | report_id、scope、inputs_version、coverage_ref、conclusion、unresolved、unchecked_items、tool_failures |

所有 Schema 根级 `additionalProperties: false`；嵌套对象通常也封闭。

## 关键业务规则（由校验器编码，不仅是文档说明）

- **覆盖闭合**：分母 = completed + failed + unchecked；未闭合 → 仅 partial_only/cannot_conclude。
- **双边证据**：potential_rejection 发现须同时有招标侧（requirement_refs）和投标侧（bid_evidence）可定位证据。
- **版本绑定**：`manifest_id` 在台账、覆盖、发现和报告间必须一致。
- **SHA-256**：严格 64 位小写十六进制 fullmatch；尾部换行拒绝。
- **结论准入**：覆盖未闭合或含未解决失败时，禁止 pass/pass_with_cautions。
- **排除文件**：`coverage.excluded` 是字符串数组；每条须为 "file_id: 非空理由"；裸 ID 或空理由不是有效排除。
- **复核追溯**：撤回/降级理由在 `findings[].limitations` 或 `report.review_summary.notes`（字符串）中；findings 无 `review_reason` 字段。

## Schema 校验

校验器使用 `jsonschema==4.25.1`（MIT，Python>=3.9），包括：
- `Draft7Validator.check_schema()` 校验元 Schema
- `Draft7Validator` + `FormatChecker` 校验实例
- 本地 Registry——不进行远程 `$ref` 解析

Schema 校验是结构性的，不保证业务一致性，也不证明独立重读已发生。

## 人工审查边界

本团队只提供**辅助审查**：
- 发现是标记为"潜在问题，需人工复核"的线索——不是评审结论。
- 资格否决、响应有效性及其他正式裁定由授权用户或评审机构作出。
- 智能体可以指出招标文件明示的后果及风险，但不能将自身判断伪称正式否决或法律裁定。

## 不包含的内容

- 校验器脚本在证据技能中，不在共享契约目录。
- 依赖锁文件由证据技能管理。
- 开发/测试产物、私人审查路径和智能体工作目录已排除。
- 历史哈希标记为 pending；最终稳定哈希由独立 assembler 从冻结制品生成。
