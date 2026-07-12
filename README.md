# Codex Dev Container

A simple GitHub template for using Codex in a dev container.

## Update Codex

```sh
npx --yes @devcontainers/cli upgrade --workspace-folder .
```

Rebuild the container after updating.

# Using in WSL

1. Store repositories under ~/projects in WSL.
2. Put this .devcontainer/devcontainer.json in each repository.
3. Open the repository with VS Code.
4. Select Dev Containers: Reopen in Container.
5. Run codex from the container terminal.