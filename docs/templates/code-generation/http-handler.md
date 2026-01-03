# Template: HTTP Handler with Service Layer

**Category**: Code Generation
**Use Case**: Creating HTTP handlers with proper error handling
**Language**: Go (adaptable to other languages)

---

## Template

```
Create a {{HTTP_METHOD}} handler for {{ENDPOINT_PATH}} in {{HANDLER_FILE_PATH}}.

**Requirements**:

1. Handler function:
   - Name: {{HANDLER_FUNCTION_NAME}}
   - Method: {{HTTP_METHOD}}
   - Path: {{ENDPOINT_PATH}}
   - Request body: {{REQUEST_STRUCT}} (validate with go-playground/validator)
   - Response: {{RESPONSE_STRUCT}}

2. Validation:
   - Validate {{REQUEST_FIELD_1}}: {{VALIDATION_RULE_1}}
   - Validate {{REQUEST_FIELD_2}}: {{VALIDATION_RULE_2}}
   - Return 400 Bad Request on validation failure

3. Service layer call:
   - Call {{SERVICE_METHOD}} from {{SERVICE_INTERFACE}}
   - Pass {{SERVICE_PARAMS}}
   - Handle service errors appropriately

4. Error handling:
   - 400: Validation errors
   - 404: {{NOT_FOUND_CONDITION}}
   - 429: Rate limit exceeded
   - 500: Internal server error
   - Log errors with request ID

5. Response:
   - 200: Success with {{RESPONSE_STRUCT}}
   - Include {{RESPONSE_HEADERS}} headers
   - JSON format

6. Testing:
   - Write unit tests mocking {{SERVICE_INTERFACE}}
   - Test cases: success, validation errors, service errors
   - Use httptest.NewRecorder for testing

Include detailed comments explaining:
- What the handler does
- Validation rules
- Error scenarios
- Expected request/response format

Use TodoWrite to track: handler creation, service integration, tests, verification.
```

---

## Example: User Registration Handler

**Filled template:**
```
Create a POST handler for /api/v1/users/register in backend/internal/handlers/user_handler.go.

**Requirements**:

1. Handler function:
   - Name: HandleRegister
   - Method: POST
   - Path: /api/v1/users/register
   - Request body: RegisterRequest (validate with go-playground/validator)
   - Response: RegisterResponse

2. Validation:
   - Validate email: required, valid email format
   - Validate password: required, min 8 chars, contains uppercase, lowercase, number
   - Validate username: required, alphanumeric, 3-20 chars
   - Return 400 Bad Request on validation failure

3. Service layer call:
   - Call CreateUser from UserService interface
   - Pass email, username, hashed password
   - Handle service errors appropriately

4. Error handling:
   - 400: Validation errors or email already exists
   - 429: Rate limit exceeded (more than 5 registrations per hour from same IP)
   - 500: Internal server error (database issues, hashing failure)
   - Log errors with request ID

5. Response:
   - 201: Created with RegisterResponse (user ID, email, created_at)
   - Include Location header with /api/v1/users/{id}
   - JSON format

6. Testing:
   - Write unit tests mocking UserService
   - Test cases: successful registration, duplicate email, weak password, invalid email format, service errors
   - Use httptest.NewRecorder for testing

Include detailed comments explaining:
- What the handler does
- Validation rules
- Error scenarios
- Expected request/response format

Use TodoWrite to track: handler creation, service integration, tests, verification.
```

---

## Placeholder Reference

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{HTTP_METHOD}}` | HTTP method | `GET`, `POST`, `PUT`, `DELETE` |
| `{{ENDPOINT_PATH}}` | API endpoint path | `/api/v1/users` |
| `{{HANDLER_FILE_PATH}}` | File location | `internal/handlers/user_handler.go` |
| `{{HANDLER_FUNCTION_NAME}}` | Function name | `HandleCreateUser` |
| `{{REQUEST_STRUCT}}` | Request type | `CreateUserRequest` |
| `{{RESPONSE_STRUCT}}` | Response type | `CreateUserResponse` |
| `{{REQUEST_FIELD_N}}` | Request field to validate | `email`, `password` |
| `{{VALIDATION_RULE_N}}` | Validation rule | `required, email format` |
| `{{SERVICE_METHOD}}` | Service method to call | `CreateUser` |
| `{{SERVICE_INTERFACE}}` | Service interface name | `UserService` |
| `{{SERVICE_PARAMS}}` | Parameters to pass | `email, username, password` |
| `{{NOT_FOUND_CONDITION}}` | When to return 404 | `User not found` |
| `{{RESPONSE_HEADERS}}` | Additional headers | `Location`, `ETag` |

---

## Common Handler Patterns

### GET List with Pagination
```
{{HTTP_METHOD}} = GET
{{ENDPOINT_PATH}} = /api/v1/users
Query params: page (int, default 1), limit (int, default 20, max 100)
Response: ListUsersResponse with pagination metadata
```

### GET Single Resource
```
{{HTTP_METHOD}} = GET
{{ENDPOINT_PATH}} = /api/v1/users/:id
Path param: id (UUID)
404: User not found
Response: UserResponse
```

### POST Create Resource
```
{{HTTP_METHOD}} = POST
{{ENDPOINT_PATH}} = /api/v1/users
Request: CreateUserRequest
Response: 201 Created with Location header
```

### PUT Update Resource
```
{{HTTP_METHOD}} = PUT
{{ENDPOINT_PATH}} = /api/v1/users/:id
Request: UpdateUserRequest
404: User not found
Response: 200 OK with UpdatedUserResponse
```

### DELETE Resource
```
{{HTTP_METHOD}} = DELETE
{{ENDPOINT_PATH}} = /api/v1/users/:id
404: User not found
Response: 204 No Content
```

---

## Error Response Format

**Include this in prompts:**
```go
// Standard error response structure
type ErrorResponse struct {
    Error   string `json:"error"`
    Message string `json:"message"`
    Details []string `json:"details,omitempty"`
}
```

---

## Tips for Better Handler Prompts

1. **Specify exact paths**: Not "user endpoint" but "/api/v1/users"
2. **List all validation rules**: Be explicit about min/max, formats, required fields
3. **Define error scenarios**: When to return 400 vs 404 vs 500
4. **Request test coverage**: "Write unit tests with mocked service"
5. **Ask for comments**: "Include detailed comments explaining..."
6. **Use TodoWrite**: Track handler, service, tests separately

---

## Advanced: Handler with Middleware

**Prompt addition:**
```
Apply middleware:
- {{AUTH_MIDDLEWARE}}: Require authenticated user
- {{RATE_LIMIT_MIDDLEWARE}}: Limit to {{RATE_LIMIT}}
- {{CORS_MIDDLEWARE}}: Allow {{ALLOWED_ORIGINS}}
```

**Example:**
```
Apply middleware:
- RequireAuth: Require authenticated user with valid JWT
- RateLimit: Limit to 10 requests per minute per user
- CORS: Allow https://frontend.example.com
```

---

## Verification Checklist

After Claude generates the handler:
- [ ] Compiles without errors
- [ ] All validation rules implemented
- [ ] Service layer properly called
- [ ] Error handling covers all cases
- [ ] Tests written and passing
- [ ] Comments are clear
- [ ] Follows project conventions
- [ ] No hardcoded values

---

**Related Templates**:
- [Service Layer](../code-generation/service-layer.md)
- [Data Model](../code-generation/data-model.md)
- [Unit Test](../testing/unit-test.md)
- [Integration Test](../testing/integration-test.md)
