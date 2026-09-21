# Ostium

**Ostium** is a camera doorbell and QR-entry system for rental properties, student housing, and multi-unit residences. Tenants use a mobile app to present a short-lived QR code; property managers use a web dashboard to issue and revoke access.

## Architecture

The project intentionally uses a small, single-service architecture:

```text
Expo mobile app + Expo web dashboard
                 | HTTPS JSON API
                 v
       FastAPI application + SQLite
                 ^
                 | HTTPS device API
              ESP32-CAM --> relay-controlled lock
```

- **Frontend:** Expo, React Native, React Native Web, and TypeScript share tenant and manager interfaces across iOS, Android, and browsers.
- **Backend:** one FastAPI application handles users, roles, units, credentials, access logs, and device configuration. It uses parameterized SQL through Python's built-in `sqlite3`; no ORM is required.
- **Device:** ESP32-CAM firmware scans QR codes, validates them locally, controls the relay, and exchanges configuration and events with FastAPI over HTTPS.

There is no MQTT broker, Redis, background worker, or separate web application in the first release. Move from SQLite to PostgreSQL only when concurrent administration or deployment scale requires it.

## Access Flow

1. FastAPI creates a short-lived, signed QR credential for a tenant or guest.
2. The Expo app displays the credential on mobile or web.
3. The ESP32-CAM validates the signature, expiry, unit/device binding, and cached revocation data locally.
4. A valid credential unlocks the relay without waiting for the backend.
5. When online, the device posts access and doorbell events to FastAPI and polls for updated configuration and revocations.

This keeps valid access working during a temporary network outage. Revocations take effect after the device receives its next configuration update.

## Repository Layout

```text
backend/        FastAPI modules, database access, and backend tests
mobile/         Expo Router application shared by native and web clients
web/            Web build and deployment notes for the shared Expo application
hardware/esp32/ ESP32-CAM firmware and hardware notes
docs/           Architecture, API, security, requirements, and operating guides
```

The `mobile/` project is the source of truth for both client experiences. The `web/` directory does not contain a second UI; it documents the web build, responsive manager experience, and deployment concerns.

## Device API

The ESP32 uses a device credential over HTTPS. Initial endpoints are:

```text
GET  /devices/{device_id}/config
POST /devices/{device_id}/events
POST /devices/{device_id}/snapshots
```

See [architecture](docs/architecture.md), [API](docs/api.md), and [security](docs/security.md) before changing device or credential behavior.

## Scope

The MVP covers QR entry, local validation, a relay-controlled lock, tenant QR display, manager access administration, and access logging. Doorbell snapshots and browser-visible event history follow once that path is stable. Push notifications, object storage, instant revocation, and background processing are later additions.
