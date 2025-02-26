---
tags:
  - Sharejob
  - ionic
  - push
Created: Invalid date
Updated: Invalid date
---
curl -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJiODA2NjkwNi1iMjVlLTQzYWEtYTE2My03N2QyMDc3OWQxYTYifQ.coEYEcI7I7_kPktos8vODa5XaUrHbGGnkYp8fvrT9ts" [https://api.ionic.io/auth/test](https://api.ionic.io/auth/test)

curl -X POST -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJiODA2NjkwNi1iMjVlLTQzYWEtYTE2My03N2QyMDc3OWQxYTYifQ.coEYEcI7I7_kPktos8vODa5XaUrHbGGnkYp8fvrT9ts" -H "Content-Type: application/json" -d '{

"tokens": ["DEV-30e20f56-bf56-46c6-8def-58f8844ae6df"],

"profile": "dev",

"notification": { "message": "Hello World!" }  
}' "  

[https://api.ionic.io/push/notifications](https://api.ionic.io/push/notifications)

"