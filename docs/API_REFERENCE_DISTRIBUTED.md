# API Reference Documentation for MemoBuild

## Overview

The MemoBuild REST API allows for remote interactions with the MemoBuild application. It is designed to support distributed execution and data caching.

## REST API Specifications

### Base URL
`https://api.memobuild.nrelab.org`

### Authentication
- **Authentication Type:** Bearer Token
- **Required Header:** `Authorization: Bearer {token}`

### Rate Limiting
- **Limit:** 100 requests per minute
- **Headers:** `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`

## Endpoints

### 1. Execute Task
- **Endpoint:** `/tasks/execute`
- **Method:** `POST`
- **Request Body:**  
  ```json
  {
      "task_id": "string",
      "parameters": {"key": "value"}
  }
  ```  
- **Response:**  
  - **201 Created**  
    ```json
    {
        "task_id": "string",
        "status": "pending"
    }
    ```
  - **400 Bad Request**  
    ```json
    {
        "error": "Invalid parameters"
    }
    ```

### 2. Get Task Status
- **Endpoint:** `/tasks/{task_id}`
- **Method:** `GET`
- **Response:**  
  - **200 OK**  
    ```json
    {
        "task_id": "string",
        "status": "completed",
        "result": {}  
    }
    ```
  - **404 Not Found**  
    ```json
    {
        "error": "Task not found"
    }
    ```

## REAPI Compliance
- **REAPI Compliance Details:** This API follows the RESTful standards and adheres to REAPI compliance by exposing resources via HTTP methods and using standard response codes.

## Error Handling
- **Common Errors:**  
  - **401 Unauthorized**: Invalid or missing token  
  - **429 Too Many Requests**: Rate limit exceeded  
  - **500 Internal Server Error**: Unexpected server error

## Integration Patterns
- **Remote Execution:** Use the `/tasks/execute` endpoint to trigger tasks remotely.
- **Caching:** Implement a caching layer to reduce API calls for frequently requested results.

## Examples
### Example Request: Execute Task
```bash
curl -X POST https://api.memobuild.nrelab.org/tasks/execute \
-H "Authorization: Bearer YOUR_TOKEN" \
-H "Content-Type: application/json" \
-d '{"task_id": "123", "parameters": {"key": "value"}}'
```

### Example Response: Task Created
```json
{
    "task_id": "123",
    "status": "pending"
}
```

### Example Error: Invalid Parameters
```json
{
    "error": "Invalid parameters"
}
```

---