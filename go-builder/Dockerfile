FROM debian:12-slim

ARG GO_VERSION=1.26.5
ARG GITLEAKS_VERSION=8.30.1

RUN apt-get update -qq \
    && apt-get install -y -qq --no-install-recommends \
        build-essential \
        git \
        curl \
        ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Install Go
RUN curl -fsSL "https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz" \
        | tar -xz -C /usr/local

# Install gitleaks (runs in CI on every push, see mtxdns-dashboard .woodpecker/check.yml)
RUN curl -fsSL "https://github.com/gitleaks/gitleaks/releases/download/v${GITLEAKS_VERSION}/gitleaks_${GITLEAKS_VERSION}_linux_x64.tar.gz" \
        | tar -xz -C /usr/local/bin gitleaks

ENV PATH="/usr/local/go/bin:/root/go/bin:${PATH}"

# Verify installation
RUN go version && gofmt --help >/dev/null 2>&1 || true
RUN gitleaks version
