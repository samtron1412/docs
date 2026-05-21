# Overview

- https://mise.jdx.dev/
- https://mise.jdx.dev/about.html
    + Install and manage dev tools / runtimes
        * Core tools: https://mise.jdx.dev/core-tools.html
        * Backends: https://mise.jdx.dev/dev-tools/backends/
        * Supported tools: https://mise.jdx.dev/registry.html
    + Manage environment variables per projects.
        * https://mise.jdx.dev/environments/
    + Task runner to share common tasks within a project.
        * https://mise.jdx.dev/tasks/
        * make tool with Makefile might be more mature than this one.

# CLI

## self-update

- https://mise.jdx.dev/cli/self-update.html
- `mise self-update [flags] [version]`
- Updates mise itself.
- Uses the GitHub Releases API to find the latest release and binary. By
  default, this will also update any installed plugins. Uses mise's
  GitHub token resolution chain for authenticated requests.
- This command is not available if mise is installed via a package
  manager (brew, apt-get, etc.).

## use

- https://mise.jdx.dev/cli/use.html
- `mise use [flags] [tool@version]...`

### [tool@version]...

### Flags

- `-g --global`
- Use the global config file (`~/.config/mise/config.toml`) instead of
  the local one
