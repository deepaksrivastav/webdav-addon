ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base:6.2.5
###############################################################################
# Use caddy builder to build caddy with custom modules
###############################################################################
FROM caddy:2.6.4-builder AS builder

## Build caddy with webdav module
RUN xcaddy build --with github.com/mholt/caddy-webdav

###############################################################################
# Build the actual add-on.
###############################################################################
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Get the caddy binary from the official image
COPY --from=builder /usr/bin/caddy /usr/bin/caddy

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="deepaksrivastav (https://github.com/deepaksrivastav/webdav-addon)" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-ons" \
    org.opencontainers.image.authors="deepaksrivastav (https://github.com/deepaksrivastav/webdav-addon)" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/deepaksrivastav/webdav-addon" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}