---
layout: home
title: Home
nav_order: 0
---

# Email over HTTP for Test Environments

cinotify provides a notification service for restricted environments
with limited resources and permissions.

Typically, continuous integration tests and builds run within a docker container that does not have access to send mail over SMTP. Additionally, this service provides a way to send notifications without leaking SMTP credentials of your company domain to a build environment.

```bash
curl --request POST 'https://www.cinotify.cc/api/notify' \
  -d "to=example@example.com&subject=email body&body=<em>hello</em>.&type=text/html&attachments[][type]=text/plain&attachments[][content]=aGVsbG8sIHdvcmxkIQ==&attachments[][filename]=hello.txt"
```
