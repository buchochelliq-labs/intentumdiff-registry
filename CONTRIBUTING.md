# Contributing to intentdiff-registry

- Plugin submissions: [docs/SUBMITTING.md](docs/SUBMITTING.md).
- Validate locally before pushing (needs only PyYAML):

  ```bash
  pip install pyyaml
  python registry_schema.py registry.yaml
  python registry_schema.py registry.yaml --catalog > CATALOG.md
  ```

- The vet gate must pass; `CATALOG.md` must match the manifest byte-for-byte.
- Schema changes land in the validator's master (the Python binding repo) first, then get
  re-vendored here in the same change.
