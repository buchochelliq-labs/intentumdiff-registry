# Submitting a plugin entry

1. **Build + verify your plugin** per the
   [plugin guide](https://github.com/buchochelliq-labs/intentdiff-plugin-sdk/blob/main/docs/PLUGIN_GUIDE.md)
   (deterministic tree, compliance tests green, component builds for `wasm32-wasip2`).
2. **Compute artifact checksums**: SHA-256 of each bundled `.wasm` (lowercase hex).
3. **Add your entry** to `registry.yaml` under `plugins:` — key = your package-safe name:

   ```yaml
   my-lang-parser:
     source: git
     ref: <full 40-char commit SHA>       # strict pinning
     repo: https://github.com/you/my-lang-parser   # omit for official org repos
     description: "One-line summary for the catalog"
     wasm_checksums:
       my_lang_parser.wasm: <sha256 hex>
     trust_tier: community                 # official is asserted by the org only
     capabilities: [parser]
     abi_target: "1.0.0"
   ```

4. **Regenerate the catalog** and include it in the PR:
   `python registry_schema.py registry.yaml --catalog > CATALOG.md`
5. **Open the PR.** The vetting gate validates schema shape, ref/checksum/dep-hash formats,
   and catalog freshness; reviewers check capability claims and provenance. Merge = listed.

Entries without checksums install as unverified (warn); official tier requires org review.
