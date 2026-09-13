# Changelog

Notable changes to the RemoteHost CLI. Versions follow the npm package
[`@remotehost/cli`](https://www.npmjs.com/package/@remotehost/cli).

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
