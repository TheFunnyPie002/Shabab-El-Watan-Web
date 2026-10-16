# EYE HRIS — Project Foundation

Starter planning and configuration pack for the EYE member-management website.

## Proposed stack
- Backend: Python, Django, Django REST Framework
- Database: PostgreSQL
- Frontend: React + Vite
- API format: JSON REST API
- Version control: Git + GitHub

This pack is a foundation, not a production-ready application. It documents the initial architecture and includes safe starter configuration examples. Authentication, permission enforcement, business rules, and tests must be implemented before real member data is entered.

## Start here
1. Read `docs/01-requirements-and-modules.md`.
2. Review `docs/02-database-schema.md` with the HR team before implementation.
3. Follow `docs/03-project-structure.md`.
4. Copy `.env.example` to `.env` for local development and replace every placeholder.
5. Use `docs/04-git-workflow.md` for team collaboration.
6. Follow `docs/05-api-guidelines.md` and `docs/06-validation-and-errors.md`.

## Important decisions to confirm
- Whether a member can belong to more than one committee.
- Who can approve applications and who can finalize the 30-day probation.
- Whether the 3-month distinguished-member average requires three consecutive calendar months with no gaps.
- The official policy for warnings and their consequences.
- Whether member cards need a QR code or public verification page.
- File storage provider, hosting provider, and data-retention policy.
