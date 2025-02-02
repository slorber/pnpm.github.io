---
id: recursive
title: pnpm recursive
---

Runs a pnpm command recursively on all subdirectories in the package or every
available workspace. Currently, only the following commands can be used
recursively: `add`, `exec`, `install`, `list`, `outdated`, `publish`, `rebuild`,
`remove`, `run`, `test`, `unlink`, `update`, `why`

Aliases: `m`, `multi`, `<command> -r`

## Options

### --link-workspace-packages

* Default: **true**
* Type: **true, false, deep**

Link locally available packages in workspaces of a monorepo into `node_modules`
instead of re-downloading them from the registry. This emulates functionality
similar to `yarn workspaces`.

When this is set to deep, local packages can also be linked to subdependencies.

Be advised that it is encouraged instead to use [npmrc] for this setting, to
enforce the same behaviour in all environments. This option exists solely so you
may override that if necessary.

[npmrc]: ../workspaces#link-workspace-packages

### --workspace-concurrency

Added in: v2.13.0

* Default: **4**
* Type: **Number**

Set the maximum number of tasks to run simultaneously. For unlimited concurrency
use `Infinity`.

### --[no-]bail

Added in: v2.13.0

* Default: **true**
* Type: **Boolean**

If true, stops when a task throws an error.

This config does not affect the exit code.
Even if `--no-bail` is used, all tasks will finish but if any of the tasks fail,
the command will exit with a non-zero code.

Example (run tests in every package, continue if tests fail in one of them):
```sh
pnpm -r --no-bail test
```

### --[no-]sort

Added in: v2.14.0

* Default: **true**
* Type: **Boolean**

When `true`, packages are sorted topologically (dependencies before dependents).
Pass `--no-sort` to disable.

Example:
```sh
pnpm -r --no-sort test
```

### --reverse

Added in: v5.17.1

* Default: **false**
* Type: **boolean**

When `true`, the order of packages is reversed.

```
pnpm -r --reverse run clean
```

## pnpm -r exec

Added in: v2.9.0

```sh
pnpm -r exec -- <command> [args...]
```

This command runs a command in each package of the monorepo.

The name of the current package is available through the environment variable
`PNPM_PACKAGE_NAME` (supported from pnpm v2.22.0 onwards).

Examples:
```sh
# prune node_modules installations for all packages
pnpm -r exec -- rm -rf node_modules
# view package information for all packages
pnpm -r exec -- pnpm view $PNPM_PACKAGE_NAME
```

### --filter &lt;package_selector\>

[Read more about filtering.](../filtering)
