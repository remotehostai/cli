# Changelog

## 1.0.1 — 2026-11-03

### Patch Changes

- `remote sleep` waits for the sandbox's snapshot to finish saving, for up to three minutes, and prints the sandbox once it is asleep (`stopped`), so a `remote wake` straight after no longer meets the save. Past three minutes it prints the sandbox as `saving`, says the save is still going and that `remote wake` waits for it, and exits 0: the sandbox is asleep either way. `--json` prints the final state the same way.
- `remote login` with no terminal (stdin not a TTY, as in an agent's shell, a pipe or CI) prints the link and code and waits for the browser, also on a machine that is already signed in. It already did in 1.0.0; this release adds the test for signing in again.

## 1.0.0 — 2026-11-02

### Major Changes

- First release on a fresh npm name. Every 0.x version of `@remotehost/cli` was unpublished from npm on 2026-11-01 and the old `remotehostai/cli` repository deleted, so 1.0.0 is the first version npm serves. It is 0.3.0 renumbered: no command, flag or output changes.

