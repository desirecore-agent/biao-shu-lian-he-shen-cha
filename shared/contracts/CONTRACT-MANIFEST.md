# Contract Manifest — v1.2

> **Status**: Pre-release development draft. All hashes are pending until generated from final frozen artifacts by an independent assembler.

## Overview

This document describes the v1.2 contract specification for the `tender-review` team. It is the public-facing reference; internal development paths, test results, and private review history are excluded.

## Contract Version

- **Version**: v1.2
- **Schema Standard**: JSON Schema Draft-07 (`http://json-schema.org/draft-07/schema#`)
- **Authoritative Location**: `<TEAM_ROOT>/shared/contracts/schemas/`
- **Version Identity**: Each schema's `$id` = `tender-review/contracts/v1.2/schemas/<name>.schema.json`
- **Product Identity**: Every artifact carries required `contract_version` with `const: "v1.2"`

## v1.2 Key Changes from v1.1

| Change | Description |
|--------|-------------|
| `contract_version` required | All six products must declare v1.2; empty objects are not contracts |
| `manifest_id` required non-null | In requirements, coverage, findings, and report's inputs_version |
| `coverage_file_ids` required | Coverage must declare its full file set |
| `coverage.excluded` string format | Must be "file_id: non-empty reason"; bare IDs rejected |
| checked items require method/location | At least one non-empty |
| `searched_coverage_item_ids` | Required for absence-type bid evidence |
| SHA-256 fullmatch | Strict 64-char hex; trailing newline rejected |
| Supersede consistency | `superseded_by` ↔ `supersede_relations` must be consistent, acyclic, with existing endpoints |

## Six Artifacts

| Artifact | File | Purpose |
|----------|------|---------|
| Project Profile | `project-profile.json` | Procurement context, program classification |
| File Manifest | `file-manifest.json` | Input file inventory with SHA-256, roles, page counts |
| Requirements Matrix | `requirements.json` | Clause extraction with source attribution |
| Coverage Ledger | `coverage.json` | Per-file, per-item coverage with closure status |
| Findings | `findings.json` | Issues with severity, certainty, bilateral evidence |
| Review Report | `review-report.json` | Final report with conclusion and open items |

## Validator

- **Library**: jsonschema 4.25.1 (MIT, Python ≥ 3.9)
- **Method**: Draft7Validator.check_schema + instance validation + FormatChecker
- **Registry**: Local-only; no remote $ref resolution
- **Business rules**: Implemented in validator code, not in the schema library
- **Installation requirement**: Verify the matching installed Evidence release ref, code, public Skill/docs, reviewed dependency lock, and initialized runtime receipt, plus the team’s six schema identities and hashes. Missing or mismatched prerequisites block validation; historical results do not establish current installation capability.

## Report Templates

| Template | Language | Status |
|----------|----------|--------|
| `report-template.md` | English | v1.2 candidate draft |
| `report-template.zh-CN.md` | Chinese | v1.2 candidate draft |

## File Hashes

> **Note**: All hashes are pending. They will be generated from the final stable artifacts by an independent assembler program. Do not use placeholder values or manually copy hashes.

| File | SHA-256 | Status |
|------|---------|--------|
| schemas/project-profile.schema.json | pending | draft |
| schemas/file-manifest.schema.json | pending | draft |
| schemas/requirements.schema.json | pending | draft |
| schemas/coverage.schema.json | pending | draft |
| schemas/findings.schema.json | pending | draft |
| schemas/review-report.schema.json | pending | draft |
| report-template.md | pending | draft |
| report-template.zh-CN.md | pending | draft |
| CONTRACT-MANIFEST.md | pending | draft (self-referential) |

## Scope and Limitations

- The validator performs structural and business-rule checks on the data pack.
- Machine validation does not equal independent re-reading or business consistency.
- This team provides assistance-level review only; it does not make binding decisions.
- Cloud model providers may process submitted text and images; this does not authorize redistribution.
- Provider configuration does not guarantee fully local processing.
