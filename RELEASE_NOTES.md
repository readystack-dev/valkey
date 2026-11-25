# Valkey 9.2.0 — ReadyStack release `9.2.0-CE-ubuntu24.04-r2`

Generated 2026-11-22 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/valkey:9.2.0-CE-ubuntu24.04-r2` (linux/amd64). Index digest `sha256:32e67f81acc782fd85516fbf77e7ce9340ee37f4913fc3ad1af13d9653ba542d` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:df5b66c64a2b9afd0e7e8fe29801faa0191a1b91714b59d70994020e312ab244` [`TARGET_DIGEST.txt`].
- **Upstream:** Valkey 9.2.0 built from source at `9.2.0` of https://github.com/valkey-io/valkey — upstream notes: https://github.com/valkey-io/valkey/releases/tag/9.2.0 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `valkey`.
- **Build:** `source-rebuild-c`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `9.2.0-CE-ubuntu24.04-r1`.

## What changed in this release

- Upstream version unchanged (9.2.0); ReadyStack rebuild.
- Valkey 9.2.0 is unchanged from the release this supersedes (9.2.0-CE-ubuntu24.04-r1); this release rebuilds it. Changes: the image is rebuilt on the current ubuntu:24.04 image (sha256:9c7f200c07e3…), which its maintainers updated after 9.2.0-CE-ubuntu24.04-r1 was built on sha256:2198e4c65076…. Settings, ports and data volumes are those of 9.2.0-CE-ubuntu24.04-r1: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-22)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `valkey` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/valkey:9.2.0-CE-ubuntu24.04-r2` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.
- **Before exposing this service:** Clients on other hosts can connect only after you set VALKEY_PASSWORD (requirepass); without it the server accepts only in-container clients. The shipped configuration has no TLS: keep the port on a private network, or enable tls-port with your own certificates (valkey-server is built with TLS support).

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:df5b66c64a2b9afd0e7e8fe29801faa0191a1b91714b59d70994020e312ab244`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 8 of 8 use cases passed (8 authored) against the running image [`docs/validation/test-results.json`].

## Known issues

- None found (reviewed by held semantic review (Claude) on 2026-11-22).

## Defects fixed

- 2 problems found before release and fixed before it shipped (2 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/valkey:9.2.0-CE-ubuntu24.04-r2
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

