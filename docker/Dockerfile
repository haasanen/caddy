# Caddy built FROM THIS FORK'S TREE (upstream-sync CI merges caddyserver/caddy
# release tags into master), plus the porkbun DNS module pinned from upstream.
# Publishes ghcr.io/haasanen/caddy:<caddy-version>. Versions come from
# docker/version.lock via CI --build-arg.
ARG CADDY_VERSION=2.11.7
FROM docker.io/library/caddy:${CADDY_VERSION}-builder AS builder
COPY . /src/caddy
ARG PORKBUN_VERSION=v0.3.1
RUN xcaddy build ${CADDY_VERSION} \
    --replace github.com/caddyserver/caddy/v2=/src/caddy \
    --with github.com/caddy-dns/porkbun@${PORKBUN_VERSION}

FROM docker.io/library/caddy:${CADDY_VERSION}-alpine
COPY --from=builder /usr/bin/caddy /usr/bin/caddy
