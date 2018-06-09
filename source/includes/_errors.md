# Errors

| Error Code | Meaning |
| ---------- | ------- |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 409 | Conflict |
| 500 | Internal Server Error |

## Parameters

> Example

```json
{
    "error": {
        "status": 401,
        "title": "Unauthorized",
        "message": "Invalid token."
    }
}
```

| Param | Description |
| ----- | ----------- |
| status | Status code |
| title | Description of error |
| message | Message of error |
