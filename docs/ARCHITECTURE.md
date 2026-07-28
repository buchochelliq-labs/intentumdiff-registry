# intentdiff-registry architecture — the root of trust

The registry decouples *how many plugin repos exist* from *what is trusted*. The client
fetches `registry.yaml` from this repo; an entry asserts identity, provenance, and the exact
artifact bytes an install must match.

## Trust model

- **`trust_tier: official`** — org-built and scanned; `wasm_checksums` (SHA-256 per bundled
  `.wasm`) present; installs verify or fail. Entries missing checksums are demoted to
  community behavior at resolve time.
- **`trust_tier: community`** — listed but unverified; installs warn.
- **Pinning** — `source: git` entries pin a `ref`; strict mode requires a full 40-char commit
  SHA (reproducible, tamper-evident). `dep_hashes` pin any pip dependencies
  (`--require-hashes`).
- **`abi_target`** — the plugin contract version; the host refuses incompatible plugins at
  resolve time, before anything is instantiated.
- **`provenance_manifest_ref`** — links an entry to its Wasm provenance manifest
  (filename → SHA-256 + source commit).

## Enforcement

The PR gate (`.github/workflows/vet.yml`) runs the vendored dependency-free validator
(`registry_schema.py`) — JSON-Schema shape + trust checks + a catalog-freshness diff — so a
registry change cannot merge unvetted. `CATALOG.md` is generated from the manifest and must
stay in sync.

Schema/validator masters currently live with the Python binding
([intentdiff-python](https://github.com/buchochelliq-labs/intentdiff-python)); the copies here
are vendored for the gate.
