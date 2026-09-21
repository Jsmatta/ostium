# ESP32 Firmware

ESP32-CAM firmware uses the Arduino framework. It scans QR codes, validates credentials from locally cached configuration, controls the relay, and communicates with FastAPI over HTTPS.

When source is added, keep application code in `src/`, headers in `include/`, local libraries in `lib/`, and tests in `tests/`. The device must poll `GET /devices/{device_id}/config` for configuration and revocations, then post access and doorbell events to FastAPI. It must not depend on a live backend request to unlock a valid credential.
