
# Address Duplicate Title in `create.mdx`

**Status:** Complete

**Priority:** High

## Description

The `title` and `openapi` metadata are duplicated in the `/api-reference/endpoint/create.mdx` file. This inconsistency can lead to incorrect documentation rendering and user confusion. This document outlines the issue and its resolution.

## Rationale

The repeated title in `/api-reference/endpoint/create.mdx` is a clear inconsistency that needs to be fixed to improve the quality and accuracy of the documentation.  Removing the duplicate ensures that the documentation is rendered correctly and avoids potential confusion for users.

## Target Audience

All users of the API documentation.

## Affected File

`/api-reference/endpoint/create.mdx`

## API Reference

This issue relates to the following API endpoint:

*   `POST /messages/individual/{accountId}/send`

## Problem

The `create.mdx` file contains duplicate `title` and `openapi` metadata.  This can cause issues with documentation generation and display.

**Example of the issue (Incorrect `create.mdx`):**

```mdx
---
title: Send Message
openapi: post /messages/individual/{accountId}/send
title: Send Message  // Duplicate title
openapi: post /messages/individual/{accountId}/send // Duplicate openapi
---

{/* Rest of the documentation content */}
```

## Solution

Remove the duplicate `title` and `openapi` metadata from the `create.mdx` file.

**Corrected `create.mdx`:**

```mdx
---
title: Send Message
openapi: post /messages/individual/{accountId}/send
---

{/* Rest of the documentation content */}
```

## Verification

After applying the fix, verify the following:

1.  The documentation site renders correctly without any errors related to duplicate metadata.
2.  The title of the API endpoint documentation page is displayed correctly.
3.  The OpenAPI specification for the `POST /messages/individual/{accountId}/send` endpoint is correctly loaded and displayed.

## Related Endpoints

The fix primarily addresses the `POST /messages/individual/{accountId}/send` endpoint. However, it's crucial to ensure that no other files in the `api-reference` directory contain similar duplicate metadata.

Here's a list of all endpoints defined in the provided OpenAPI specification:

*   `POST /messages/individual/{accountId}/send`
*   `POST /messages/group/{accountId}/send`
*   `POST /messages/send/{accountId}`
*   `GET /messages/individual/{accountId}/get-details/{messageId}`
*   `GET /messages/threads/{accountId}/get-recent/{threadId}`
*   `GET /messages/threads/{accountId}/get-details/{threadId}`
*   `GET /messages/threads/{accountId}/get-all`
*   `GET /messages/threads/{accountId}/get-all/{phone_number}`
*   `POST /emails/{accountId}/create-email`
*   `POST /emails/{accountId}/send`
*   `POST /emails/mailserver/incoming`
*   `POST /wa/whatsapp/incoming`

It is recommended to review the corresponding `.mdx` files for these endpoints to ensure consistency and avoid similar issues.

## OpenAPI Specification Snippet (Relevant Endpoint)

```yaml
/v1/messages/individual/{accountId}/send:
  post:
    tags:
      - messages
      - messages
    summary: Send Message
    description: |
      Send a message

      Parameters:
      - content: str - Message body text
      - attachment_uri: str - Optional file/media attachment
      - from: str - Sender phone number
      - to: str - Recipient phone number
      - service: str - whatsapp, telegram

      Returns:
      {
      "to": "61433174782",
      "from": "61421868490",
      "body": "today was good.",
      "status": "queued"
      }

      Message sent status returns in webhook
    operationId: messages-send_message
    parameters:
      - name: accountId
        in: path
        required: true
        schema:
          type: string
          title: Accountid
      - name: x-api-key
        in: header
        required: true
        schema:
          type: string
          title: X-Api-Key
      - name: x-api-secret
        in: header
        required: true
        schema:
          type: string
          title: X-Api-Secret
    responses:
      "200":
        description: Successful Response
        content:
          application/json:
            schema: {}
      "422":
        description: Validation Error
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/HTTPValidationError'
