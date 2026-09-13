# RemoteHost CLI

Create sandboxes, attach to them, and manage a fleet without leaving the terminal.

```sh
npm i -g @remotehost/cli
remote login
```

The install puts three names on your PATH — `remote`, with `rh` and `remotehost`
as aliases — all the same program.

## Getting started

```sh
remote new claude          # a sandbox with Claude Code booting inside it
remote ls                  # what is running
remote attach <name>       # drop into one
remote sleep <name>        # stop paying for it, keep the disk
```

Run `remote` on its own to open the TUI, the interactive version of all of the above.

## Authentication

`remote login` opens a browser and approves this machine. For CI and agents,
create a key with `remote keys create` and set `REMOTEHOST_TOKEN` instead.

## Configuration

| variable | what it does |
| --- | --- |
| `REMOTEHOST_TOKEN` | API key, for non-interactive use |
| `REMOTEHOST_API_URL` | point the CLI at a different API |
| `REMOTEHOST_CONFIG_DIR` | where the login session is stored |

## Requirements

Node.js 22 or newer. Nothing else — the package is a single bundled file with no
runtime dependencies.

## About this repository

This is the home for the CLI's documentation, releases and issues. The CLI is
distributed through npm as `@remotehost/cli`; its source is not published here.

- **Report a bug or request a feature:** [open an issue](https://github.com/remotehostai/cli/issues)
- **Release notes:** [CHANGELOG.md](./CHANGELOG.md)
- **Product docs:** https://remotehost.ai

## Licence

© RemoteHost, Inc. All rights reserved. Use is subject to RemoteHost's
[Terms of Service](https://remotehost.ai/terms). See [LICENSE.md](./LICENSE.md).
