# Repository Guidelines

## Project Structure & Module Organization

This repository contains Ostium. Keep work scoped to the relevant component:

- `backend/` contains the FastAPI API, authentication, access control, credentials, device configuration, logs, SQLite access, and planned tests.
- `mobile/` contains the shared Expo Router application for native tenant use and the browser-based manager dashboard.
- `web/` contains browser build and deployment notes for the shared Expo application; it is not a second frontend.
- `hardware/esp32/` contains ESP32-CAM firmware and hardware notes.
- `docs/` holds the system requirements, architecture, API, device communication, security, testing, user, and maintenance documentation. Put meeting records in `docs/meeting-notes/`.

Read the relevant component README and `docs/` material before changing interfaces or security-sensitive behavior.

## Build, Test, and Development Commands

Run commands from the component being changed once its project configuration exists:

```sh
cd backend && python -m unittest discover -s tests  # backend tests
cd mobile && npm test                              # Expo client tests
```

The GitHub workflows skip the backend or Expo test suite until that component has its project configuration. Once initialized, document install, build, lint, and local-run commands in the component README.

## Coding Style & Naming Conventions

Follow the formatter, linter, and conventions established within the component once present. Use domain-based directories such as `credentials/`, `access/`, or `devices/`. Name files after their responsibility and use descriptive security-critical names, such as `credentialExpiry` and `revocationList`.

## Testing Guidelines

Add or update tests with every behavior change. Cover access decisions, QR expiration and signature validation, revocation, authorization boundaries, and offline synchronization failures. Name tests after observable behavior, such as `rejects expired credential`. Run the affected component's test command before opening a pull request.

## Commit & Pull Request Guidelines

The available history only contains an initial commit, so no established commit format exists. Use concise imperative subjects, optionally scoped: `backend: reject revoked QR credentials`. Keep commits focused.

Use the pull-request template: describe the change and testing performed. Link relevant issues, update applicable documentation, and include screenshots for web or mobile UI changes. Call out migrations, configuration changes, and security impact.

## Security & Configuration

Never commit secrets. Start local backend configuration from `backend/.env.example`. Treat signing keys, QR payload validation, authentication, HTTPS device credentials, and relay control as security-sensitive; align changes with `docs/security.md`, `docs/api.md`, and `docs/mqtt.md`.
