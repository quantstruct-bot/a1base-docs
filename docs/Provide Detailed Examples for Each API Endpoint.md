
# API Reference with Detailed Examples

This document provides detailed examples for each API endpoint to help developers understand how to use the API effectively. The examples cover common use cases and demonstrate how to handle different data types and error scenarios.

## Messages

### Send Individual Message (`/v1/messages/individual/{accountId}/send`)

Sends a message to an individual recipient.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Request Body (JSON):**

```json
{
  "content": "Hello, this is a test message.",
  "attachment_uri": "https://example.com/image.jpg",
  "from": "61421868490",
  "to": "61433174782",
  "service": "whatsapp"
}
```

**Example Request (cURL):**

```bash
curl -X POST \
  'https://your-api-endpoint/v1/messages/individual/your_account_id/send' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret' \
  -d '{
    "content": "Hello, this is a test message.",
    "attachment_uri": "https://example.com/image.jpg",
    "from": "61421868490",
    "to": "61433174782",
    "service": "whatsapp"
  }'
```

**Example Request (Python):**

```python
import requests
import json

url = "https://your-api-endpoint/v1/messages/individual/your_account_id/send"
headers = {
    "Content-Type": "application/json",
    "x-api-key": "your_api_key",
    "x-api-secret": "your_api_secret"
}
data = {
    "content": "Hello, this is a test message.",
    "attachment_uri": "https://example.com/image.jpg",
    "from": "61421868490",
    "to": "61433174782",
    "service": "whatsapp"
}

response = requests.post(url, headers=headers, data=json.dumps(data))

print(response.status_code)
print(response.json())
```

**Example Request (Node.js):**

```javascript
const axios = require('axios');

const data = JSON.stringify({
  "content": "Hello, this is a test message.",
  "attachment_uri": "https://example.com/image.jpg",
  "from": "61421868490",
  "to": "61433174782",
  "service": "whatsapp"
});

const config = {
  method: 'post',
  url: 'https://your-api-endpoint/v1/messages/individual/your_account_id/send',
  headers: {
    'Content-Type': 'application/json',
    'x-api-key': 'your_api_key',
    'x-api-secret': 'your_api_secret'
  },
  data: data
};

axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
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

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "to"
      ],
      "msg": "value is not a valid phone number",
      "type": "value_error"
    }
  ]
}
```

### Send Group Message (`/v1/messages/group/{accountId}/send`)

Sends a message to a group.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Request Body (JSON):**

```json
{
  "content": "Hello everyone, this is a group message!",
  "attachment_uri": "https://example.com/group_image.png",
  "from": "61421868490",
  "service": "whatsapp"
}
```

**Example Request (cURL):**

```bash
curl -X POST \
  'https://your-api-endpoint/v1/messages/group/your_account_id/send' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret' \
  -d '{
    "content": "Hello everyone, this is a group message!",
    "attachment_uri": "https://example.com/group_image.png",
    "from": "61421868490",
    "service": "whatsapp"
  }'
```

**Successful Response (200 OK):**

```json
{
  "thread_id": "some_thread_id",
  "body": "Hello everyone, this is a group message!",
  "status": "queued"
}
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "from"
      ],
      "msg": "value is not a valid phone number",
      "type": "value_error"
    }
  ]
}
```

### Send Message (`/v1/messages/send/{accountId}`)

Sends a message (individual or group).

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Request Body (JSON):**

```json
{
  "content": {
    "message": "Hello, this is a test message."
  },
  "type": "individual",
  "from": "61421868490",
  "to": "61433174782",
  "service": "whatsapp"
}
```

**Example Request (cURL):**

```bash
curl -X POST \
  'https://your-api-endpoint/v1/messages/send/your_account_id' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret' \
  -d '{
    "content": {
      "message": "Hello, this is a test message."
    },
    "type": "individual",
    "from": "61421868490",
    "to": "61433174782",
    "service": "whatsapp"
  }'
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

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "type"
      ],
      "msg": "value is not a valid enumeration member; permitted: 'individual', 'group'",
      "type": "value_error.enum"
    }
  ]
}
```

### Get Message Details (`/v1/messages/individual/{accountId}/get-details/{messageId}`)

Retrieves details for a specific message.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `messageId` (path, required): The ID of the message.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Example Request (cURL):**

```bash
curl -X GET \
  'https://your-api-endpoint/v1/messages/individual/your_account_id/get-details/your_message_id' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret'
```

**Successful Response (200 OK):**

```json
{
  "messageId": "your_message_id",
  "accountId": "your_account_id",
  "from": "61421868490",
  "to": "61433174782",
  "body": "Hello, this is a test message.",
  "status": "sent",
  "timestamp": "2024-01-01T12:00:00Z"
}
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "messageId"
      ],
      "msg": "value is not a valid UUID",
      "type": "value_error.uuid"
    }
  ]
}
```

### Get Recent Messages (`/v1/messages/threads/{accountId}/get-recent/{threadId}`)

Retrieves recent messages from a thread.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `threadId` (path, required): The ID of the thread.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Example Request (cURL):**

```bash
curl -X GET \
  'https://your-api-endpoint/v1/messages/threads/your_account_id/get-recent/your_thread_id' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret'
```

**Successful Response (200 OK):**

```json
[
  {
    "messageId": "message_id_1",
    "body": "Recent message 1"
  },
  {
    "messageId": "message_id_2",
    "body": "Recent message 2"
  }
]
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "threadId"
      ],
      "msg": "value is not a valid UUID",
      "type": "value_error.uuid"
    }
  ]
}
```

### Get Chat Group (`/v1/messages/threads/{accountId}/get-details/{threadId}`)

Retrieves details for a chat group.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `threadId` (path, required): The ID of the thread.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Example Request (cURL):**

```bash
curl -X GET \
  'https://your-api-endpoint/v1/messages/threads/your_account_id/get-details/your_thread_id' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret'
```

**Successful Response (200 OK):**

```json
{
  "threadId": "your_thread_id",
  "name": "Group Chat Name",
  "participants": ["61421868490", "61433174782"]
}
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "threadId"
      ],
      "msg": "value is not a valid UUID",
      "type": "value_error.uuid"
    }
  ]
}
```

### All Threads (`/v1/messages/threads/{accountId}/get-all`)

Retrieves all threads for an account.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Example Request (cURL):**

```bash
curl -X GET \
  'https://your-api-endpoint/v1/messages/threads/your_account_id/get-all' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret'
```

**Successful Response (200 OK):**

```json
[
  {
    "threadId": "thread_id_1",
    "name": "Thread 1"
  },
  {
    "threadId": "thread_id_2",
    "name": "Thread 2"
  }
]
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "accountId"
      ],
      "msg": "string does not match regex \"^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$\"",
      "type": "value_error.str.regex"
    }
  ]
}
```

### All Threads Number (`/v1/messages/threads/{accountId}/get-all/{phone_number}`)

Retrieves all threads for an account associated with a specific phone number.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `phone_number` (path, required): The phone number.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Example Request (cURL):**

```bash
curl -X GET \
  'https://your-api-endpoint/v1/messages/threads/your_account_id/get-all/61433174782' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret'
```

**Successful Response (200 OK):**

```json
[
  {
    "threadId": "thread_id_1",
    "name": "Thread with 61433174782"
  }
]
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "path",
        "phone_number"
      ],
      "msg": "value is not a valid phone number",
      "type": "value_error"
    }
  ]
}
```

## Emails

### Create Email (`/v1/emails/{accountId}/create-email`)

Creates a new email.  The specific parameters for creating an email are not defined in the provided OpenAPI spec.  This example assumes a basic structure.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Request Body (JSON - Example):**

```json
{
  "sender_address": "jane@a101.bot",
  "recipient_address": "john@a101.bot",
  "subject": "Test Email",
  "body": "This is a test email body."
}
```

**Example Request (cURL):**

```bash
curl -X POST \
  'https://your-api-endpoint/v1/emails/your_account_id/create-email' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret' \
  -d '{
    "sender_address": "jane@a101.bot",
    "recipient_address": "john@a101.bot",
    "subject": "Test Email",
    "body": "This is a test email body."
  }'
```

**Successful Response (200 OK):**

```json
{
  "emailId": "email_id_123",
  "status": "created"
}
```

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "sender_address"
      ],
      "msg": "value is not a valid email address",
      "type": "value_error.email"
    }
  ]
}
```

### Send Email (`/v1/emails/{accountId}/send`)

Sends an email.

**Parameters:**

*   `accountId` (path, required): The ID of the account.
*   `x-api-key` (header, required): Your API key.
*   `x-api-secret` (header, required): Your API secret.

**Request Body (JSON):**

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

**Example Request (cURL):**

```bash
curl -X POST \
  'https://your-api-endpoint/v1/emails/your_account_id/send' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: your_api_key' \
  -H 'x-api-secret: your_api_secret' \
  -d '{
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
  }'
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

**Error Response (422 Validation Error):**

```json
{
  "detail": [
    {
      "loc": [
        "body",
        "recipient_address"
      ],
      "msg": "value is not a valid email address",
      "type": "value_error.email"
    }
  ]
}
```

## Webhooks

### New Mail (`/v1/emails/mailserver/incoming`)

This endpoint is for receiving incoming emails via webhook.

**Request Body (JSON - Example):**

```json
{
  "sender": "john@example.com",
  "recipient": "your_webhook_endpoint@example.com",
  "subject": "Incoming Email",
  "body": "This is the body of the incoming email.",
  "attachments": [
    "https://example.com/attachment1.pdf"
  ]
}
```

**Successful Response (200 OK):**

```json
{
  "status": "received",
  "message": "Email received successfully"
}
```

### Whatsapp Incoming (`/v1/wa/whatsapp/incoming`)

This endpoint is for receiving incoming WhatsApp messages via webhook.

**Request Body (JSON - Example):**

```json
{
  "external_thread_id": "3456098@s.whatsapp",
  "external_message_id": "2asd5678cfvgh123",
  "chat_type": "group",
  "content": "Hello from WhatsApp!",
  "sender_name": "Bobby",
  "sender_number": "61421868490",
  "participants": ["61421868490", "61433174782"],
  "a1_account_number": "61421868490",
  "timestamp": 1734486451000,
  "secret_key": "xxx"
}
```

**Successful Response (200 OK):**

```json
{
  "status": "received",
  "message": "WhatsApp message received successfully"
}
```
