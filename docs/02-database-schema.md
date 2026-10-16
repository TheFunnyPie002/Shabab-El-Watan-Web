# A2 — Initial Database Schema

This is a conceptual first draft. Use Django migrations to implement it after HR approves the relationships and rules.

## Main entities

### User
- `id` — primary key
- `email` — unique login identifier (if email login is chosen)
- `password` — stored only as a secure password hash by Django
- `is_active`, `is_staff`, `date_joined`
- `last_login`

### Role / Permission / UserRole
Prefer Django's built-in groups and permissions for standard permissions. Add an explicit scope assignment model for governorate/committee boundaries if needed.
- `UserRole`: user, role/group, assigned_by, assigned_at
- `ScopeAssignment`: user, scope_type, scope_id (or explicit foreign keys), assigned_by, created_at

### Member
- `id`
- `user` — one-to-one with User after an account is created
- `membership_number` — unique, nullable until assigned
- `temporary_membership_number` unique, nullable
- `full_name`
- `phone` and other approved contact fields
- `governorate` — foreign key
- `committee` — foreign key, or a many-to-many relationship if multiple committees are allowed
- `membership_status` — applicant / probation / active / inactive / rejected / suspended
- `probation_started_at`, `probation_ends_at`
- `approved_at`, `approved_by`
- `created_at`, `updated_at`

### Application
- `id`, applicant details, requested governorate/committee
- `status` — pending / reviewing / interview / accepted_for_probation / rejected / withdrawn
- `submitted_at`, `reviewed_by`, `reviewed_at`, `decision_note`

### Governorate
- `id`, `name` (unique), `is_active`
- Optional branch contact details

### Committee
- `id`, `name` (unique), `is_active`
- If committees are local to a governorate, add a governorate foreign key. If they are organization-wide, keep the committee global.

### AttendanceRecord
- `id`, `member`, optional `event`, date, status (present / absent / excused / late)
- `recorded_by`, `recorded_at`, `notes`
- Add a uniqueness rule appropriate to the event/meeting so duplicate attendance entries are prevented.

### MonthlyEvaluation
- `id`, `member`, `year`, `month`
- `attendance_score` (0–20)
- `teamwork_score` (0–10)
- `task_score` (0–30)
- `initiative_score` (0–20)
- `participation_score` (0–20)
- `total_score` (computed and stored on finalization, or computed consistently by service logic)
- `classification`
- `status` — draft / finalized
- `evaluated_by`, `finalized_at`, `created_at`, `updated_at`
- Unique constraint: one evaluation per member per calendar month, unless HR explicitly defines another model.

### Warning
- `id`, `member`, `issued_by`, `issued_at`, `reason`, `policy_reference`
- `status` and `action_taken`, if required by the approved regulations
- Restrict visibility and preserve an audit trail.

### Task
- `id`, `title`, `description`, `assigned_to`, `created_by`
- `governorate`, `committee`, `due_at`
- `status` — pending / in_progress / completed / cancelled
- `priority`, `created_at`, `updated_at`, `completed_at`

### Event
- `id`, `title`, `description`, `governorate`, `location`
- `starts_at`, `ends_at`, `status`, `created_by`
- Optional budget/cost field only if approved and appropriately restricted.

### EventParticipant
- `event`, `member`, `registration_status`, `attendance_status`
- Unique constraint on `(event, member)`.

### FileAsset
- `id`, `uploaded_by`, `storage_key`, `original_filename`, `content_type`, `size_bytes`
- Optional relations to event, task, report, or governorate
- `created_at`; never trust a client-provided storage path.

### Report
- `id`, `title`, `summary`, `governorate`, optional `event`
- `created_by`, `created_at`, `status`
- Link report attachments through FileAsset or a dedicated relationship.

### AuditLog
- `id`, `actor`, `action`, `entity_type`, `entity_id`
- `timestamp`, `request_id`, safe change summary
- Do not log passwords, session tokens, or other secrets.

## Relationship overview
- User 1 — 0..1 Member profile
- Member 1 — many Applications (if reapplications are allowed)
- Member 1 — many AttendanceRecords
- Member 1 — many MonthlyEvaluations
- Member 1 — many Warnings
- Member 1 — many Tasks (assignment model may be needed for multiple assignees)
- Event many — many Members through EventParticipant
- Governorate 1 — many Members / Events / Reports (depending on approved rules)
- Committee 1 — many Members only if one committee per member; otherwise use a join table.

## Data and integrity rules
- Use foreign keys and database constraints, not just frontend validation.
- Store timestamps consistently; choose the organization timezone for display.
- Define whether records are archived or deleted. Prefer soft-archiving for official membership history.
- Do not expose sensitive fields through member-facing API serializers.
- Treat evaluation finalization as a controlled action with permission checks and audit logging.
