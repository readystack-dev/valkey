# Provenance — Valkey (`9.2.0-CE-ubuntu24.04-r2`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/valkey-io/valkey
- Revision built: `9.2.0` (commit `d23684e3ec302240754664417e3b99df23e8e4c9`)
- Source tree: `349cea9dd30beb04d82c8f4af26837872a747688a99daad2b7d44e0627e2e99e` over 2060 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-c`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795380563` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/valkey:9.2.0-CE-ubuntu24.04-r2` — index digest `sha256:32e67f81acc782fd85516fbf77e7ce9340ee37f4913fc3ad1af13d9653ba542d` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:df5b66c64a2b9afd0e7e8fe29801faa0191a1b91714b59d70994020e312ab244` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/valkey:9.2.0-CE-ubuntu24.04-r2`

## Pinned inputs, and why

- 22 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, dependency versions readystack sets 2, pins in the kit's dockerfiles 5, readystack's build engine 6, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.trail.json`, published beside this archive and signed with the release key (`ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.trail.json.sigstore`), and readable at https://readystack.dev/products/valkey/trail/9.2.0-CE-ubuntu24.04-r2.

