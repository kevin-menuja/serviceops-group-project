# ServiceOps frontend (academic group project)

This directory contains the **Next.js 16 / React 19** client for the ServiceOps academic final project.

Read the [repository root README](../README.md) first for the architecture, group-project attribution, backend and PostgreSQL prerequisites, setup instructions and security limitations.

## Local development

~~~bash
cp .env.example .env.local
# Edit BACKEND_API_URL to point at a locally running ServiceOps.Api
npm ci
npm run dev
~~~

## Validation

~~~bash
npm run lint
npm run build
npm audit --omit=dev
~~~

The current coursework snapshot uses a pinned shadcn stylesheet resolved from the installed package for Tailwind compilation. Dependencies must be installed before building. Do not put real keys in NEXT_PUBLIC_* variables: those values are exposed to browsers.

This frontend is part of the **completed ServiceOps final group project** for the **Computing Project** module in the **4th semester** of the **Higher Diploma in Computing & Software Engineering**.
