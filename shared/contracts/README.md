# Optional legacy structured export — v1.2

This directory preserves six JSON schemas for users explicitly requesting the legacy structured export. Ordinary review uses natural-language goals and [quality criteria](../quality-rubric.md); these files are not task admission or business-completion gates.

The optional export consists of project-profile, file-manifest, requirements, coverage, findings and review-report JSON products. For that export, conform to the unchanged Draft-07 schemas in `schemas/`, each identified by `tender-review/contracts/v1.2/schemas/<name>.schema.json`. Export artifacts declare `contract_version: v1.2`; version references and coverage accounting must remain consistent.

The Evidence skill retains `scripts/validate_report.py` and its optional pinned dependencies. It checks structure and internal export consistency, not whether independent source reading occurred or conclusions are correct. Unavailable validation limits the requested export; useful narrative review can still proceed.

[Manifest](CONTRACT-MANIFEST.md) lists the resources. [Report outline](report-template.md) is an adaptable human-readable guide, not a mandatory output shape.
