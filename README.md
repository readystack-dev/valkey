# Valkey: ReadyStack build kit

The offline build kit for the Docker image `readystack/valkey:9.2.0-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [9.2.0-CE-ubuntu24.04-r2](https://github.com/readystack-dev/valkey/releases/tag/9.2.0-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/valkey:9.2.0-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/valkey/tags), manifest digest `sha256:df5b66c64a2b9afd0e7e8fe29801faa0191a1b91714b59d70994020e312ab244`
- Product page: https://readystack.dev/products/valkey
- Source and build recipe: https://readystack.dev/products/valkey/recipe
- Build trail: https://readystack.dev/products/valkey/trail/9.2.0-CE-ubuntu24.04-r2
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=valkey

## The image

Single container, single self-contained C binary (valkey-server) compiled from source, foreground process (PID 1). An in-memory key-value data store; state persists to disk as an RDB snapshot (and optionally an AOF) under /data. NO relational/SQL database, NO external datastore, NO sidecar. Drop-in Redis-compatible (RESP protocol, reports redis_version 7.2.4 for client compat).

## Who uses Valkey and why

Developers who need a key-value data store for caching, message queues, sessions and other real-time workloads.

Valkey is an open-source key-value datastore and data structure server, used for caching, message queues and as a primary database, with a plugin system for new data structures.

A typical use: A web application computes the same expensive results again and again. It stores each result in Valkey under a key with a timeout; later requests read the stored value instead of recomputing it, and Valkey deletes the entries when their timeout expires.

From the upstream project's own description: https://github.com/valkey-io/valkey, https://valkey.io/, https://valkey.io/commands/expire/.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-22 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 16 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`valkey`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-22; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/valkey.

Valkey is distributed under its upstream licence (BSD-3-Clause); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [9.2.0-CE-ubuntu24.04-r2 release](https://github.com/readystack-dev/valkey/releases/tag/9.2.0-CE-ubuntu24.04-r2): `ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.tar.gz` (526.5 MB), SHA-256 `d20fbcab5792f855f4f4891c1ded5aa9688e21de8aa3ecae34aa66accd739618`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.rebuild.json.sigstore ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.tar.gz
cd 9.2.0-CE-ubuntu24.04-r2
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-valkey-9.2.0-CE-ubuntu24.04-r2.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/valkey/recipe. The complete kit is the release download. Each release is a tag here.

— ReadyStack · https://readystack.dev
