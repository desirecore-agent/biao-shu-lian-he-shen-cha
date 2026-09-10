# 标书联合审查报告模板（契约 v1.2）

这是 `review-report.json` 的中文同形参考模板。最终报告由总审单写。所有标识和范围必须替换为有证据的值。本保守示例是诚实 partial；只有覆盖与失败门禁允许时才能改为 `pass`。

## JSON 示例

```json
{
  "contract_version": "v1.2",
  "report_id": "REPORT_ID",
  "scope": "明确的已审范围；列出排除项与未完成区域",
  "inputs_version": {"manifest_id": "MANIFEST_ID"},
  "coverage_ref": {
    "coverage_id": "COVERAGE_ID",
    "coverage_closed": false,
    "planned_items": 0,
    "completed_items": 0,
    "failed_items": 0,
    "unchecked_items": 0
  },
  "conclusion": "partial_only",
  "unresolved": [],
  "unchecked_items": [],
  "tool_failures": [],
  "review_summary": null,
  "disclaimers": ["仅供辅助审查，不构成正式采购评审决定。"]
}
```

## 字段契约

| 字段 | 类型 | 必填 | 规则 |
|---|---|---:|---|
| contract_version | 字符串常量 v1.2 | 是 | 精确产品契约版本 |
| report_id | 非空字符串 | 是 | 稳定报告标识 |
| scope | 非空字符串 | 是 | 明确已审、排除与未完成范围 |
| inputs_version.manifest_id | 非空字符串 | 是 | 匹配文件台账及下游产物 |
| coverage_ref | 对象 | 是 | ID、闭合状态与计数匹配覆盖台账 |
| conclusion | 枚举 | 是 | pass、pass_with_cautions、issues_found、partial_only、cannot_conclude |
| unresolved | 字符串数组 | 是 | 需授权人决定的事项 |
| unchecked_items | 对象数组 | 是 | 每项记录 item/reason |
| tool_failures | 对象数组 | 是 | failure 必填；未恢复失败阻断 pass |
| review_summary | 对象或 null | 否 | 为对象时 reviewed_count 必填；notes 是单个、关联 issue 的字符串 |
| disclaimers | 字符串数组 | 否 | 附加限制，不得为 null |

## 准入规则

- 机器 `result=pass` 只表示数据包通过校验，不等于报告业务结论或独立重读已经发生。
- pass/pass_with_cautions 要求覆盖闭合、无有效未检查项、无未恢复工具失败。
- partial_only/cannot_conclude 保留 failed、partial、unchecked、excluded 与恢复限制。
- 所有 manifest 绑定必须一致；输入变化生成新 manifest 并使旧结论失效。
- 本团队只提供辅助审查；正式决定由授权用户或有权评审机构作出。
