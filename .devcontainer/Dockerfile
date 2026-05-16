FROM debian:bookworm-slim

COPY install.sh /app/install.sh

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends \
    bash git curl wget unzip tzdata openssl ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN chmod +x /app/install.sh && /app/install.sh
COPY config.json /etc/config.json

# Update the echo command to output a WebSocket (ws) link with correct host headers
RUN echo 'echo -e "\n✅ VLESS LINK:\nvless://550e8400-e29b-41d4-a716-446655440000@94.130.50.12:443?encryption=none&security=tls&type=ws&host=${CODESPACE_NAME}-443.app.github.dev&sni=${CODESPACE_NAME}-443.app.github.dev&path=%2Fsecure-ws-tunnel#ghtun-WS"' >> /etc/bash.bashrc

CMD ["/usr/local/bin/xray", "-c", "/etc/config.json"]
