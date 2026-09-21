# RemoteHost CLI

Create sandboxes, attach to them, and manage a fleet without leaving the
terminal.

```sh
npm i -g @remotehost/cli
remote login
```

The command is `remote`.

## Getting started

```sh
remote new claude          # a sandbox with Claude Code booting inside it
remote ls                  # what is running
remote attach <name>       # drop into one
remote sleep <name>        # stop paying for it, keep the disk
```

Run `remote` on its own to open the TUI, which is the interactive version of all
of the above.

In the sandbox table, **Space** toggles the highlighted row, **Shift+Up/Down**
selects a range, **Ctrl+A** selects all matching rows, and **a** toggles all.
**Esc** clears the selection. Use **/** to filter; Space and **a** type into
the filter while it is focused. Selections follow sandbox IDs across refreshes
and clear when rows are filtered out or you leave the project.

With rows selected, **Enter**, **s**, or **Ctrl+G** opens actions for the selection:
Sleep, Wake, Renew, and Delete. Each action shows its eligible sandbox count;
for example, Sleep applies to running persistent sandboxes and Renew applies to
running ephemeral sandboxes. Delete lists its targets and requires **y** to
confirm. Results report successes and failures, leaving failed rows selected
for retry.

Type while the command menu is open to filter its actions. Use **Up/Down** to
move through matches, **Enter** to run, **Backspace** to edit, and **Esc** or
**Ctrl+G** to close. The filter resets each time the menu opens.

## Scripting

Every command that reports data takes `--json`, which is the flag to reach for
from a script or an SDK rather than parsing the table:

```sh
remote ls --json | jq '.[] | select(.status == "running") | .name'
remote new claude --name checkout --json
```

The contract is narrow on purpose:

- **stdout** carries exactly one JSON document, or nothing. A list command emits
  an array — empty when there is nothing, never the words "No sandboxes found."
  A single-subject command emits an object.
- **stderr** carries every diagnostic, including a `{"error": {...}}` document
  when a command fails. Nothing that is not the result reaches stdout.
- **the exit code** is 0 on success and 1 on failure, so you can decide which
  stream to parse before parsing it.

The tab-separated output is unchanged and is not going away. It is a good thing
to read and a poor thing to parse: values contain spaces, and every number
arrives as text with its unit attached.

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

Node.js 22 or newer. No other runtime dependencies — the package is a single
bundled file.

Because it is bundled, the open-source packages it depends on are compiled into
that file rather than installed beside it. Their licences and copyright notices
are reproduced in full in `THIRD-PARTY-NOTICES.md`, which ships with the
package.

## Issues and docs

- Issues: https://github.com/remotehostai/cli/issues
- Docs: https://remotehost.ai/docs

## Local development

`remote-staging` runs `packages/cli/src/index-staging.ts` from the local root
checkout through `tsx`, against `https://api-staging.remotehost.ai`. CLI source
edits take effect on the next launch without copying a bundle. Staging keeps its
own login session. `remote-staging-update` rebuilds local workspace dependencies.

`remote` is the npm registry installation of `@remotehost/cli`; keep it separate
from local builds and workspace links.
