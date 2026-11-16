<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/icon.svg">
    <img src="assets/icon.svg" alt="Trilium Notes logo" width="128">
  </picture>
</p>

<h1 align="center">aac-trilium</h1>

<p align="center">Self-hosted deployment definition for Trilium Notes, a hierarchical note-taking application and personal knowledge base.</p>

<p align="center">
  <a href="https://github.com/TriliumNext/Trilium"><img alt="Upstream" src="https://img.shields.io/badge/upstream-TriliumNext%2FTrilium-blue?logo=github"></a>
  <img alt="Image" src="https://img.shields.io/badge/image-triliumnext%2Ftrilium%3Av0.106.1-2496ED?logo=docker&logoColor=white">
  <a href="https://github.com/TriliumNext/Trilium/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/license-AGPL--3.0-green"></a>
</p>

## About

Trilium Notes is a hierarchical note-taking application for building a personal knowledge base.
Notes can be arranged in a tree, linked to each other and enriched with different note types
(text, code, files, images and more). The application runs as a single Node.js server with a
web interface, and all data is kept in a local data directory.

Key features (as provided by upstream):

- Hierarchical note tree with cross-links between notes
- Rich-text and code notes, file and image attachments
- Full-text search across the note collection
- Web interface with optional sync between instances
- Encrypted note protection (password-protected notes)

## Upstream

- Project: <https://github.com/TriliumNext/Trilium>
- Documentation: <https://docs.triliumnotes.org>
- Container image: `triliumnext/trilium:v0.106.1` (Docker Hub)
- License: AGPL-3.0 (upstream project)

## Quick start (Docker Compose)

The Compose file is rendered from `service.yml` by the App-as-Code template engine; this
repository does not contain a hand-written Compose file. The service needs no secrets, so no
`.env` file is required.

```bash
# Render the manifests from service.yml with aac-template-engine, then in the rendered directory:
docker compose up -d
```

## Configuration

Environment variables (from `service.yml`; all values are fixed defaults, no secrets are used):

| Variable | Default | Description |
|---|---|---|
| `PUID` | `1000` | User ID the container runs as |
| `PGID` | `1000` | Group ID the container runs as |
| `USER_UID` | `1000` | User ID used by the application user |
| `USER_GID` | `1000` | Group ID used by the application user |
| `TZ` | `Europe/Berlin` | Time zone |

Ports:

| Port | Protocol | Purpose |
|---|---|---|
| `8080` | TCP | Web interface (`web`); external port `8181` as declared in `service.yml` |

Volumes:

| Mount | Description |
|---|---|
| `data` -> `/home/node/trilium-data` | Trilium Notes data directory (host path under `/export/docker`) |

## Deploy with App-as-Code

1. Edit `service.yml`. It is the single source of truth for image, ports, environment,
   volumes, integrations and per-stage overrides. Do not edit the rendered output.
2. Pushing to `main` (or a configured stage branch) runs the service pipeline, which renders
   the manifests with `aac-template-engine` and triggers the deployment.
3. Releases of this definition are published under <https://github.com/app-as-code/aac-trilium>.

## Credits and license

Trilium Notes is developed by the TriliumNext project and licensed under AGPL-3.0. This
repository only contains the deployment definition for it and is not a fork of the
application. The logo is provided through the homarr-labs dashboard icon collection; see
[`assets/ICON_SOURCE.md`](assets/ICON_SOURCE.md) for icon sources and licenses.
