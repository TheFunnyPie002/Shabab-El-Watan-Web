# A6 — API Architecture Guidelines

## Conventions
- Prefix API routes with `/api/v1/`.
- Use plural resource names: `/members/`, `/applications/`, `/events/`.
- Use JSON request and response bodies.
- Paginate list endpoints.
- Apply filtering and search on the server for large datasets.
- Use consistent timestamps and document the organization timezone.
- Version API behavior deliberately; avoid breaking frontend clients silently.

## Example route map
- `POST /api/v1/auth/login/`
- `POST /api/v1/auth/logout/`
- `GET /api/v1/me/`
- `GET /api/v1/members/`
- `GET /api/v1/members/{id}/`
- `GET /api/v1/applications/`
- `POST /api/v1/applications/`
- `POST /api/v1/applications/{id}/decision/`
- `GET /api/v1/attendance/`
- `GET /api/v1/evaluations/`
- `POST /api/v1/evaluations/{id}/finalize/`
- `GET /api/v1/tasks/`
- `GET /api/v1/events/`
- `GET /api/v1/dashboard/summary/`

These are proposed routes, not implemented endpoints.

## API contract example
Successful response:
```json
{
  "data": {
    "id": 42,
    "status": "probation"
  }
}
```

Paginated list response:
```json
{
  "data": [],
  "pagination": {
    "page": 1,
    "page_size": 20,
    "total": 0
  }
}
```

Keep the API format consistent across the project. If the team chooses standard DRF pagination/error responses instead, document that choice and use it everywhere.

## Security
- Every endpoint must enforce authentication where required.
- Every object lookup must check the user's permissions and data scope.
- Do not rely on frontend hiding to protect data.
- Use explicit serializers to control which fields are readable/writable.
- Use controlled action endpoints for approval, finalization, and status transitions.
