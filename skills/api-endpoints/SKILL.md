---
name: api-endpoints
description: Guides the creation of new API endpoints. Use when adding routes, handlers, and controllers to the project.
---

# API Endpoints

Follow these conventions whenever you add an endpoint.

## Where files live

- Routes: `src/routes/<resource>.routes.ts` (one file per resource)
- Controllers: `src/controllers/<resource>.controller.ts`
- Handlers/services: `src/services/<resource>.service.ts`
- Tests: next to the file under test, `<name>.test.ts`

Routes only map a path to a controller. Controllers parse input and shape the response. Business logic lives in services.

## Naming conventions

- Route paths: lowercase, plural nouns, kebab-case. `/api/v1/user-profiles`, not `/getUserProfile`.
- HTTP verbs carry the action: `GET` read, `POST` create, `PUT`/`PATCH` update, `DELETE` remove.
- Controller functions: `verbResource`, camelCase. `listUsers`, `getUser`, `createUser`, `updateUser`, `deleteUser`.
- Files: kebab-case with a role suffix (`.routes`, `.controller`, `.service`).

## Error handling pattern

- Validate input at the controller boundary before calling a service.
- Services throw typed errors (`NotFoundError`, `ValidationError`, `UnauthorizedError`). Never return `null` to signal failure.
- Controllers do not use `try/catch` for flow control. Wrap async handlers so errors reach one central error middleware.
- The error middleware maps error types to status codes: 400 validation, 401 unauthenticated, 403 forbidden, 404 not found, 500 anything else.
- Never leak stack traces or internal messages in a response.

## Response shape

Success:

```json
{ "data": { }, "error": null }
```

Failure:

```json
{ "data": null, "error": { "code": "NOT_FOUND", "message": "User not found" } }
```

- `error.code` is a stable `UPPER_SNAKE_CASE` string. `message` is human-readable.
- List endpoints return `data` as an array and include `meta` with `page`, `pageSize`, `total`.
- Use the correct status: 201 on create, 204 on delete with no body, 200 otherwise.

## Before committing

- [ ] Route registered in the router index
- [ ] Input validated, and auth applied where required
- [ ] Errors go through the central error middleware
- [ ] Response matches the shape above
- [ ] Tests cover success, validation failure, and not-found
- [ ] Lint, type check, and the test suite pass
- [ ] API docs updated (OpenAPI or README) for the new endpoint
