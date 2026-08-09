# docker-images

Shared Docker base images for phanes-io CI/CD pipelines.

## Images

### rust-builder

Debian 12 (Bookworm) with Rust stable + build tools for CI/CD.

```
registry.local.phanes.net/phanes-io/rust-builder:bookworm
```

Includes: `build-essential`, `pkg-config`, `libssl-dev`, `cmake`, `git`, `rustfmt`, `clippy`

Built by Woodpecker on push to master, into the local Harbor.

### go-builder

Debian 12 (Bookworm) with Go + gitleaks for CI/CD (used by mtxdns-dashboard).

```
registry.local.phanes.net/phanes-io/go-builder:bookworm
```

Includes: Go 1.26.5, gitleaks 8.30.1, `build-essential`, `git`

Built by Woodpecker on push to master, into the local Harbor.
