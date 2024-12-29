FROM        --platform=$TARGETOS/$TARGETARCH node:20-alpine

LABEL       author="Nikolas Trochalakis" maintainer="nick@calliecorner.net"

RUN         apk update \
                && apk add --no-cache ffmpeg iproute2 bash git sqlite sqlite-dev python3 python3-dev ca-certificates bind-tools tzdata zip tar curl build-base libtool iputils nss tini \
                && adduser -D -h /home/container container


RUN         npm install npm@latest typescript ts-node @types/node --location=global

# install pnpm
RUN         npm install -g corepack
RUN         corepack enable
RUN         corepack prepare pnpm@latest --activate

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]