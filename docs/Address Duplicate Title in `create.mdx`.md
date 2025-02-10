
# Address Duplicate Title in `create.mdx`

**Status:** Complete
**Priority:** High

## Description

The `title` and `openapi` metadata were duplicated in the `/api-reference/endpoint/create.mdx` file. This inconsistency has been resolved to ensure the documentation renders correctly and avoids confusion.

## Rationale

The repeated title in `/api-reference/endpoint/create.mdx` was a clear inconsistency that needed to be fixed to improve the quality and accuracy of the documentation.  Duplicate metadata can lead to unexpected behavior in documentation generation and potentially confuse users.

## Target Audience

All users of the API documentation.

## Affected Files

*   `/api-reference/endpoint/create.mdx`

## API Reference

This fix relates to the following API endpoint:

*   `POST /messages/individual/{accountId}/send`

## Details

The issue was identified in the `create.mdx` file within the `api-reference/endpoint` directory. The file contained redundant `title` and `openapi` metadata declarations.

The following changes were made:

1.  **Removed the duplicate `title` metadata.**
2.  **Removed the duplicate `openapi` metadata.**

The corrected `create.mdx` file now contains only one instance of each metadata element, ensuring consistency and proper rendering.

## Example

Before (Incorrect):

```mdx
---
title: Send Message
openapi: post-messages-individual-accountid-send.yaml
title: Send Message  // Duplicate title
openapi: post-messages-individual-accountid-send.yaml // Duplicate openapi
---

{/* Rest of the documentation */}
```

After (Corrected):

```mdx
---
title: Send Message
openapi: post-messages-individual-accountid-send.yaml
---

{/* Rest of the documentation */}
```

## Related Endpoints

The following endpoints are related to messaging and may be affected by similar documentation issues.  A review of these files is recommended.

*   `POST /messages/individual/{accountId}/send`
*   `POST /messages/group/{accountId}/send`
*   `POST /messages/send/{accountId}`
*   `GET /messages/individual/{accountId}/get-details/{messageId}`
*   `GET /messages/threads/{accountId}/get-recent/{threadId}`
*   `GET /messages/threads/{accountId}/get-details/{threadId}`
*   `GET /messages/threads/{accountId}/get-all`
*   `GET /messages/threads/{accountId}/get-all/{phone_number}`

## OpenAPI Specification Snippet

The following is a snippet from the OpenAPI specification related to the affected endpoint:

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "fastapi supabase template",
    "version": "0.1.0"
  },
  "paths": {
    "/v1/messages/individual/{accountId}/send": {
      "post": {
        "tags": [
          "messages",
          "messages"
        ],
        "summary": "Send Message",
        "description": "Send a message\n\nParameters:\n- content: str - Message body text\n- attachment_uri: str - Optional file/media attachment\n- from: str - Sender phone number\n- to: str - Recipient phone number\n- service: str - whatsapp, telegram\n\nReturns:\n{\n\"to\": \"61433174782\",\n\"from\": \"61421868490\",\n\"body\": \"today was good.\",\n\"status\": \"queued\"\n}\n\nMessage sent status returns in webhook",
        "operationId": "messages-send_message",
        "parameters": [
          {
            "name": "accountId",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string",
              "title": "Accountid"
            }
          },
          {
            "name": "x-api-key",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string",
              "title": "X-Api-Key"
            }
          },
          {
            "name": "x-api-secret",
            "in": "header",
            "required": true,
            "schema": {
              "type": "string",
              "title": "X-Api-Secret"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful Response",
            "content": {
              "application/json": {
                "schema": {}
              }
            }
          },
          "422": {
            "description": "Validation Error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/HTTPValidationError"
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "HTTPValidationError": {
        "properties": {
          "detail": {
            "items": {
              "$ref": "#/components/schemas/ValidationError"
            },
            "type": "array",
            "title": "Detail"
          }
        },
        "type": "object",
        "title": "HTTPValidationError"
      },
      "ValidationError": {
        "properties": {
          "loc": {
            "items": {
              "anyOf": [
                {
                  "type": "string"
                },
                {
                  "type": "integer"
                }
              ]
            },
            "type": "array",
            "title": "Location"
          },
          "msg": {
            "type": "string",
            "title": "Message"
          },
          "type": {
            "type": "string",
            "title": "Error Type"
          }
        },
        "type": "object",
        "required": [
          "loc",
          "msg",
          "type"
        ],
        "title": "ValidationError"
      }
    }
  }
}
