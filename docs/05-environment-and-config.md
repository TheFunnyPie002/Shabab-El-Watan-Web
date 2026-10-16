# A5 — Environment Configuration

## Local setup
1. Install a supported Python version, Node.js LTS, Git, and PostgreSQL.
2. Create a Python virtual environment inside `backend/`.
3. Install backend requirements.
4. Create a local PostgreSQL database and a dedicated development database user.
5. Copy `.env.example` to `.env` and replace placeholders.
6. Keep `.env` out of Git.
7. Run migrations and create a local development admin account only after Django settings are configured.

## Rules
- Never commit real passwords, API keys, secret keys, or production connection strings.
- Use separate secrets and databases for development, staging, and production.
- Set `DEBUG=False` in production.
- Restrict allowed hosts and configure HTTPS in production.
- Use a secret manager or hosting environment variables for deployment secrets.
- Do not put secrets in React variables prefixed with `VITE_`; those values are exposed to browsers.
