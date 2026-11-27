# Valkey 9.2.1 — ReadyStack release `9.2.1-CE-ubuntu24.04-r1`

Generated 2026-11-27 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/valkey:9.2.1-CE-ubuntu24.04-r1` (linux/amd64). Index digest `sha256:741b0b6cb3064149249d0bf3fd70cbb164de9a69e58d25bdcd0acae1413d4125` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:c0ed093167c7835f8f3d797fa7b6eb7ae6f45c41282b8c5cc314201f17204c9b` [`TARGET_DIGEST.txt`].
- **Upstream:** Valkey 9.2.1 built from source at `9.2.1` of https://github.com/valkey-io/valkey — upstream notes: https://github.com/valkey-io/valkey/releases/tag/9.2.1 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `valkey`.
- **Build:** `source-rebuild-c`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `9.2.0-CE-ubuntu24.04-r2`.

## What changed in this release

- Upstream version 9.2.0 → 9.2.1.
- This release moves Valkey from 9.2.0 to 9.2.1, a newer release of upstream's 9.2.x line. Upstream's release notes list what changed: https://github.com/valkey-io/valkey/releases/tag/9.2.1

## Security status at release (measured 2026-11-27)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `valkey` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/valkey:9.2.1-CE-ubuntu24.04-r1` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.
- **Before exposing this service:** Clients on other hosts can connect only after you set VALKEY_PASSWORD (requirepass); without it the server accepts only in-container clients. The shipped configuration has no TLS: keep the port on a private network, or enable tls-port with your own certificates (valkey-server is built with TLS support).

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:c0ed093167c7835f8f3d797fa7b6eb7ae6f45c41282b8c5cc314201f17204c9b`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 8 of 8 use cases passed (8 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None found (reviewed by held semantic review (Claude) on 2026-11-27).

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/valkey:9.2.1-CE-ubuntu24.04-r1
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

