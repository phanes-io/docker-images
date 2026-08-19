FROM debian:12-slim

ARG GO_VERSION=1.26.5
ARG GITLEAKS_VERSION=8.30.1

RUN apt-get update -qq \
    && apt-get install -y -qq --no-install-recommends \
        build-essential \
        git \
        curl \
        ca-certificates \
        gnupg \
    && rm -rf /var/lib/apt/lists/*

# postgresql-client-17 from PGDG: Debian 12 ships client 15, and pg_dump
# refuses to dump a newer server ("aborting because of server version
# mismatch") — the CI database is postgres 17.
RUN curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor -o /usr/share/keyrings/pgdg.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/pgdg.gpg] http://apt.postgresql.org/pub/repos/apt bookworm-pgdg main" > /etc/apt/sources.list.d/pgdg.list \
    && apt-get update -qq \
    && apt-get install -y -qq --no-install-recommends postgresql-client-17 \
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
# mtxdns-dashboard's check.yml seeds its CI database with psql/pg_isready
RUN pg_isready --version && pg_dump --version | grep -q " 17\." 
