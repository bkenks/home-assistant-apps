ARG BUILD_FROM=ghcr.io/hassio-addons/base:21.0.10
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

ARG BUILD_ARCH
ARG PANGOLIN_CLI_VERSION=0.21.0
# Stops the embedded self-updater from overwriting the binary at runtime
ENV NEWT_SYSTEM_SUBSTRATE=CONTAINER

RUN \
    case "${BUILD_ARCH}" in \
        aarch64) CLI_ARCH="arm64" ;; \
        amd64)   CLI_ARCH="amd64" ;; \
        *) echo "Unsupported arch: ${BUILD_ARCH}" >&2; exit 1 ;; \
    esac \
    && curl -fsSL -o /usr/bin/pangolin \
        "https://github.com/fosrl/cli/releases/download/${PANGOLIN_CLI_VERSION}/pangolin-cli_linux_${CLI_ARCH}" \
    && chmod a+x /usr/bin/pangolin \
    && pangolin version

# Copy root filesystem
COPY rootfs /

# Build arguments
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
    maintainer="Brian Kenkel <briankenkel.t@gmail.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Brian Kenkel" \
    org.opencontainers.image.authors="Brian Kenkel <briankenkel.t@gmail.com>" \
    org.opencontainers.image.licenses="MIT AND AGPL-3.0-only" \
    org.opencontainers.image.url="https://github.com/bkenks/home-assistant-apps" \
    org.opencontainers.image.source="https://github.com/bkenks/home-assistant-apps" \
    org.opencontainers.image.documentation="https://github.com/bkenks/home-assistant-apps/blob/main/pangolin-site-connector/DOCS.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
