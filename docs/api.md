# API

FastAPI exposes JSON over HTTPS. User endpoints use a user access token; device endpoints use a device-specific credential. Version routes before public use, for example `/api/v1/...`.

## User API

Initial user routes cover login, profile, current QR credential, guest credentials, revocation, users, units, and access logs. Enforce roles server-side for every manager action; client route visibility is not authorization.

## Device API

```text
GET  /devices/{device_id}/config
POST /devices/{device_id}/events
POST /devices/{device_id}/snapshots
```

`config` returns the current device configuration and revocation data. `events` accepts an access result or doorbell event. Snapshot upload is optional in the MVP. Device calls must be authenticated, scoped to the requested device ID, and accepted only over HTTPS.
