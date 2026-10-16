# A4 — Git and Team Workflow

## Branches
- `main`: stable, reviewed code only.
- `develop`: shared integration branch if the team needs one.
- `feature/A2-database-schema`: feature branches named after task IDs.
- `fix/B8-api-permission-check`: bug-fix branches.

## Workflow
1. Pull the latest shared branch.
2. Create a branch for one task or a tightly related small set of tasks.
3. Commit small, meaningful changes.
4. Push and open a pull request.
5. Ask at least one teammate to review.
6. Run tests and resolve review comments.
7. Merge only after checks pass.

## Commit message examples
- `docs(A1): define initial system scope`
- `feat(B1): add login endpoint`
- `fix(B8): enforce branch scope on member API`
- `test(F7): cover monthly score boundaries`

## Pull request checklist
- [ ] Task ID and purpose are clear.
- [ ] No secrets or real member data are included.
- [ ] Relevant tests pass.
- [ ] Permissions are checked server-side.
- [ ] Database migrations are included if the schema changed.
- [ ] UI handles loading, empty, and error states.
- [ ] Reviewer approved the change.

## Team rules
- Avoid having two people edit the same files simultaneously without coordination.
- Agree on API contracts before frontend/backend work proceeds in parallel.
- Do not push directly to `main`.
- Do not use real member data in development or screenshots.
