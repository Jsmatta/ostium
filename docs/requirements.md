# Requirements

## MVP

- Tenants can sign in and display a short-lived QR credential in the Expo mobile app.
- Property managers can use the Expo web experience to manage users, units, guest access, revocations, and access logs.
- ESP32-CAM scans and locally validates a credential before controlling the relay.
- FastAPI records synchronized access and doorbell events in SQLite.
- Devices continue to validate previously synchronized credentials during a temporary network outage.

## Constraints

Use one FastAPI application, SQLite through `sqlite3`, one Expo Router codebase for native and web clients, and ESP32 Arduino firmware. Devices communicate with FastAPI through HTTPS polling and event posts. The MVP excludes MQTT, Redis, an ORM, a background worker, push notifications, and a second web frontend.
