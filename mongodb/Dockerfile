# syntax = docker/dockerfile:1.4
########################################
ARG APPVERSION
########################################

FROM ghcr.io/sergelogvinov/wal-g:2.0.1-mongo AS walg

########################################

FROM registry.k8s.io/pause:3.6 AS pause

########################################

FROM bitnami/mongodb:${APPVERSION}-debian-11-r0 AS pkg
ARG APPVERSION
LABEL org.opencontainers.image.description="Mongodb with utils" \
      org.opencontainers.image.documentation="https://www.mongodb.com" \
      org.opencontainers.image.url="https://github.com/bitnami/containers/tree/main/bitnami/mongodb" \
      org.opencontainers.image.version=${APPVERSION}

COPY --from=pause    ["/pause","/pause"]
COPY --from=walg     ["/usr/local/bin/wal-g","/usr/bin/wal-g"]

########################################

FROM mongo:${APPVERSION} AS official
ARG APPVERSION
LABEL org.opencontainers.image.description="Mongodb official with utils" \
      org.opencontainers.image.documentation="https://www.mongodb.com" \
      org.opencontainers.image.version=${APPVERSION}

COPY --from=pause    ["/pause","/pause"]
COPY --from=walg     ["/usr/local/bin/wal-g","/usr/bin/wal-g"]
