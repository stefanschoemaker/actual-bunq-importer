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

### Fixed
- `--init-accounts` and syncs crashed (`TypeError: cafile, capath and cadata cannot be all
  omitted`) when `config.json` was created via the web UI, which doesn't write `actual.cert`
- Syncs crashed with `KeyError: 'state_file'` for the same reason; it now defaults to
  `data/sync_state.json`
- Full syncs of accounts with many payments failed with `413 Payload Too Large`: all
  transactions went to Actual in one sync request (~1.25 MB per 1000), over the server's
  20 MB default. They are now committed in batches of 1000
- After a failed commit, the local budget copy kept the unsent transactions, so the next run
  skipped them as duplicates and they never reached Actual. The copy is now discarded on failure
- Changing the schedule or the sync toggle in the web UI had no effect until a restart: `pkill`
  isn't in the image, and its SIGHUP would have stopped supercronic. It now gets SIGUSR2 (reload)

## [0.1.1] - 2026-03-26
### Fixed
- Incremental sync blocked by since_date from config
- Missing cleared flag on transfer transactions

### Added
- salary_detector.py for auto-transfer labeling

## [0.1.0] - 2026-03-24
### Added
- Initial release
