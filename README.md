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

The host directories are created before the container starts and bind-mounted to a neutral path under `/var/lib/`. Each tool's dot-directory in the container user's home is then symlinked to its `/var/lib/<name>` counterpart so the tool finds its state where it expects. The same pattern is used for all three agents; for Codex and opencode the bind mount and symlink are owned by their respective sliekens devcontainer features, while for Oh My Pi they are owned by this repo (`devcontainer.json` and `.devcontainer/setup-oh-my-pi-state.sh`).

## Update the agents

```sh
npx --yes @devcontainers/cli upgrade --workspace-folder .
```

Rebuild the container after updating.

### Pinning Oh My Pi

Oh My Pi is installed from upstream `can1357/oh-my-pi` GitHub releases by `.devcontainer/install-omp.sh` during container creation. Pin a version by setting `OMP_VERSION` in `.devcontainer/devcontainer.json` (`containerEnv`), e.g. `"OMP_VERSION": "16.4.6"` or `"OMP_VERSION": "v16.4.6"`. The default is `latest`.

# Using in WSL

1. Store repositories under `~/projects` in WSL.
2. Put this `.devcontainer/devcontainer.json` in each repository.
3. Open the repository with VS Code.
4. Select `Dev Containers: Reopen in Container.`
5. Run `codex`, `opencode`, or `omp` from the container terminal.
