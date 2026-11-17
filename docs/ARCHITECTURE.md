# Architecture — ServiceOps academic group project

ServiceOps is a role-aware, full-stack service-management application completed as the **final group project** for the **Computing Project** module in the **4th semester** of the **Higher Diploma in Computing & Software Engineering**. The group implemented a Next.js web client, ASP.NET Core Web API and PostgreSQL persistence.

## Component overview

~~~mermaid
flowchart TB
    BROWSER["Browser: five operational roles"] --> NEXT["Next.js 16 / React 19 / TypeScript"]
    NEXT --> BFF["Next.js backend API proxy<br/>/api/backend/[...path]"]
    BFF --> API["ASP.NET Core 10 Web API"]
    API --> AUTH["JWT authentication<br/>role and permission policies"]
    API --> SERVICES["Operations / Auth / Reporting / Inventory<br/>Users / Attachments / Notifications"]
    SERVICES --> EF["Entity Framework Core / Npgsql"]
    EF --> DB[("PostgreSQL")]
    API --> FILES["Attachment handling"]
~~~

The browser-facing API route in frontend/src/app/api/backend/[...path]/route.ts mediates requests to the configured backend API. The route contains token handling and refresh logic; see the implementation for exact cookie and error behavior.

## Core source boundaries

| Component | Confirmed responsibility | Main source location |
| --- | --- | --- |
| Web UI | Landing, login, dashboard and role-specific service workspaces | frontend/src/app and frontend/src/components/serviceops |
| BFF/proxy | Next.js API route forwarding requests to backend | frontend/src/app/api/backend/[...path]/route.ts |
| Backend API | Controllers for operations, inventory, analytics, reports, users, auth and attachments | backend/ServiceOps.Api/Controllers |
| Business services | Operational workflows, access, reporting, notifications, user management | backend/ServiceOps.Api/Services |
| Persistence | Entity models, DbContext and EF Core migrations | backend/ServiceOps.Api/Data, Models, Migrations |
| Configuration | PostgreSQL hosted-URL support and private JWT configuration | backend/ServiceOps.Api/Services/Configuration and Program.cs |

## Example work-order view

~~~mermaid
sequenceDiagram
    actor Staff as Service manager or technician
    participant UI as Next.js workspace
    participant PROXY as Next.js backend proxy
    participant API as Operations controller
    participant SERVICE as Operations service
    participant DB as EF Core PostgreSQL

    Staff->>UI: View or update service workflow
    UI->>PROXY: Request with session context
    PROXY->>API: Authorized API request
    API->>SERVICE: Apply role and business rules
    SERVICE->>DB: Read / update records
    DB-->>SERVICE: Persisted state
    SERVICE-->>API: Result
    API-->>PROXY: JSON response
    PROXY-->>UI: Response
    UI-->>Staff: Updated workspace
~~~

This is a conceptual source-boundary diagram; individual controller methods may have different steps. Consult actual endpoints for implementation details.

## Architectural decisions and constraints

- Different roles — Administrator, Service Manager, Technician, Inventory Manager and Customer — use distinct access permissions and workflows.
- Backend uses PostgreSQL/EF Core migrations, so deployment requires a controlled database change and secret-management process.
- The frontend presents a server-side API proxy rather than providing database access directly to the browser.
- Authentication is implemented, but a local build and classroom demo do not establish a public production security assessment.
- The archive contains demo-data seeders, so public demo deployment needs deliberate data and credential isolation.
- The documented architecture and workflows reflect the completed academic group application.

Related: [Case study](CASE_STUDY.md) · [Screenshot evidence](SCREENSHOT_EVIDENCE.md) · [Dependency notes](DEPENDENCY_NOTES.md).
