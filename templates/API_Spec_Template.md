# 🔗 API Spec: [Nama Endpoint]

## Overview
- **Path**: `/v1/...`
- **Method**: `GET|POST|PUT|DELETE`
- **Auth**: `Required|Optional`

## Request
### Headers
```json
{ "Authorization": "Bearer <token>" }
```
### Body
```json
{ "key": "value" }
```

## Response
### 200 OK
```json
{ "status": "success", "data": {} }
```
### 400 Bad Request
```json
{ "error": "invalid_input" }
```