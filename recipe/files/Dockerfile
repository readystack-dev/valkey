# GENERATED L-009 hermetic C build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases; vendored source (in-tree deps) + extra build debs + runtime debs from Dockerfile.vendor.
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS cbuild
# dpkg-install the vendored EXTRA build debs (pkg-config/libssl-dev/...) — gcc/make are in the builder.
RUN --mount=type=bind,source=vendored/build-debs,target=/tmp/bdebs \
    set --; for f in /tmp/bdebs/*.deb; do [ -e "$f" ] && set -- "$@" "$f"; done; \
    for pass in 1 2 3 4 5; do [ $# -eq 0 ] || dpkg -i --skip-same-version "$@" >/dev/null 2>&1 && break; done; \
    dpkg --configure -a && bad= && for d in "$@"; do p=$(dpkg-deb -f "$d" Package) v=$(dpkg-deb -f "$d" Version); \
      case "$(dpkg-query -W -f='${Version} ${db:Status-Abbrev}' "$p" 2>/dev/null)" in "$v ii"*) ;; *) bad="$bad $p=$v" ;; esac; done && \
    { [ -z "$bad" ] || { echo "vendored debs not installed at their vendored version:$bad" >&2; false; }; }
WORKDIR /src
COPY vendored/valkey-src/ .
ARG SOURCE_DATE_EPOCH=1795380563
ENV SOURCE_DATE_EPOCH=${SOURCE_DATE_EPOCH}
ENV BUILD_TLS=yes USE_FAST_FLOAT=yes
RUN make -j"$(nproc)" all BUILD_TLS=yes USE_FAST_FLOAT=yes
RUN make install PREFIX=/opt/valkey BUILD_TLS=yes
RUN set -eu; find /opt/valkey -type f | LC_ALL=C sort | while read -r f; do \
      readelf -h "$f" >/dev/null 2>&1 || continue; \
      readelf -lW "$f" | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; \
      readelf -dW "$f" | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; \
    done | LC_ALL=C sort -u | while read -r lib; do case "$lib" in \
      /*) echo "$lib" ;; *) [ -n "$(find /opt/valkey -name "$lib" -print -quit)" ] || echo "$lib" ;; esac; \
    done > /kitforge.needs && echo "the install prefix loads: $(tr '\n' ' ' < /kitforge.needs)"
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.27.3-bookworm@sha256:972b4110ba0f47539a975c31e52c64765e1ff19f2d74469ae4a595c6676e80a5 AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795380563
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795380563
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'valkey:x:999:999::/data:/bin/sh\n' >> /rootfs/etc/passwd && printf 'valkey:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/data /rootfs/etc/valkey && chown -R 999:999 /rootfs/data /rootfs/etc/valkey
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
COPY valkey.conf /rootfs/etc/valkey/valkey.conf
COPY readystack-entrypoint.sh /rootfs/usr/local/bin/readystack-entrypoint.sh
COPY --from=cbuild /opt/valkey /rootfs/opt/valkey
COPY --from=cbuild /kitforge.needs /tmp/needs/valkey
RUN chmod 755 /rootfs/usr/local/bin/rs-probe && \
    chmod 0755 /rootfs/usr/local/bin/readystack-entrypoint.sh
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795380563
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin PATH=/opt/valkey/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.licenses="BSD-3-Clause"
LABEL org.opencontainers.image.title="Valkey"
LABEL org.opencontainers.image.source="https://github.com/valkey-io/valkey"
LABEL org.opencontainers.image.description="Valkey 9.2.0 in-memory key-value data store (BSD-3-Clause, the Linux Foundation fork of Redis)"
LABEL org.opencontainers.image.version="9.2.0-CE-ubuntu24.04-r2"
LABEL org.opencontainers.image.vendor="ReadyStack.dev"
LABEL readystack.product="valkey"
LABEL readystack.edition="CE"
LABEL readystack.build_method="source-rebuild-c"
LABEL readystack.open_source_note="BSD-3-Clause Linux Foundation fork of Redis (which went SSPL/RSALv2 at 7.4)"
LABEL org.opencontainers.image.revision="d23684e3ec302240754664417e3b99df23e8e4c9"
HEALTHCHECK --interval=5s --timeout=120s --start-period=5s \
  CMD if [ -n "$VALKEY_PASSWORD" ]; then export VALKEYCLI_AUTH="$VALKEY_PASSWORD"; fi; case "$(valkey-cli -h 127.0.0.1 -p 6379 ping)" in PONG) ;; *) exit 1 ;; esac || exit 1
USER valkey
EXPOSE 6379
ENTRYPOINT ["/usr/local/bin/readystack-entrypoint.sh"]
