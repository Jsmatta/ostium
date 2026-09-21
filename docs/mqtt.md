# Device Communication

The initial architecture does not use MQTT. ESP32-CAM units communicate directly with FastAPI through authenticated HTTPS requests.

Devices poll for configuration and revocations, then post access and doorbell events. This adds bounded delay to revocation updates but removes a broker, topic ACLs, retained messages, and another deployed service. MQTT can be reconsidered when immediate updates or a larger device fleet require it.
