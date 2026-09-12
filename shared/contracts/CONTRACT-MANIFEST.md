# Optional export resource manifest — v1.2

These unchanged resources support an explicitly requested legacy export only. They are separate from the outcome-oriented 0.2.0 team instructions.

| Resource | Optional export purpose |
| --- | --- |
| schemas/project-profile.schema.json | Project context |
| schemas/file-manifest.schema.json | Source inventory and versions |
| schemas/requirements.schema.json | Requirement references |
| schemas/coverage.schema.json | Checked, failed and unchecked scope |
| schemas/findings.schema.json | Findings and evidence |
| schemas/review-report.schema.json | Export summary and open items |

All six use Draft-07 and v1.2 identifiers. The retained Evidence validator expects this six-product export and its internal version/coverage consistency. Those requirements do not apply to ordinary natural-language reports. No new frozen hash or validation result is claimed here.

See [README](README.md) and the Evidence skill dependency documentation for optional execution. Installation source/identity locks remain release metadata, not business-task preparation.
