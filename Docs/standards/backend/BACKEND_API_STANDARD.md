# BACKEND_API_STANDARD

## REST Conventions

### Routes Naming
- Lowercase, plural nouns (kebab-case preferred)
- Resource-oriented endpoints
- `/api/{version}/{resource}` structure

Examples:
```
GET    /api/v1/users
GET    /api/v1/users/:id
POST   /api/v1/users
PUT    /api/v1/users/:id
DELETE /api/v1/users/:id
```

### HTTP Methods
- `GET` — тільки для отримання даних
- `POST` — створення нового ресурсу або слідовання
- `PUT` — повне оновлення ресурсу
- `PATCH` — часткове оновлення ресурсу
- `DELETE` — видалення ресурсу

### Status Codes
- `200 OK` — успішний GET
- `201 Created` — створення (POST)
- `204 No Content` — успішне DELETE
- `400 Bad Request` — валідація помилок
- `401 Unauthorized` — немає токена
- `403 Forbidden` — немає прав
- `404 Not Found` — ресурс не існує
- `422 Unprocessable Entity` — валідація даних
- `429 Too Many Requests` — rate limiting
- `500 Internal Server Error` — внутрішня помилка

### Pagination
- Обязательне пагінація для колекцій
- Параметри: `page`, `limit` (default 20, max 100)
- Відповідь включає `meta`

Examples:
```
GET /api/v1/users?page=1&limit=20
```

### Filtering
- Параметри `filter[field]=value`
- Підтримка операторів: `eq`, `ne`, `gt`, `gte`, `lt`, `lte`, `like`, `in`
- Приклад: `GET /api/v1/users?filter[active]=true&filter[age][gt]=18`

### Sorting
- Параметр `sort=field:direction`
- Направлення: `asc` або `desc`
- Приклад: `GET /api/v1/users?sort=created_at:desc`

### Versioning
- URL versioning: `/api/v1/`, `/api/v2/`
- Заборонено query parameter versioning
- Новий версію тільки додавання, ніколи зміна старого

### Errors

Коротка структура відповіді:
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      { "field": "email", "issue": "must be valid" }
    ]
  }
}
```

Enum кодів помилок:
- `VALIDATION_ERROR`
- `AUTHENTICATION_ERROR`
- `AUTHORIZATION_ERROR`
- `NOT_FOUND`
- `CONFLICT`
- `RATE_LIMIT`
- `INTERNAL_ERROR`
