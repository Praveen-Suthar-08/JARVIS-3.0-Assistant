# 📡 JARVIS 3.0 — API & Web Interface Documentation

Welcome to the official **API & Developer Specification** for **JARVIS 3.0 (Mark LV)**, created by **Praveen Suthar**.

This document outlines the WebSocket protocol, REST API endpoints, security & encryption mechanisms, authentication headers, and payload structures used by the JARVIS Remote Control Dashboard and client SDKs.

---

## 🔒 1. Authentication & Security Architecture

JARVIS 3.0 uses a dual-layer authentication and security model:

1. **Bearer Token Authentication:** Every HTTP request and WebSocket connection requires a valid temporary session token generated during PIN passcode authentication.
2. **AES-256-CBC Payload Encryption:** Sensitive text payloads sent over WebSocket can be encrypted on the client side using CryptoJS with a key derived from the session PIN.

### Session Headers
```http
Authorization: Bearer <SESSION_TOKEN>
Content-Type: application/json
```

---

## 🌐 2. REST API Endpoints

### 🔑 Authentication Endpoint (`POST /login`)
Authenticates a user with a 6-digit session passcode.

- **Request Body:**
  ```json
  {
    "pin": "123456"
  }
  ```
- **Response (200 OK):**
  ```json
  {
    "ok": true,
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6..."
  }
  ```
- **Error Response (401 Unauthorized):**
  ```json
  {
    "ok": false,
    "error": "Invalid or expired key"
  }
  ```

---

### 📱 Device Auto-Login (`POST /api/device-login`)
Authenticates paired mobile devices using a stored persistent device token.

- **Request Body:**
  ```json
  {
    "device_token": "dev_tok_98f7a6b5c4d3e2f1"
  }
  ```
- **Response (200 OK):**
  ```json
  {
    "ok": true,
    "key": "123456",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6..."
  }
  ```

---

### 📤 File Upload (`POST /api/upload`)
Uploads a file to JARVIS for local storage, processing, or document summarization.

- **Headers:** `Authorization: Bearer <TOKEN>`
- **Body:** `multipart/form-data` with form field `file`.
- **Response (200 OK):**
  ```json
  {
    "ok": true,
    "filename": "document.pdf",
    "size": 1048576,
    "path": "C:\\Users\\...\\Downloads\\document.pdf"
  }
  ```

---

### 📥 File Download (`GET /api/download/<filename>`)
Downloads a file from the server's output directory.

- **Query Parameters:** `?token=<SESSION_TOKEN>`
- **Response:** Raw binary file content stream.

---

## ⚡ 3. WebSocket Real-Time Interface

- **Endpoint:** `wss://<HOST>:<PORT>/ws?token=<SESSION_TOKEN>`

### Client -> Server Messages

#### Plain Text Command:
```json
{
  "type": "text",
  "text": "Open Chrome and search for quantum computing news"
}
```

#### Encrypted Text Command (AES-256):
```json
{
  "type": "text_encrypted",
  "payload": "Base64EncodedAES256CiphertextHere=="
}
```

#### Wake Signal:
```json
{
  "type": "wake"
}
```

---

### Server -> Client Messages

#### Log Broadcast:
```json
{
  "type": "log",
  "speaker": "jarvis",
  "text": "Opening Google Chrome and fetching quantum computing headlines now."
}
```

#### Status Broadcast:
```json
{
  "type": "status",
  "state": "active" // "active" | "sleeping"
}
```

#### System Notification:
```json
{
  "type": "sys",
  "text": "Remote session active."
}
```

#### File Received Notification:
```json
{
  "type": "file_received",
  "filename": "report.pdf",
  "size": 204800
}
```

---

## 👨‍💻 Developer Notice

Designed and maintained by **Praveen Suthar**.  
Repository: [https://github.com/Praveen-Suthar-08/JARVIS-3.0-Assistant.git](https://github.com/Praveen-Suthar-08/JARVIS-3.0-Assistant.git)
