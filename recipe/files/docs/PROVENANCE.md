# Provenance — Valkey (`9.2.1-CE-ubuntu24.04-r1`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/valkey-io/valkey
- Revision built: `9.2.1` (commit `d1a551720f5feb1a2ff5b9a7b5e22520ae77eeef`)
- Source tree: `aae5cf5c8989548629d1f899727593a821cda5d8ddd8c4fb9b72b3fa1168476b` over 2061 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-c`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795692143` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/valkey:9.2.1-CE-ubuntu24.04-r1` — index digest `sha256:741b0b6cb3064149249d0bf3fd70cbb164de9a69e58d25bdcd0acae1413d4125` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:c0ed093167c7835f8f3d797fa7b6eb7ae6f45c41282b8c5cc314201f17204c9b` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/valkey:9.2.1-CE-ubuntu24.04-r1`

## Pinned inputs, and why

- 22 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 2, pins in the kit's dockerfiles 5, readystack's build engine 6, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.trail.json`, published beside this archive and signed with the release key (`ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.trail.json.sigstore`), and readable at https://readystack.dev/products/valkey/trail/9.2.1-CE-ubuntu24.04-r1.

