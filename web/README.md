# Web Experience

The web dashboard is built from the shared Expo application in `mobile/` through React Native Web. This directory is reserved for browser build, deployment, and responsive-layout notes; do not create a separate React, Vite, or Next.js application here.

Manager routes should present users, units, guest access, revocations, access logs, and doorbell events in a desktop-friendly layout. The same TypeScript API client calls FastAPI over HTTPS for web and native clients.
