# API Contracts — [PROJECT_NAME]
# ── AI reads this to avoid inventing endpoints or misusing existing ones. ────

## Base URLs
| Environment | URL                                     |
|-------------|-----------------------------------------|
| Local       | `http://localhost:8000`                 |
| Staging     | `https://api-staging.[domain].com`      |
| Production  | `https://api.[domain].com`              |

## Auth
- Method: [Bearer JWT in `Authorization` header | Cookie `session`]
- Token obtained from: `POST /auth/login` or `POST /auth/refresh`
- Token lifetime: [access: 15min · refresh: 7 days]
- Unauthenticated response: `401 { error: "Unauthorized" }`

## Conventions
- All endpoints: `/api/v1/[resource]`
- Request body: JSON (`Content-Type: application/json`)
- Response envelope: `{ data: {...}, error: null }` on success · `{ data: null, error: { code, message } }` on failure
- Dates: ISO 8601 strings (`2024-03-15T10:30:00Z`)
- IDs: UUIDs (string)
- Pagination: `?page=1&limit=20` → response includes `{ data: [...], meta: { total, page, limit } }`
- Errors follow RFC 7807 problem format

## Endpoints

### Auth
| Method | Path                  | Auth? | Description                  |
|--------|-----------------------|-------|------------------------------|
| POST   | `/auth/login`         | No    | Email + password login       |
| POST   | `/auth/logout`        | Yes   | Invalidate session           |
| POST   | `/auth/refresh`       | No    | Refresh access token         |
| POST   | `/auth/register`      | No    | Create account               |
| GET    | `/auth/me`            | Yes   | Current user profile         |

### [Resource: e.g. Projects]
| Method | Path                      | Auth? | Description                  |
|--------|---------------------------|-------|------------------------------|
| GET    | `/projects`               | Yes   | List user's projects         |
| POST   | `/projects`               | Yes   | Create project               |
| GET    | `/projects/:id`           | Yes   | Get project by ID            |
| PATCH  | `/projects/:id`           | Yes   | Update project fields        |
| DELETE | `/projects/:id`           | Yes   | Soft-delete project          |

### [Resource: e.g. Users / Members]
| Method | Path                          | Auth?  | Description                 |
|--------|-------------------------------|--------|-----------------------------|
| GET    | `/users`                      | Admin  | List all users (paginated)  |
| PATCH  | `/users/:id`                  | Admin  | Update user role            |

## Request / response examples

### POST /auth/login
Request:
```json
{ "email": "user@example.com", "password": "..." }
```
Response 200:
```json
{ "data": { "accessToken": "...", "user": { "id": "uuid", "email": "...", "role": "member" } }, "error": null }
```
Response 401:
```json
{ "data": null, "error": { "code": "INVALID_CREDENTIALS", "message": "Email or password is incorrect" } }
```

### POST /projects
Request:
```json
{ "name": "My Project", "description": "Optional", "visibility": "private" }
```
Response 201:
```json
{ "data": { "id": "uuid", "name": "My Project", "createdAt": "2024-03-15T10:30:00Z" }, "error": null }
```

## Error codes
| Code                   | HTTP | When                                      |
|------------------------|------|-------------------------------------------|
| `UNAUTHORIZED`         | 401  | No valid session                          |
| `FORBIDDEN`            | 403  | Authenticated but insufficient permission |
| `NOT_FOUND`            | 404  | Resource does not exist                   |
| `VALIDATION_ERROR`     | 422  | Invalid request body fields               |
| `CONFLICT`             | 409  | Duplicate resource (e.g. email taken)     |
| `INTERNAL_ERROR`       | 500  | Unexpected server error                   |

## Webhooks (if applicable)
- Delivery: POST to registered URL · signed with `X-Signature-256` header
- Retry: [3 attempts · exponential backoff]
- Events: `[project.created | payment.succeeded | user.deleted]`
- Payload: `{ event: "[type]", data: {...}, timestamp: "ISO8601" }`
