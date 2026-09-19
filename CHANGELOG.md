# Changelog

Notable changes to the RemoteHost CLI. Versions follow the npm package
[`@remotehost/cli`](https://www.npmjs.com/package/@remotehost/cli).

## 0.1.3 — 2026-09-19

- `remote` is the command the CLI prints everywhere; `rh` remains a short alias.
- Dropped the `remotehost` bin alias. It collided with the desktop app's own launcher at /usr/local/bin/remotehost, where whichever installed last decided what the name ran.

## 0.1.2 — 2026-09-16

- `remote --version` now reports the version that was actually published; 0.1.1 identified itself as 0.1.0.

## 0.1.1 — 2026-09-15

- Document the `--json` flag and its output contract.
- First release published through CI rather than by hand.

## Unreleased

### Added
- First npm release. The CLI installs with `npm i -g @remotehost/cli` and ships
  as a single bundled file with no runtime dependencies.
- `remote` is the command, with `rh` and `remotehost` kept as aliases so anyone
  who learned either name is not broken by the change.

### Changed
- Installing no longer builds from source. The previous installer cloned a
  repository and ran a build on your machine, which needed git, corepack and
  pnpm; none of that is required now.
