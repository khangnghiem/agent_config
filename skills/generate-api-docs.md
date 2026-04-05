# Skill: Generate API Documentation

## Purpose

Produce clear, accurate documentation for a REST API from its source code or schema.

## Instructions

When asked to document an API, follow these steps:

1. **Identify all endpoints** – Extract HTTP method, path, path parameters, query parameters, request body, and response schemas.
2. **Describe each endpoint**:
   - One-sentence summary of what it does.
   - Detailed description of the behaviour, including side effects.
   - Authentication and authorisation requirements.
3. **Document parameters** – For each parameter include: name, type, required/optional, default value, and description.
4. **Document responses** – For each HTTP status code include: when it is returned and the response body schema with field descriptions.
5. **Provide examples** – At least one request/response example per endpoint using realistic data.
6. **Note error responses** – List common error codes and their meanings.

## Output Format

Use the following Markdown structure for each endpoint:

```markdown
### `METHOD /path`

Short description.

**Auth:** Required / Not required (role: `admin`)

#### Parameters

| Name | In | Type | Required | Description |
|------|-----|------|----------|-------------|
| `id` | path | string | Yes | Unique identifier of the resource |

#### Request Body

```json
{
  "field": "value"
}
```

#### Responses

| Status | Description |
|--------|-------------|
| 200 | Success – returns the updated resource |
| 404 | Resource not found |

#### Example

**Request**
```http
GET /api/v1/users/42
Authorization: Bearer <token>
```

**Response**
```json
{ "id": "42", "name": "Alice" }
```
```
