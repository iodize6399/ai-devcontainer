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
| Codex | `~/.codex` | `~/.codex` |
| opencode | `~/.local/share/opencode` and `~/.config/opencode` | `~/.local/share/opencode` and `~/.config/opencode` |
| Oh My Pi | `~/.omp` | `/var/lib/omp` (linked from `~/.omp`) |

The host directories are created before the container starts and bind-mounted into the container. Oh My Pi's mounted state is linked to the container user's home when the container is first created.

## Update the agents

```sh
npx --yes @devcontainers/cli upgrade --workspace-folder .
```

Rebuild the container after updating.

# Using in WSL

1. Store repositories under `~/projects` in WSL.
2. Put this `.devcontainer/devcontainer.json` in each repository.
3. Open the repository with VS Code.
4. Select `Dev Containers: Reopen in Container.`
5. Run `codex`, `opencode`, or `omp` from the container terminal.
