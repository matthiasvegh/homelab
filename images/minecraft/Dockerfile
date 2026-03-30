FROM eclipse-temurin:25-jre-noble

ENV SERVER_URL="https://piston-data.mojang.com/v1/objects/3872a7f07a1a595e651aef8b058dfc2bb3772f46/server.jar"
LABEL MINECRAFT_VERSION="26.1"
LABEL org.opencontainers.image.source=https://github.com/matthiasvegh/homelab
LABEL org.opencontainers.image.description="Minecraft Server"

EXPOSE 25565

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install --yes --no-install-recommends wget ca-certificates catatonit && \
    wget "${SERVER_URL}" -O /minecraft_server.jar && \
    apt-get remove --yes wget && \
    apt-get autoremove --yes && \
    rm -rf /var/cache/apt/archives /var/lib/apt/lists/* && \
    echo "eula=TRUE" > /eula.txt

ENTRYPOINT ["catatonit", "-g", "--"]
ENV HEAP_START="-Xms4096M"
ENV HEAP_MAX="-Xmx4096M"

CMD exec java -jar $HEAP_START $HEAP_MAX -jar /minecraft_server.jar --nogui
