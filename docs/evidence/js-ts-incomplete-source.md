# JS/TS partial-signature candidate

Candidate: parser PR [#5](https://github.com/buchochelliq-labs/intentumdiff-js-ts-parser/pull/5),
commit `c007224439a623d72209e9a83b9bb519227ef569`.
The Rust parser retains ERROR/missing tokens so core can report changes inside
incomplete syntax rather than equating empty semantic trees. Requires core's
source fallback (core PR #46); no Python processing is introduced.

The pin uses the **CI-built component**, not a local checksum:

- Successful build/test run: [35524279013](https://github.com/buchochelliq-labs/intentumdiff-js-ts-parser/actions/runs/35524279013).
- Artifact: `parser-wasm`, ID `10608989692`, attributed to the exact candidate SHA.
- ZIP SHA256 verified against GitHub's digest: `cc9d0f89ce03b4394a920fdf6bce459314b3b17e616621337f1ebfea1ab8124c`.
- Component SHA256: `3990e217dbadb3624a2793f9a08c600b1e9c3b6d0accfbf7b5fe50712a7e8a42`.

The local development build had a different checksum. This candidate therefore
uses downloaded CI bytes, with real-component acceptance rerun before publication;
no byte-for-byte reproducibility between local and CI builds is asserted.

Registry schema/trust validation passes for all 69 entries. CATALOG.md was
regenerated and compared with fresh generator output. Schema/validator masters
were re-vendored from intentumdiff-python and were already byte-identical.
Only the JS/TS entry changes. This is a reviewed adoption candidate targeting
release/v0.0.2-rc; no registry merge, plugin release or downstream pin bypass.

Downloaded CI bytes passed 71 public/native acceptance and regression checks.
An independent reviewer reran the 9 JS/TS/TSX acceptance cases against those bytes,
recomputed the component checksum, checked the exact commit pin, reran all registry
gates and confirmed the generated catalog and schema/validator masters match.
No blocking findings; approved for PR publication, not merge.
