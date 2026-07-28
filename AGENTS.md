# Agent instructions — intentdiff-registry

The root of trust: registry.yaml pins every official plugin (commit SHA + SHA-256 checksums).

## Hard invariants
- Every manifest change must pass the vet gate (schema + trust + catalog freshness).
- CATALOG.md is GENERATED — regenerate, never hand-edit:
  `python registry_schema.py registry.yaml --catalog > CATALOG.md`
- Schema/validator masters live in intentdiff-python; re-vendor here in the same change.

Map: docs/ARCHITECTURE.md (trust model) · docs/SUBMITTING.md · CONTRIBUTING.md.
