# Product Requirements — [PROJECT_NAME]
# ── AI reads this to understand intent before writing code. ─────────────────

## Product in one line
[What it is and who it's for. e.g. "B2B SaaS that helps HR teams automate onboarding workflows."]

## Users
| Role           | Description                          | Key goals                            |
|----------------|--------------------------------------|--------------------------------------|
| [Admin]        | [Manages team, billing, settings]    | [Visibility, control, reporting]     |
| [Member]       | [Day-to-day user of the product]     | [Speed, simplicity, reliability]     |
| [Viewer]       | [Read-only stakeholder]              | [Access data without clutter]        |

## Features — current scope
Mark status: ✅ done · 🔨 in progress · 📋 planned · ❌ out of scope

| Feature                  | Status | Description                                          |
|--------------------------|--------|------------------------------------------------------|
| Authentication           | ✅     | Email/password + Google OAuth. JWT sessions.         |
| [Feature 2]              | 🔨     | [What it does and why]                               |
| [Feature 3]              | 📋     | [What it does and why]                               |
| [Feature 4]              | ❌     | Out of scope — [reason]                              |

## Feature details

### [Feature Name]
**Problem**: [What user pain does this solve?]
**User story**: As a [role], I want to [action] so that [outcome].
**Acceptance criteria**:
- [ ] [Specific, testable condition 1]
- [ ] [Specific, testable condition 2]
- [ ] [Edge case handled: what happens when X]
**Out of scope**: [What this feature explicitly does NOT do]

### [Feature Name]
**Problem**: [...]
**User story**: As a [...], I want to [...] so that [...].
**Acceptance criteria**:
- [ ] [...]
**Out of scope**: [...]

## Business rules
These are non-negotiable constraints AI must always respect:
- [e.g. "A user can belong to only one organisation at a time"]
- [e.g. "Deleted records are soft-deleted — never hard-deleted"]
- [e.g. "Free plan is limited to 5 active projects"]
- [e.g. "All monetary values stored in cents (integer), displayed in dollars"]

## Non-functional requirements
| Concern         | Requirement                                          |
|-----------------|------------------------------------------------------|
| Performance     | [API p95 response < 300ms under normal load]         |
| Availability    | [99.9% uptime SLA]                                   |
| Security        | [OWASP Top 10 compliance · penetration tested yearly]|
| Accessibility   | [WCAG 2.1 AA for all user-facing pages]              |
| Data retention  | [User data deleted within 30 days of account closure]|

## What we are NOT building
[List explicitly to prevent AI from gold-plating or misinterpreting scope]
- [e.g. Mobile apps — web-only for now]
- [e.g. Real-time collaboration — future phase]
- [e.g. Public API — internal use only]
