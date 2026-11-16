# Changelog

All notable changes to this deployment definition are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Changed

- Upstream image tracks Node-RED 5.0 (`nodered/node-red:5.0-debian`) as defined in `service.yml`.

## [0.0.1]

### Added

- Initial App-as-Code service definition for Node-RED on port 1880.
- Persistent flows and configuration in the `data` volume.
- Traefik routing and automatic DNS integration.
- README with configuration reference and project icon.
