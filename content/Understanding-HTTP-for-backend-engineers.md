+++
title = "Understanding HTTP for Backend Engineers"
date = 2025-08-30
description = "Contains information about the HTTP things..."
+++

## 1. Random information:
- Client is responsible for any headers, ui etc
- Http protocol states that client should always initiate the connection.
- `https` is the more secured version of `http`
- Their should be a connection mechanism between client and server. In order to establish that http uses `TCP`.
*Note*: `TCP` and `UDP` are the most used transfer protocols on the internet. Among them `TCP` is the most reliable one.

**The 7 Layers of OSI model**
This is often referred when sending or receiving data.
<img src="/assets/levelsofosimodel.png" alt="OSI 7 Layers Explained the Easy Way" width="400" height="50" style="max-width: 300px; height: 600px;">

- Most of these layers fall under network engineering concepts.
- In http 1.1 persistent connections is introduced.
- In http 2.0 multiplexing is introduced.
- In http 3.0 it is designed over udp instead of tcp. It support
Client and server are connected and information is `client`

Request is sent by the client and response is received by the client

## 2. HTTP messages
### Request
```json
PUT: /api/users/12345/ HTTP/1.1
Host: example.com
User-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
AppleWebKit/537.36(KHTML, like Gecko) Chrome/93.0.4577.82
Safari/537.36
Content-Type: application/json
Content-Length: 123
Authorization: Bearer
eyJhbGci0iJIUzI1NiIsInR5cCI6IkpXVCJ9...
Accept: application/json
Accept-Encoding: keep-alive
Referer: https://example.com/dashboard
Cookie: sessionId=abc123xyx456; lang-en-US
// The above are headers
//  a blank line here means, everything has been sent
{
	"firstName": "John",
	"lastName": "Doe",
	"email": "john.doc@example.com",
	"age": 30
}
```
### Response
```json
HTTP/1.1 200 OK
Date: Fri, 20 Sep 2024 12:00:00 GMT
Content-Type: application/json
Content-Length: 85
Server: Apache/2.4.41 (Ubuntu)
Cache-Control: no-store
X-Request-ID: abcdef123456
Strict-Transport-Security: max-age=31536000;
includeSubDomains: preload
Set-Cookie: sessionId=abc123xyz456; path=/; Secure;
HttpOnly
Vary: Accept-Encoding
Connection: keep-alive

// a blank line here means, everything has been sent
// this the response body
{
	"message": "User updated successfully",
	"userId": 12345,
	"status": "success"
}
```
## 3. Types of Headers
  1. **Request Headers**
     1. User-Agent - for identirfying client
     2. Authorization - diff credentials bearer tokens
     3. Cookie
     4. Accept - what type of content our client accpets
  2. **General Headers**: somekind of info about the Header
     1. Date
     2. Cache-control
     3. connection: whether to keep it alive or close it
  3. **Representation Headers**
     1. Content-Type: type i.e json, html etc
     2. Content-Length: size of resource in bytes
     3. Content-Encoding: deeplayer
     4. ETag
  4. **Security Headers**
     1. Strict-Transport-Security(HSTS): client only communicates over https
     2. Content-Security-Policy(CSP): Helping prevent cross site scripting attacks
     3. X-Frame-Options:
     4. X-Content-Type-Options: preventing mining attacks
     5. Set-Cookie:
  5. **Custom headers**

## 4. HTTP Methods
- Methods define the **intent** of the interactions

  1. **GET** - fetch the data from the server. It shouldn't modify anything on the server.
  2. **POST** - create some data in the server. post req has a body(bcz how else can we send the data to the server.)
  3. **PUT** - Update data but the entire data need to be replaced. *PUT is the complete replacement*
  4. **PATCH** - Patch is like append method i.e we can just add new data but in case of put we need to replace everything. Patch is selective replacement
  5.  **DELETE** - Remove everything
- <span style="color: yellow;">**Rule of thumb**</span>: Always use Patch method. Unless you have an explicit usecase with PUT

## 5. Idempotent vs. Non-idempotent
