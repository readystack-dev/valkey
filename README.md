[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fvalkey-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/valkey) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/valkey)](https://hub.docker.com/r/readystack/valkey) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/valkey) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# Valkey: ReadyStack build kit

The offline build kit for the Docker image `readystack/valkey:9.2.1-CE-ubuntu24.04-r1`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [9.2.1-CE-ubuntu24.04-r1](https://github.com/readystack-dev/valkey/releases/tag/9.2.1-CE-ubuntu24.04-r1)
- Image: [`docker.io/readystack/valkey:9.2.1-CE-ubuntu24.04-r1`](https://hub.docker.com/r/readystack/valkey/tags), manifest digest `sha256:c0ed093167c7835f8f3d797fa7b6eb7ae6f45c41282b8c5cc314201f17204c9b`
- Product page: https://readystack.dev/products/valkey
- Source and build recipe: https://readystack.dev/products/valkey/recipe
- Build trail: https://readystack.dev/products/valkey/trail/9.2.1-CE-ubuntu24.04-r1
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=valkey

## The image

Single container, single self-contained C binary (valkey-server) compiled from source, foreground process (PID 1). An in-memory key-value data store; state persists to disk as an RDB snapshot (and optionally an AOF) under /data. NO relational/SQL database, NO external datastore, NO sidecar. Drop-in Redis-compatible (RESP protocol, reports redis_version 7.2.4 for client compat).

## Who uses Valkey and why

Developers who need a key-value data store for caching, message queues, sessions and other real-time workloads.

Valkey is an open-source key-value datastore and data structure server, used for caching, message queues and as a primary database, with a plugin system for new data structures.

A typical use: A web application computes the same expensive results again and again. It stores each result in Valkey under a key with a timeout; later requests read the stored value instead of recomputing it, and Valkey deletes the entries when their timeout expires.

From the upstream project's own description: https://github.com/valkey-io/valkey, https://valkey.io/, https://valkey.io/commands/expire/.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-27 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 16 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`valkey`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-27; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/valkey.

Valkey is distributed under its upstream licence (BSD-3-Clause); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [9.2.1-CE-ubuntu24.04-r1 release](https://github.com/readystack-dev/valkey/releases/tag/9.2.1-CE-ubuntu24.04-r1): `ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.tar.gz` (526.5 MB), SHA-256 `8861e518436aba86666f19d4a31473a03bbd36b181fd0b16fcef3db3f7d40757`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.rebuild.json.sigstore ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.tar.gz
cd 9.2.1-CE-ubuntu24.04-r1
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-valkey-9.2.1-CE-ubuntu24.04-r1.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/valkey/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev
