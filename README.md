# Valkey: ReadyStack build kit

The offline build kit for the Docker image `readystack/valkey:9.2.0-CE-ubuntu24.04-r2`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [9.2.0-CE-ubuntu24.04-r2](https://github.com/readystack-dev/valkey/releases/tag/9.2.0-CE-ubuntu24.04-r2)
- Image: [`docker.io/readystack/valkey:9.2.0-CE-ubuntu24.04-r2`](https://hub.docker.com/r/readystack/valkey/tags), manifest digest `sha256:df5b66c64a2b9afd0e7e8fe29801faa0191a1b91714b59d70994020e312ab244`
- Product page: https://readystack.dev/products/valkey
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=valkey

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
