# intentdiff-registry

The **official IntentDiff plugin registry** — the root of trust for plugin discovery and
verified installs. The IntentDiff client fetches `registry.yaml` from this repo; an entry
here asserts what a plugin is, where it comes from, and the exact artifact checksums an
install must match.

## Contents

- **`registry.yaml`** — the manifest: plugins keyed by name, each with its git source,
  pinned ref, SHA-256 `wasm_checksums` of the built component, `trust_tier`,
  `capabilities`, and the `abi_target` contract version the host gates on.
- **`registry.schema.json`** — the JSON Schema (draft 2020-12) the manifest must satisfy.
- **`registry_schema.py`** — the dependency-free validator + catalog generator
  (`python registry_schema.py registry.yaml [--catalog]`).
- **`CATALOG.md`** — the generated, human-readable plugin catalog.
- **`.github/workflows/vet.yml`** — the PR gate: schema + trust validation and a
  catalog-freshness check on every change. Adding or changing a plugin is a PR that must
  pass vetting; that is what makes this repo the root of trust.

## Trust model

- `trust_tier: official` — org-built and scanned; `wasm_checksums` present; installs are
  verified against them. The initial 69 official parser entries are pinned to their split
  repos' commits, with checksums taken from certified component builds (validated against
  the engine's plugin-host hardening suite before registration).
- `trust_tier: community` — listed but unverified; installs warn.
- `abi_target` — the plugin contract version; the host refuses incompatible plugins at
  resolve time.

## Provenance

Schema and validator are vendored from the IntentDiff monorepo
(`buchochelliq-labs/intentdiff`), which remains the archive of record; the master copies
live with the Python binding until its extraction.

License: MIT.
