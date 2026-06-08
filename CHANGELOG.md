# Changelog

All notable changes to `@kiqr/cli` are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `kiqr open mail` — outgoing WordPress email is captured by a Mailpit service
  in the kiqr agent and viewable at `http://mail.lvh.me:5477`. Development-only,
  routed via the mu-plugin's `phpmailer_init` hook.
- `kiqr share` — expose your running local site at a public Cloudflare quick
  tunnel URL, with WordPress URL handling so links/assets resolve correctly.
- `kiqr agent` — the shared proxy + splash are now a persistent background
  service with `start` / `stop` / `restart` / `status` / `logs` subcommands.
- `kiqr doctor` — preflight environment check (Docker installed/running, ports
  free, WSL detection).
- `kiqr status` — show whether the project is running and where to reach it.
- `kiqr seed` — generate realistic demo content (blog / portfolio / woocommerce)
  as a WordPress import file.
- `kiqr completion <bash|zsh|fish>` — shell tab-completion scripts.
- WordPress + PHP version validation against Docker Hub before `kiqr up` pulls
  an image, with a clear message listing the available PHP versions.
- The configured `wordpress.php_version` is now applied to the WordPress image.
- `kiqr.yaml` / `config.yaml` are validated with zod schemas, surfacing clear
  errors instead of cryptic crashes.

### Changed

- Local project hostnames are simplified to `<slug>.lvh.me` (dropped the
  machine-name segment).
- Adopted Biome for linting/formatting, wired into CI.
- Pinned infrastructure Docker image versions (mariadb, phpmyadmin, nginx).

### Fixed

- File watching now uses chokidar for reliable cross-platform (incl. nested
  directory) change detection.
- Commands handle an invalid `kiqr.yaml` gracefully instead of crashing.
- `kiqr wp` / `kiqr db` invoke WP-CLI with `--profile cli` and pass arguments
  shell-free so quoted values survive.
- `kiqr db restore` no longer risks a stdout pipe deadlock.
- Docker Compose failures now surface the underlying error instead of a blank
  failed step.

## [0.1.1]

- Initial published release: local WordPress theme development via Docker
  (`up` / `down` / `restart` / `watch` / `init` / `info` / `open` / `logs` /
  `wp` / `db` / `destroy`), Traefik routing, and lvh.me hostnames.
