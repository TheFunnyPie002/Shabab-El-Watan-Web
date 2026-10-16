# A7 — Error Handling and Validation

## Validation layers
1. **Frontend:** helpful early feedback; not a security boundary.
2. **Backend serializers/forms:** validate types, required fields, lengths, ranges, and cross-field rules.
3. **Database:** enforce unique constraints, foreign keys, and other integrity rules.
4. **Domain/service layer:** enforce business transitions, such as probation approval and evaluation finalization.

## Proposed error shape
```json
{
  "error": {
    "code": "validation_error",
    "message": "Please correct the highlighted fields.",
    "fields": {
      "attendance_score": ["Must be between 0 and 20."]
    },
    "request_id": "server-generated-id"
  }
}
```

## Common status codes
- `400 Bad Request`: invalid input or invalid state transition.
- `401 Unauthorized`: authentication is missing or invalid.
- `403 Forbidden`: authenticated user lacks permission.
- `404 Not Found`: resource does not exist or is intentionally concealed from this user.
- `409 Conflict`: duplicate or conflicting state, where appropriate.
- `429 Too Many Requests`: rate limit reached.
- `500 Internal Server Error`: unexpected server failure; do not reveal stack traces to users.

## Business validation examples
- Evaluation component scores must be within their component limits.
- Final monthly total must be 0–100 and computed by trusted backend logic.
- A member cannot approve their own application or edit their own evaluation.
- An application cannot be approved into official membership without the required review/probation process.
- A user cannot access a member record outside their authorized scope.
- Duplicate attendance for the same member/event must be rejected or handled idempotently.

## Logging
- Log unexpected exceptions with a request ID for debugging.
- Do not expose internal stack traces to the frontend.
- Never log passwords, authentication tokens, or unnecessary sensitive member details.
- Record sensitive administrative changes in an audit log.
