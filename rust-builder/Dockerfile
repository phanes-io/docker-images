FROM debian:12-slim

RUN apt-get update -qq \
    && apt-get install -y -qq --no-install-recommends \
        build-essential \
        pkg-config \
        libssl-dev \
        cmake \
        git \
        curl \
        ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Install Rust stable
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && /root/.cargo/bin/rustup component add rustfmt clippy

ENV PATH="/root/.cargo/bin:${PATH}"

# Verify installation
RUN rustc --version && cargo --version && rustfmt --version && cargo clippy --version
