
# Detailed Request and Response Examples for API Endpoints

This document provides detailed examples of request bodies and response structures for various API endpoints. These examples will help developers understand how to properly format their requests and handle the responses they receive.

## API Reference

This section provides examples for the following endpoints:

*   `POST /messages/individual/{accountId}/send`
*   `POST /messages/group/{accountId}/send`
*   `GET /messages/individual/{accountId}/get-details/{messageId}`
*   `GET /messages/threads/{accountId}/get-all`
*   `GET /messages/threads/{accountId}/get-all/{phone_number}`
*   `GET /messages/threads/{accountId}/get-details/{threadId}`
*   `GET /messages/threads/{accountId}/get-recent/{threadId}`
*   `POST /emails/{accountId}/send`
*   `POST /emails/{accountId}/create-email`

All examples are in JSON format.

### 1. `POST /messages/individual/{accountId}/send`

Sends an individual message.

**Description:** Sends a message to a specified recipient.  Message sent status returns in webhook.

**Parameters:**

*   `accountId` (path): The account ID.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Request Body Example:**

```json
{
  "content": "Hello, this is a test message.",
  "attachment_uri": "https://example.com/attachment.pdf",
  "from": "61421868490",
  "to": "61433174782",
  "service": "whatsapp"
}
```

**Successful Response (200 OK):**

```json
{
  "to": "61433174782",
  "from": "61421868490",
  "body": "Hello, this is a test message.",
  "status": "queued"
}
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "to"
      ],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

### 2. `POST /messages/group/{accountId}/send`

Sends a message to a group.

**Description:** Sends a message to a WhatsApp group.

**Parameters:**

*   `accountId` (path): The account ID.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Request Body Example:**

```json
{
  "content": "Hello everyone!",
  "attachment_uri": "https://example.com/group_image.jpg",
  "from": "61421868490",
  "service": "whatsapp"
}
```

**Successful Response (200 OK):**

```json
{
  "thread_id": "some_thread_id",
  "body": "Hello everyone!",
  "status": "queued"
}
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "content"
      ],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

### 3. `GET /messages/individual/{accountId}/get-details/{messageId}`

Retrieves details of an individual message.

**Description:** Retrieves details for a specific message.

**Parameters:**

*   `accountId` (path): The account ID.
*   `messageId` (path): The ID of the message to retrieve.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Successful Response (200 OK):**

```json
{
  "messageId": "some_message_id",
  "accountId": "some_account_id",
  "from": "61421868490",
  "to": "61433174782",
  "body": "Hello, this is a test message.",
  "status": "sent",
  "timestamp": "2024-01-01T12:00:00Z"
}
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "messageId"
      ],
      "msg": "value is not a valid uuid",
      "type": "type_error.uuid"
    }
  ]
}
```

### 4. `GET /messages/threads/{accountId}/get-all`

Retrieves all threads for an account.

**Description:** Retrieves all message threads associated with the specified account.

**Parameters:**

*   `accountId` (path): The account ID.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Successful Response (200 OK):**

```json
[
  {
    "threadId": "thread_1",
    "participants": ["61421868490", "61433174782"],
    "lastMessage": "Hello there!",
    "lastMessageTimestamp": "2024-01-05T10:00:00Z"
  },
  {
    "threadId": "thread_2",
    "participants": ["61421868490", "61400000000"],
    "lastMessage": "How are you?",
    "lastMessageTimestamp": "2024-01-04T15:30:00Z"
  }
]
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "accountId"
      ],
      "msg": "value is not a valid uuid",
      "type": "type_error.uuid"
    }
  ]
}
```

### 5. `GET /messages/threads/{accountId}/get-all/{phone_number}`

Retrieves all threads for an account filtered by phone number.

**Description:** Retrieves all message threads associated with the specified account and containing the specified phone number.

**Parameters:**

*   `accountId` (path): The account ID.
*   `phone_number` (path): The phone number to filter by.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Successful Response (200 OK):**

```json
[
  {
    "threadId": "thread_1",
    "participants": ["61421868490", "61433174782"],
    "lastMessage": "Hello there!",
    "lastMessageTimestamp": "2024-01-05T10:00:00Z"
  }
]
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "accountId"
      ],
      "msg": "value is not a valid uuid",
      "type": "type_error.uuid"
    }
  ]
}
```

### 6. `GET /messages/threads/{accountId}/get-details/{threadId}`

Retrieves details of a specific thread.

**Description:** Retrieves details for a specific message thread.

**Parameters:**

*   `accountId` (path): The account ID.
*   `threadId` (path): The ID of the thread to retrieve.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Successful Response (200 OK):**

```json
{
  "threadId": "some_thread_id",
  "participants": ["61421868490", "61433174782"],
  "createdAt": "2023-12-25T08:00:00Z"
}
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "threadId"
      ],
      "msg": "value is not a valid uuid",
      "type": "type_error.uuid"
    }
  ]
}
```

### 7. `GET /messages/threads/{accountId}/get-recent/{threadId}`

Retrieves recent messages from a thread.

**Description:** Retrieves the most recent messages from a specific thread.

**Parameters:**

*   `accountId` (path): The account ID.
*   `threadId` (path): The ID of the thread to retrieve messages from.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Successful Response (200 OK):**

```json
[
  {
    "messageId": "message_1",
    "sender": "61421868490",
    "body": "Hello!",
    "timestamp": "2024-01-06T14:00:00Z"
  },
  {
    "messageId": "message_2",
    "sender": "61433174782",
    "body": "Hi there!",
    "timestamp": "2024-01-06T14:05:00Z"
  }
]
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "threadId"
      ],
      "msg": "value is not a valid uuid",
      "type": "type_error.uuid"
    }
  ]
}
```

### 8. `POST /emails/{accountId}/send`

Sends an email.

**Description:** Sends an email message.

**Parameters:**

*   `accountId` (path): The account ID.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Request Body Example:**

```json
{
  "sender_address": "jane@a101.bot",
  "recipient_address": "john@a101.bot",
  "subject": "Hello from Jane",
  "body": "have a nice day",
  "headers": {
    "bcc": ["jim@a101.bot", "james@a101.bot"],
    "cc": ["sarah@a101.bot", "janette@a101.bot"],
    "reply-to": "jane@a101.bot"
  },
  "attachment_uri": "https://a101.bot/attachment.pdf"
}
```

**Successful Response (200 OK):**

```json
{
  "to": "john@a101.bot",
  "from": "jane@email",
  "subject": "Hello from Jane",
  "body": "have a nice day",
  "status": "queued"
}
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "recipient_address"
      ],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

### 9. `POST /emails/{accountId}/create-email`

Creates an email.  This endpoint's purpose is unclear from the provided OpenAPI spec.  It lacks a request body definition.  A request body example is not possible without further information.

**Description:** Creates an email.

**Parameters:**

*   `accountId` (path): The account ID.
*   `x-api-key` (header): Your API key.
*   `x-api-secret` (header): Your API secret.

**Request Body Example:**

*No request body defined in the OpenAPI spec.*

**Successful Response (200 OK):**

```json
{
  "message": "Email created successfully"
}
```

**Validation Error Response (422 Unprocessable Entity):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "subject"
      ],
      "msg": "field required",
      "type": "value_error.missing"
    }
  ]
}
```

**Note:** The above example assumes a request body is required, even though the OpenAPI spec doesn't define one.  This endpoint needs further clarification.

## Error Handling

All endpoints may return a 422 Unprocessable Entity error if the request body fails validation. The response body will contain a `detail` array with information about each validation error, including the location of the error (`loc`), the error message (`msg`), and the error type (`type`).

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "field_name"
      ],
      "msg": "error message",
      "type": "error.type"
    }
  ]
}
```
