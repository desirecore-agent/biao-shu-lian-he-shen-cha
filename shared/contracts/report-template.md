# Tender Review Report Template (contract v1.2)

This is the English reference for `review-report.json`. The Lead single-writes it. Replace identifiers and scope with evidence-backed values. The conservative example is an honest partial report; use `pass` only when coverage and failure gates allow it.

## JSON example

```json
{
  "contract_version": "v1.2",
  "report_id": "REPORT_ID",
  "scope": "Explicit reviewed scope; list exclusions and incomplete areas",
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
  "disclaimers": ["Assistance-level review only; not an official procurement decision."]
}
```

## Field contract

| Field | Type | Required | Rule |
|---|---|---:|---|
| contract_version | string const v1.2 | yes | Exact product contract version |
| report_id | nonempty string | yes | Stable report identifier |
| scope | nonempty string | yes | Explicit reviewed/excluded/incomplete scope |
| inputs_version.manifest_id | nonempty string | yes | Matches file-manifest and downstream products |
| coverage_ref | object | yes | ID, closed state and counts match coverage |
| conclusion | enum | yes | pass, pass_with_cautions, issues_found, partial_only, cannot_conclude |
| unresolved | string array | yes | Items requiring authorized human decision |
| unchecked_items | object array | yes | Each entry records item/reason |
| tool_failures | object array | yes | failure required; unresolved failures block pass |
| review_summary | object or null | no | reviewed_count required when object; notes is one issue-linked string |
| disclaimers | string array | no | Additional limitations; never null |

## Admission rules

- Machine `result=pass` validates the pack; it is not the report conclusion or proof of independent re-reading.
- pass/pass_with_cautions requires closed coverage, no effective unchecked items and no unresolved tool failure.
- partial_only/cannot_conclude preserves failed, partial, unchecked, excluded and recovery limitations.
- All manifest bindings match; changed input creates a new manifest and invalidates stale conclusions.
- This team provides assistance only. Authorized humans or procurement authorities make binding decisions.
