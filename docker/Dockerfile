FROM soulter/astrbot:latest

USER root
ARG TARGETARCH
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    gnupg \
    fonts-noto-cjk \
    fonts-liberation \
    libasound2 \
    libatk-bridge2.0-0 \
    libatk1.0-0 \
    libc6 \
    libcairo2 \
    libcups2 \
    libdbus-1-3 \
    libexpat1 \
    libfontconfig1 \
    libgbm1 \
    libgcc1 \
    libglib2.0-0 \
    libgtk-3-0 \
    libnspr4 \
    libnss3 \
    libpango-1.0-0 \
    libpangocairo-1.0-0 \
    libstdc++6 \
    libx11-6 \
    libx11-xcb1 \
    libxcb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxi6 \
    libxrandr2 \
    libxrender1 \
    libxss1 \
    libxtst6 \
    xdg-utils \
    && rm -rf /var/lib/apt/lists/*

RUN set -eux; \
    if [ "${TARGETARCH}" = "amd64" ]; then \
      curl -fsSL https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor -o /usr/share/keyrings/google-linux.gpg; \
      echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-linux.gpg] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list; \
      apt-get update; \
      apt-get install -y --no-install-recommends google-chrome-stable; \
      ln -sf /usr/bin/google-chrome /usr/local/bin/steamshot-browser; \
    elif [ "${TARGETARCH}" = "arm64" ]; then \
      apt-get update; \
      apt-get install -y --no-install-recommends chromium chromium-driver; \
      ln -sf /usr/bin/chromium /usr/local/bin/steamshot-browser; \
    else \
      echo "Unsupported TARGETARCH: ${TARGETARCH}"; \
      exit 1; \
    fi; \
    rm -rf /var/lib/apt/lists/*

ENV STEAMSHOT_BROWSER_BIN=/usr/local/bin/steamshot-browser
ENV STEAMSHOT_BROWSER_KIND=auto
ENV STEAMSHOT_SKIP_WDM=0
