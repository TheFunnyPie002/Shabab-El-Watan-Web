# A3 — Proposed Project Structure

```text
eye-hris/
├── backend/
│   ├── manage.py
│   ├── config/
│   │   ├── settings/
│   │   │   ├── base.py
│   │   │   ├── development.py
│   │   │   └── production.py
│   │   ├── urls.py
│   │   ├── asgi.py
│   │   └── wsgi.py
│   ├── apps/
│   │   ├── accounts/
│   │   ├── members/
│   │   ├── applications/
│   │   ├── branches/
│   │   ├── attendance/
│   │   ├── evaluations/
│   │   ├── warnings/
│   │   ├── tasks/
│   │   ├── events/
│   │   ├── reports/
│   │   └── audit/
│   ├── requirements.txt
│   └── tests/
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   ├── components/
│   │   ├── features/
│   │   │   ├── auth/
│   │   │   ├── members/
│   │   │   ├── applications/
│   │   │   ├── attendance/
│   │   │   ├── evaluations/
│   │   │   ├── tasks/
│   │   │   ├── events/
│   │   │   └── dashboard/
│   │   ├── api/
│   │   ├── hooks/
│   │   ├── layouts/
│   │   └── styles/
│   ├── package.json
│   └── .env.example
├── docs/
├── .gitignore
├── .env.example
└── README.md
```

## Structure rules
- Keep business logic in backend service functions/domain modules, not in React components.
- Keep each Django app focused on one domain.
- Reuse common UI components, but keep each feature's pages and API calls inside its feature folder.
- Add tests alongside each module or in a centralized test folder, consistently.
- Never commit `.env`, credentials, production database dumps, or uploaded member files.
