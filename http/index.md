---
title: HTTP API
layout: page
permalink: /docs/http/
---

# HTTP API

The HTTP API is how emails are sent from Continuous Integration environments.

## `POST /api/notify`

### Parameters

| name        | type   | required                      |
| ----------- | ------ | ----------------------------- |
| to          | string | true                          |
| subject     | string | true                          |
| body        | string | false (default: ' ')          |
| attachments | array  | false (default: undefined)    |
| type        | string | false (default: 'text/plain') |

#### Attachments

| name     | type   | required | description                                  |
| -------- | ------ | -------- | -------------------------------------------- |
| type     | string | true     | The content's MIME type                      |
| content  | string | true     | The Base64 encoded content of the attachment |
| filename | string | true     | The attachment's filename                    |

### Example

#### application/x-www-form-urlencoded

```bash
curl --request POST 'https://www.cinotify.cc/api/notify' \
  -d "to=example@example.com&subject=building main&body=hello.&attachments[][type]=text/plain&attachments[][content]=aGVsbG8sIHdvcmxkIQ==&attachments[][filename]=hello.txt"
```

#### json

```bash
curl -X POST 'https://www.cinotify.cc/api/notify' \
  -H "Content-Type: application/json" \
  -d '{
    "to": "example@example.com",
    "subject": "building main",
    "body": "hello.",
    "attachments": [
      {
        "type": "text/plain",
        "content": "aGVsbG8sIHdvcmxkIQ==",
        "filename": "hello.txt"
      }
    ]
  }'
```

#### HTML Email

```bash
curl -X POST 'https://www.cinotify.cc/api/notify' \
  -H "Content-Type: application/json" \
  -d '{
    "body": "<em>hello</em>",
    "subject": "example html email",
    "to": "example@example.com",
    "type": "text/html"
  }'
```
