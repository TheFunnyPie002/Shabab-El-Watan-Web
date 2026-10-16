# A1 — Requirements and Modules

## Purpose
Create one authoritative system for member records, applications, probation, attendance, monthly evaluations, tasks, events, branches, committees, warnings, files, and administration.

## Roles (initial proposal)
- **Union President:** organization-wide overview and explicitly authorized approvals.
- **Vice President:** organization-wide access according to assigned permissions.
- **Central HR:** member lifecycle, applications, probation, attendance, evaluations, and warnings.
- **Branch Manager:** records and operational information for assigned governorate/branch only.
- **Committee Manager:** tasks and committee information within assigned scope.
- **Ordinary Member:** read-only access to their own profile, membership card, evaluations, attendance, and assigned tasks.
- **System Administrator:** technical account/configuration maintenance; business-data access should not be granted automatically unless required.

Roles are starting templates. The implementation should use permissions and scope assignments, not role-name checks scattered through the code.

## Core modules
1. Identity and access control
2. Member directory and profile
3. Applications and 30-day probation
4. Attendance
5. Monthly evaluation and rating classification
6. Three-month distinguished-member eligibility
7. Warnings and policy actions
8. Membership cards
9. Tasks and projects
10. Events and participation
11. Governorates/branches and committees
12. Reports and file storage
13. Admin analytics dashboard
14. Member dashboard
15. Audit logs, security, backups, and deployment

## Business rules to confirm
- Monthly score components total 100: attendance 20, conduct/teamwork 10, task completion 30, initiative/self-development 20, active participation 20.
- Monthly classifications: 90–100 distinguished for that month; 75–89 active; 50–74 needs development; 0–49 underperforming.
- Three-month distinction: average of the latest three consecutive completed monthly scores is at least 90. Clarify whether this is recalculated when a finalized score is corrected.
- Probation: 30 days; a temporary membership number is assigned. Only authorized HR can approve or reject final membership.
- A member should never be able to change their own scores, warnings, official membership state, or administrative assignments.
- Every sensitive write action should record who did it, when, and what changed.

## Acceptance criteria for A1
- HR signs off on the scope and definitions.
- Roles and data scopes are agreed.
- Missing/ambiguous rules are recorded rather than guessed.
- Every module has an owner later assigned by the team.
