# Changelog

All notable changes to this project will be documented here.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]
### Added
- Docker image builds on arm64 as well as amd64 (supercronic binary per platform, checksum-verified)
- Optional HTTP basic auth for the web UI via `WEB_USERNAME` / `WEB_PASSWORD`
- Cross-site request protection: state-changing requests from other origins are rejected (403)
- `.dockerignore` so `config/config.json`, data and logs are never copied into the image

### Changed
- `docker-compose.yml`: removed the hard-coded DNS server, `TZ` is configurable, the
  templates live-edit mount is commented out (development only)

## [0.1.1] - 2026-03-26
### Fixed
- Incremental sync blocked by since_date from config
- Missing cleared flag on transfer transactions

### Added
- salary_detector.py for auto-transfer labeling

## [0.1.0] - 2026-03-24
### Added
- Initial release
