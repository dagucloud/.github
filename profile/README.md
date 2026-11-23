<p align="center">
  <a href="https://dagu.sh">
    <img src="https://raw.githubusercontent.com/dagucloud/dagu/main/assets/images/hero-logo.png" width="720" alt="Dagu: built for teams whose main work is not orchestration">
  </a>
</p>

<p align="center">
  <a href="https://dagu.sh">Website</a> ·
  <a href="https://docs.dagu.sh">Docs</a> ·
  <a href="https://dagu-demo-f5e33d0e.dagu.sh">Live demo</a> <code>demouser / demouser</code> ·
  <a href="https://dagu.sh/recipes">Recipes</a> ·
  <a href="https://discord.gg/gpahPUjGRk">Discord</a>
</p>

Dagu is a local-first workflow engine for operations and internal automation. Workflows are declarative YAML DAGs that run existing shell commands, Docker containers, Kubernetes Jobs, and remote commands over SSH. It ships as one binary with a built-in Web UI and needs no external database or message broker.

```yaml
schedule: "0 2 * * *"
steps:
  - id: extract
    run: ./extract.sh
    retry_policy:
      limit: 3
      interval_sec: 60
  - id: summarize
    action: duckdb@v1
    with:
      query: SELECT count(*) FROM 'out/*.parquet'
```

### Install

```sh
# macOS / Linux
curl -fsSL https://raw.githubusercontent.com/dagucloud/dagu/main/scripts/installer.sh | bash

# Homebrew
brew install dagu

# Windows (PowerShell)
irm https://raw.githubusercontent.com/dagucloud/dagu/main/scripts/installer.ps1 | iex
```

npm, Scoop, Docker, and Helm are covered in the [installation guide](https://docs.dagu.sh/getting-started/installation/).

### Repositories

| Repository | Contents |
|---|---|
| [dagu](https://github.com/dagucloud/dagu) | Engine, CLI, Web UI, scheduler, coordinator, and workers in one binary |
| [docs](https://github.com/dagucloud/docs) | Source for [docs.dagu.sh](https://docs.dagu.sh) |
| [recipes](https://github.com/dagucloud/recipes) | Validated workflow recipes, browsable at [dagu.sh/recipes](https://dagu.sh/recipes) |

### Official actions

`action: <name>@v1` resolves to `dagucloud/<name>`. Each action declares and pins its own tools, so worker images stay unchanged. See the [actions reference](https://docs.dagu.sh/dagu-actions/official).

| Action | Runs |
|---|---|
| [python-script](https://github.com/dagucloud/python-script) | Python with a pinned runtime and optional requirements |
| [node-script](https://github.com/dagucloud/node-script) | JavaScript with a pinned Node.js runtime |
| [dbt](https://github.com/dagucloud/dbt) | dbt Core commands with project-local adapters |
| [duckdb](https://github.com/dagucloud/duckdb) | Analytical SQL through the DuckDB CLI |
| [ffmpeg](https://github.com/dagucloud/ffmpeg) | Media conversion and probing with a pinned FFmpeg |
| [github-cli](https://github.com/dagucloud/github-cli) | Repository, release, and API automation with `gh` |
| [rclone](https://github.com/dagucloud/rclone) | Copy, sync, and check files across rclone storage backends |

### Community

- Questions: [Discord](https://discord.gg/gpahPUjGRk)
- Bugs and feature requests: [Issues](https://github.com/dagucloud/dagu/issues)
- Security reports: [private advisory](https://github.com/dagucloud/dagu/security)
- Updates: [Bluesky](https://bsky.app/profile/dagu-sh.bsky.social)
