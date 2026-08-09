# docker-images

Shared Docker base images for phanes-io CI/CD pipelines.

## Images

### rust-builder

Debian 12 (Bookworm) with Rust stable + build tools for CI/CD.

```
ghcr.io/phanes-io/rust-builder:bookworm
```

Includes: `build-essential`, `pkg-config`, `libssl-dev`, `cmake`, `git`, `rustfmt`, `clippy`

Built weekly (Sunday 4am UTC) and on push to master.

### go-builder

Debian 12 (Bookworm) with Go + gitleaks for CI/CD (used by mtxdns-dashboard).

```
ghcr.io/phanes-io/go-builder:bookworm
```

Includes: Go 1.26.5, gitleaks 8.30.1, `build-essential`, `git`

Built weekly (Sunday 4am UTC) and on push to master.
