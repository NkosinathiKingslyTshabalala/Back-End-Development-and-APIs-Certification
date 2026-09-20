# HTTP and Web Standards

A focused study and practice repository covering **HTTP, DNS, TCP/IP, web servers, the HTTP request-response model, HTTP methods, headers, status codes, and browser-server communication**.

This milestone is part of my **freeCodeCamp Back-End Development and APIs Certification** journey.

---

## Overview

The web works through communication between **clients and servers**.

A simplified model:

```text
Client
  ↓
DNS
  ↓
Server
  ↓
HTTP Request
  ↓
Application
  ↓
HTTP Response
  ↓
Client
```

The main technologies covered in this milestone are:

- HTTP
- DNS
- TCP/IP
- Web servers
- HTTP requests
- HTTP responses
- HTTP methods
- HTTP headers
- HTTP status codes
- XHR / AJAX

---

# What I Learned

## 1. What Is a Server?

A **server** is a computer or program that provides services or resources to clients.

A web server can:

- Receive HTTP requests
- Process requests
- Run application code
- Access databases
- Retrieve files
- Generate responses
- Send responses back to clients

Simplified:

```text
Client
   ↓
Request
   ↓
Web Server
   ↓
Application
   ↓
Database / Files
   ↓
Response
   ↓
Client
```

---

# 2. Client and Server

A **client** requests resources or services.

Examples:

- Web browser
- Mobile application
- Desktop application
- API client

A **server** processes requests and provides responses.

Example:

```text
Browser
   ↓
GET /index.html
   ↓
Web Server
   ↓
index.html
   ↓
Browser
```

---

# 3. DNS

**DNS** stands for:

**Domain Name System**

DNS translates human-readable domain names into IP addresses.

Example:

```text
example.com
     ↓
    DNS
     ↓
93.184.216.34
```

This allows users to access websites using names instead of remembering IP addresses.

---

# 4. Why DNS Is Needed

Computers communicate using IP addresses.

Humans prefer domain names.

```text
Human
  ↓
example.com
  ↓
DNS
  ↓
IP address
  ↓
Server
```

DNS acts like a naming system for internet resources.

---

# 5. TCP/IP

**TCP/IP** is the fundamental networking protocol suite used for communication across the internet.

### IP

**Internet Protocol**

Responsible for addressing and routing packets between devices.

### TCP

**Transmission Control Protocol**

Provides reliable, ordered delivery of data between applications.

Simplified:

```text
Application
    ↓
TCP
    ↓
IP
    ↓
Network
```

---

# 6. HTTP

**HTTP** stands for:

**Hypertext Transfer Protocol**

HTTP is an application-layer protocol used for communication between clients and servers.

Example:

```text
Client
  ↓
HTTP Request
  ↓
Server
  ↓
HTTP Response
  ↓
Client
```

HTTP is commonly used to transfer:

- HTML
- CSS
- JavaScript
- Images
- JSON
- XML
- Plain text
- Other resources

---

# 7. HTTP Request

A request is sent by the client to the server.

Basic request structure:

```http
GET /index.html HTTP/1.1
Host: example.com
```

An HTTP request can contain:

- Method
- URL/path
- HTTP version
- Headers
- Optional body

---

# 8. HTTP Methods

Common HTTP methods:

| Method | Purpose |
|---|---|
| `GET` | Retrieve data |
| `POST` | Submit/create data |
| `PUT` | Replace/update a resource |
| `PATCH` | Partially update a resource |
| `DELETE` | Delete a resource |
| `HEAD` | Retrieve headers without the response body |
| `OPTIONS` | Discover supported communication options |

Example:

```http
GET /users
```

means the client is requesting the users resource.

---

# 9. HTTP Request Example

```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "name": "John",
  "age": 25
}
```

Breakdown:

```text
POST
  ↓
HTTP method

/users
  ↓
Requested resource

Host
  ↓
Target server

Content-Type
  ↓
Type of request body

JSON
  ↓
Data being sent
```

---

# 10. HTTP Response

The server responds to the request.

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html

<h1>Hello World</h1>
```

An HTTP response contains:

- Status code
- Status message/reason phrase
- Headers
- Optional body

---

# 11. Request-Response Model

The basic HTTP cycle:

```text
1. Client sends request
          ↓
2. Server receives request
          ↓
3. Server processes request
          ↓
4. Server generates response
          ↓
5. Server sends response
          ↓
6. Client receives response
```

Example:

```text
Browser
   │
   │ GET /index.html
   ↓
Server
   │
   │ Process request
   ↓
Server
   │
   │ 200 OK + HTML
   ↓
Browser
```

---

# 12. HTTP Headers

Headers provide additional information about requests and responses.

Example:

```http
Content-Type: application/json
```

Common headers include:

```text
Host
Content-Type
Content-Length
Authorization
Accept
User-Agent
Cache-Control
Cookie
Set-Cookie
Location
```

### Example

```http
GET /api/users HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer token
```

---

# 13. Content-Type

`Content-Type` tells the receiver what type of data is being sent.

Examples:

```text
text/html
text/plain
text/css
application/json
application/xml
image/jpeg
```

Example:

```http
Content-Type: application/json
```

means the body contains JSON data.

---

# 14. HTTP Status Codes

HTTP status codes indicate the result of a request.

They are grouped into five categories:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client Error
5xx → Server Error
```

---

# 15. Common 2xx Status Codes

### 200 OK

Request succeeded.

```http
HTTP/1.1 200 OK
```

### 201 Created

A new resource was successfully created.

```http
HTTP/1.1 201 Created
```

### 204 No Content

Request succeeded but there is no response body.

---

# 16. Common 3xx Status Codes

### 301 Moved Permanently

The resource has permanently moved to another URL.

### 302 Found

The resource is temporarily available at another URL.

### 304 Not Modified

The cached version can be used because the resource has not changed.

---

# 17. Common 4xx Status Codes

These generally indicate a problem with the client's request.

### 400 Bad Request

The request is invalid or malformed.

### 401 Unauthorized

Authentication is required or has failed.

### 403 Forbidden

The server understood the request but refuses access.

### 404 Not Found

The requested resource could not be found.

### 405 Method Not Allowed

The HTTP method is not supported for the requested resource.

### 429 Too Many Requests

The client has sent too many requests in a given period.

---

# 18. Common 5xx Status Codes

These generally indicate a server-side problem.

### 500 Internal Server Error

A generic server-side error.

### 502 Bad Gateway

A server acting as a gateway/proxy received an invalid response from an upstream server.

### 503 Service Unavailable

The server is temporarily unable to handle the request.

### 504 Gateway Timeout

An upstream server did not respond within the required time.

---

# 19. Status Code Quick Reference

| Code | Meaning |
|---|---|
| `200` | OK |
| `201` | Created |
| `204` | No Content |
| `301` | Moved Permanently |
| `302` | Found |
| `304` | Not Modified |
| `400` | Bad Request |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not Found |
| `405` | Method Not Allowed |
| `429` | Too Many Requests |
| `500` | Internal Server Error |
| `502` | Bad Gateway |
| `503` | Service Unavailable |
| `504` | Gateway Timeout |

---

# 20. HTTP Request Circle

A webpage normally requires multiple HTTP requests.

Example:

```text
Browser
   │
   ├── GET HTML
   │       ↓
   │     Server
   │       ↓
   │     HTML
   │
   ├── GET CSS
   │       ↓
   │     Server
   │       ↓
   │      CSS
   │
   ├── GET JavaScript
   │       ↓
   │     Server
   │       ↓
   │      JS
   │
   └── GET Image
           ↓
         Server
           ↓
         Image
```

The browser combines these resources to render the webpage.

---

# 21. HTTP and APIs

HTTP is also widely used for APIs.

Example:

```http
GET /api/users
```

Response:

```json
[
  {
    "id": 1,
    "name": "John"
  }
]
```

The client and server communicate using HTTP while transferring structured data such as JSON.

---

# 22. XHR

**XHR** stands for:

**XMLHttpRequest**

It is a browser API that allows JavaScript to communicate with a server without requiring a full page reload.

XHR can:

- Send requests
- Receive data
- Update webpages dynamically
- Communicate with APIs
- Work asynchronously

Despite its name, XHR is not limited to XML.

It can work with:

- JSON
- HTML
- CSS
- XML
- Plain text
- Other data formats

---

# 23. AJAX

**AJAX** stands for:

**Asynchronous JavaScript and XML**

It describes the general technique of using JavaScript to communicate with a server asynchronously and update a webpage without a full reload.

Simplified:

```text
Webpage
   ↓
JavaScript
   ↓
HTTP Request
   ↓
Server
   ↓
HTTP Response
   ↓
JavaScript
   ↓
Update Page
```

Modern applications commonly use `fetch()` instead of the older XHR API.

---

# 24. Complete Web Communication Model

```text
User
 ↓
Browser
 ↓
Domain Name
 ↓
DNS
 ↓
IP Address
 ↓
TCP/IP
 ↓
Server
 ↓
HTTP Request
 ↓
Web Application
 ↓
Database / Files
 ↓
HTTP Response
 ↓
Browser
 ↓
Rendered Webpage
```

---

# 25. Important Distinctions

### DNS

```text
Domain name → IP address
```

### IP

```text
Addressing + routing
```

### TCP

```text
Reliable transport
```

### HTTP

```text
Application-level web communication
```

### Server

```text
Receives requests + processes them + returns responses
```

---

# Key Takeaways

The most important concepts:

- HTTP enables communication between clients and servers.
- A client sends requests.
- A server processes requests and sends responses.
- DNS translates domain names into IP addresses.
- IP handles addressing and routing.
- TCP provides reliable, ordered transport.
- HTTP requests contain methods, paths, headers, and sometimes bodies.
- HTTP responses contain status codes, headers, and sometimes bodies.
- `GET` retrieves resources.
- `POST` submits or creates data.
- `PUT` replaces a resource.
- `PATCH` partially updates a resource.
- `DELETE` removes a resource.
- `2xx` indicates success.
- `3xx` indicates redirection.
- `4xx` generally indicates client-side request errors.
- `5xx` generally indicates server-side errors.
- XHR allows browser JavaScript to communicate with servers without a full page reload.
- APIs commonly use HTTP to exchange data such as JSON.

---

# Practical Skills

By completing this milestone, I should be able to:

- Explain how the web communicates
- Explain the role of a server
- Explain DNS at a high level
- Explain TCP/IP at a high level
- Explain HTTP
- Understand the HTTP request-response model
- Identify HTTP request components
- Identify HTTP response components
- Understand common HTTP methods
- Understand HTTP headers
- Interpret common HTTP status codes
- Understand browser-server communication
- Understand XHR
- Understand AJAX
- Understand how HTTP is used by APIs

---

# Learning Checklist

- [x] Understanding how HTTP, DNS and TCP/IP work
- [x] What Is a Server and How Does It Work?
- [x] What Is DNS?
- [x] What Are TCP/IP and HTTP?
- [x] Basic HTTP Syntax
- [x] Common HTTP Response Codes
- [x] Understanding the HTTP Request-Response Model
- [x] HTTP Requests
- [x] HTTP Responses
- [x] HTTP Methods
- [x] HTTP Headers
- [x] XHR
- [x] AJAX
- [x] HTTP and APIs
- [x] HTTP and Web Standards Review
- [x] HTTP and Web Standards Quiz

---

# Certification Progress

**Course:** freeCodeCamp Back-End Development and APIs

**Section:** HTTP and Web Standards

**Status:** Completed

---

## Core Principle

> **The web works through a request-response cycle: DNS finds the server, TCP/IP handles network communication, HTTP defines the messages, and the server processes the request and returns a response.**