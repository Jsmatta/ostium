# Testing

Test the backend with Python's built-in `unittest` until a larger test suite justifies additional tooling. Test the shared Expo application once, then verify the tenant QR flow on native and web targets.

Prioritize credential expiry, signature validation, unit/device binding, revocations, device authentication, manager authorization, and offline ESP32 behavior. Treat a device configuration update as a separate test case from local QR validation: a valid cached credential must work while the backend is unavailable.

Before a pull request, run the affected component's documented test command and perform a hardware check for relay control changes.
