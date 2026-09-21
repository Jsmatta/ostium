# Backend

The backend is one FastAPI application backed by SQLite. It provides the JSON API for the Expo client and the HTTPS device API for ESP32-CAM units.

Organize application code by domain: `auth/`, `users/`, `units/`, `credentials/`, `access/`, `devices/`, and `logs/`. Keep database queries in a small `database/` layer using parameterized `sqlite3` statements. Add tests under `tests/` as implementation begins.

The backend issues signed, time-limited QR credentials and records access events. It does not make unlock decisions: ESP32 units validate credentials locally. Device configuration and revocation data are served through `GET /devices/{device_id}/config`; devices post events through `POST /devices/{device_id}/events`.

There is no MQTT, Redis, ORM, or job worker in the initial architecture. Use environment variables for signing keys and device secrets; never store them in the repository.
