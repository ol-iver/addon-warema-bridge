ARG BUILD_FROM=alpine:3.22.1
FROM ${BUILD_FROM}

# Setup base
RUN apk add --no-cache npm

# Copy root filesystem
COPY rootfs/srv /srv

WORKDIR /srv

RUN apk add --no-cache --virtual .build-deps python3 make g++ linux-headers \
    && npm ci --omit=dev && npm rebuild --build-from-source\
    && apk del --no-cache --purge .build-deps \
    && rm -rf /root/.npm /root/.cache

ENTRYPOINT ["node", "/srv/bridge.js"]
