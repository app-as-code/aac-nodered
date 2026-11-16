<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/icon-dark.svg">
    <img src="assets/icon.svg" alt="Node-RED logo" width="128">
  </picture>
</p>

<h1 align="center">aac-nodered</h1>

<p align="center">Self-hosted deployment definition for Node-RED, a flow-based programming tool for event-driven automation.</p>

<p align="center">
  <a href="https://github.com/node-red/node-red"><img alt="Upstream" src="https://img.shields.io/badge/upstream-node--red%2Fnode--red-blue?logo=github"></a>
  <img alt="Image" src="https://img.shields.io/badge/image-nodered%2Fnode--red%3A5.0--debian-2496ED?logo=docker&logoColor=white">
  <a href="https://github.com/node-red/node-red/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/badge/license-Apache--2.0-green"></a>
</p>

## About

Node-RED is a browser-based tool for wiring together devices, APIs and online services. Logic is
built as flows of connected nodes in a visual editor, which makes it well suited to home
automation, IoT glue code and simple data pipelines. Flows are stored as JSON and can be
exported, imported and shared.

Key features (as provided by upstream):

- Visual flow editor in the browser with a large library of nodes
- Event-driven runtime for MQTT, HTTP, WebSocket and many other protocols
- Function nodes for custom JavaScript where the palette is not enough
- Package manager for installing additional nodes from npm
- Flows, settings and installed nodes persisted in a data directory

## Upstream

- Project: <https://github.com/node-red/node-red>
- Website and documentation: <https://nodered.org/docs/>
- Container image: `nodered/node-red:5.0-debian` (Docker Hub)
- License: Apache-2.0 (upstream project)

## Quick start (Docker Compose)

The Compose file is rendered from `service.yml` by the App-as-Code template engine. For a
manual run, the external networks used for routing must exist first:

```bash
docker network create services-secured
docker network create services-exposed
# The network "docker-default" is also referenced as external and must exist.

docker compose up -d
```

The deployment needs no secrets. The user, group and time zone settings can be provided
through `.env` (see Configuration).

## Configuration

Environment variables (defaults from `service.yml`):

| Variable | Default | Description |
|---|---|---|
| `PUID` | `1000` | User ID the container runs as |
| `PGID` | `1000` | Group ID the container runs as |
| `TZ` | `Europe/Berlin` | Time zone |

Ports:

| Port | Protocol | Purpose |
|---|---|---|
| `1880` | TCP | Node-RED editor and runtime (`web`) |

Volumes:

| Mount | Description |
|---|---|
| `data` -> `/data` | Node-RED flows, nodes and configuration |

## Deploy with App-as-Code

1. Edit `service.yml`. It is the single source of truth for image, ports, environment,
   volumes and per-stage overrides. Do not edit the rendered output.
2. Pushing to `main` (or a configured stage branch) runs the service pipeline, which renders
   the manifests with `aac-template-engine` and triggers the deployment.
3. Releases of this definition are published under <https://github.com/app-as-code/aac-nodered>.

## Credits and license

Node-RED is developed by the OpenJS Foundation and contributors and licensed under Apache-2.0.
This repository only contains the deployment definition for it and is not a fork of the
application. The logo is provided by the Node-RED project; see [`assets/ICON_SOURCE.md`](assets/ICON_SOURCE.md)
for icon sources and licenses.
