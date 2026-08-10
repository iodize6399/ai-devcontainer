# AI Coding Agents Dev Container

A simple GitHub template for using Codex, opencode, and Oh My Pi in a dev container.

After building the container, run any agent from the terminal:

```sh
codex
opencode
omp
```

## Persistent configuration

Authentication, configuration, and session data survive container rebuilds:

| Agent | Host directory | Container directory |
| --- | --- | --- |
| Codex | `~/.codex` | `/var/lib/codex` (linked from `~/.codex`) |
| opencode | `~/.local/share/opencode` and `~/.config/opencode` | `/var/lib/opencode` and `/var/lib/opencode-config` (linked from `~/.local/share/opencode` and `~/.config/opencode`) |
| Oh My Pi | `~/.omp` | `/var/lib/omp` (linked from `~/.omp`) |

The host directories are created before the container starts and bind-mounted to a neutral path under `/var/lib/`. Each tool's dot-directory in the container user's home is then symlinked to its `/var/lib/<name>` counterpart so the tool finds its state where it expects. The bind mounts and symlinks are owned by the respective sliekens devcontainer features.

## Update the agents

```sh
npx --yes @devcontainers/cli upgrade --workspace-folder .
```

Rebuild the container after updating.

### Pinning Oh My Pi

Oh My Pi is installed from upstream `can1357/oh-my-pi` GitHub releases by `ghcr.io/sliekens/devcontainer-features/omp:1`. Pin its version with the feature's `version` option in `.devcontainer/devcontainer.json`, e.g. `"version": "17.2.9"` or `"version": "v17.2.9"`. The default is `latest`.

The universal base image includes Node.js, satisfying the feature's peer-runtime requirement for the full Oh My Pi harness.

# Using in WSL

1. Store repositories under `~/projects` in WSL.
2. Put this `.devcontainer/devcontainer.json` in each repository.
3. Open the repository with VS Code.
4. Select `Dev Containers: Reopen in Container.`
5. Run `codex`, `opencode`, or `omp` from the container terminal.
