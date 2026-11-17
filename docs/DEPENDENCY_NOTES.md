# Dependency verification notes (academic source snapshot)

During preparation for the personal GitHub academic portfolio:

- Next.js upgraded from 16.3.8 to 16.4.6.
- eslint-config-next synchronized to 16.4.6.
- Zod upgraded to 4.6.7.
- shadcn developer package upgraded to 4.23.0.
- A Tailwind stylesheet import was adjusted to reference the pinned installed shadcn package; the Next.js production build passed after this adjustment.
- Full npm audit retains four moderate-severity advisories in transitive development-time shadcn / ts-morph / minimatch packages. No critical or high findings remained.
- These are development tooling findings, not a verified production exploit. Avoid running vulnerable generator tooling on untrusted input until patched upstream.
- Before any deployment, rerun npm ci, npm audit, npm run lint and npm run build and review any new advisories.

This project remains an academic group source snapshot. No production-grade certification is claimed.
