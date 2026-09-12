# 可选旧结构化导出 — v1.2

本目录保留六类 JSON Schema，供用户明确要求旧结构化导出时使用。普通复核依自然语言目标和[质量标准](../quality-rubric.zh-CN.md)开展，这些文件不是任务准入或业务完成门槛。

可选导出包含 project-profile、file-manifest、requirements、coverage、findings 和 review-report 六类 JSON。选择该导出时遵循 `schemas/` 内保留的 Draft-07 Schema，标识为 `tender-review/contracts/v1.2/schemas/<name>.schema.json`。导出声明 `contract_version: v1.2`，版本引用和覆盖计数应一致。

Evidence 技能保留 `scripts/validate_report.py` 及其可选锁定依赖，检查格式和导出内部一致性，不证明实际独立读取或结论正确。校验不可用仅限制所请求的导出，有用的自然语言复核仍可继续。

[资源清单](CONTRACT-MANIFEST.zh-CN.md)列明文件，[报告提纲](report-template.zh-CN.md)是可调整的人类可读指引，不是固定输出形状。
