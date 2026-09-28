# HTTP and Web Standards

A focused study and practice repository covering **web standards, HTTP, DNS, TCP/IP, web servers, the HTTP request-response model, HTTP methods, headers, status codes, browser-server communication, and APIs**.

This milestone is part of my **freeCodeCamp Back-End Development and APIs Certification** journey.

---

# Overview

The web works through communication between **clients and servers**, following standards that define how browsers, servers, and web technologies should behave.

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

* Web Standards
* Standards Bodies
* W3C
* WHATWG
* ECMA / TC39
* Khronos Group
* HTTP
* DNS
* TCP/IP
* Web servers
* HTTP requests
* HTTP responses
* HTTP methods
* HTTP headers
* HTTP status codes
* XHR / AJAX
* APIs

---

# Web Standards

## What Are Web Standards?

**Web standards** are rules and specifications that define how web technologies should work.

They allow browsers, servers, developers, and other tools to implement web technologies consistently.

Examples include standards related to:

* HTML
* CSS
* JavaScript
* DOM
* SVG
* Web APIs
* WebGL
* Accessibility
* Browser behavior

Without standards, different browsers could interpret the same website differently.

---

# Standards Bodies

Several organizations and groups are responsible for developing and maintaining important web standards.

## W3C

**W3C — World Wide Web Consortium**

The W3C is a major standards organization for the web.

It works on areas including:

* CSS
* SVG
* Accessibility
* Web APIs
* Web standards and guidelines

The W3C uses structured working groups and review processes.

---

## WHATWG

**WHATWG — Web Hypertext Application Technology Working Group**

WHATWG maintains important parts of the web platform, including:

* HTML
* DOM

WHATWG uses a continuously updated **living standard** rather than traditional versioned releases.

---

## ECMA International

**ECMA International** is a standards organization that formally publishes the **ECMAScript** standard that JavaScript implementations are based on.

The technical development of the JavaScript language is handled by:

**TC39 — Technical Committee 39**

TC39 includes delegates from major technology companies and browser vendors.

JavaScript features move through a proposal process before becoming part of the language standard.

---

## TC39 Proposal Process

TC39 uses stages to move JavaScript features from ideas to standardized features.

```text
Stage 0
  ↓
Stage 1
  ↓
Stage 2
  ↓
Stage 3
  ↓
Stage 4
```

### Stage 0

Idea or proposal.

### Stage 1

Proposal is formally explored and its use cases are established.

### Stage 2

The feature is more fully specified.

### Stage 3

The proposal is considered ready for implementation and feedback.

### Stage 4

The proposal has been completed and is ready to become part of the ECMAScript standard.

Examples of JavaScript features that went through this process include:

* `async/await`
* Optional chaining
* ES modules

---

## Khronos Group

The **Khronos Group** is a member-funded consortium focused on:

* Graphics
* Compute
* Media standards

Important web technologies associated with Khronos include:

* WebGL
* WebGL 2

WebGL allows browsers to use GPU-accelerated graphics and 3D rendering.

---

# Creating Web Standards

Although different standards bodies have different processes, the development of a web standard generally follows a similar pattern.

```text
Identify a Need
      ↓
Proposal
      ↓
Specification
      ↓
Review & Iteration
      ↓
Implementation & Testing
      ↓
Finalization
```

---

## 1. Identifying a Need

Standards often begin because developers or browser vendors encounter a problem.

Examples:

* Existing browsers behave differently.
* Developers need a capability that doesn't exist.
* A new web technology needs standardized behavior.

The problem is identified before a formal solution is created.

---

## 2. Proposal and Early Discussion

The idea is written down through something such as:

* GitHub issue
* Explainer
* Technical document
* Community discussion

The goal is to determine:

* Is the problem real?
* Do developers need the feature?
* Are browser vendors interested?
* What possible solutions exist?

---

## 3. Writing the Specification

A **specification**, or **spec**, precisely describes how a feature should behave.

It needs to define:

* Normal behavior
* Edge cases
* Error conditions
* Interactions with existing features
* Security considerations

The goal is for independent engineers to be able to read the specification and implement the same behavior.

---

## 4. Review, Objection, and Iteration

The proposed specification is reviewed.

Browser vendors and other participants can:

* Raise objections
* Suggest changes
* Identify problems
* Request clarification
* Propose alternative approaches

The specification is revised through this process.

---

## 5. Implementation and Testing

Browser vendors begin implementing the feature.

Implementation can reveal problems that were not obvious during specification.

Shared test suites are used to verify that different browsers implement the feature consistently.

```text
Specification
      ↓
Chrome
      ↓
Firefox
      ↓
Safari
      ↓
Shared Tests
```

If browsers behave differently, the specification or implementation may need to be corrected.

---

## 6. Finalization

The feature becomes stable after:

* Multiple implementations exist
* Tests pass
* Interoperability is established
* The community reaches sufficient agreement

Different standards bodies use different finalization processes.

### W3C

A specification can reach **Recommendation** status.

### TC39

A JavaScript feature reaches **Stage 4**.

### WHATWG

The feature becomes part of the continuously updated living standard.

---

# Web Standards Feature Lifecycle

The creation of a standard describes the overall process.

The **feature lifecycle** focuses on what happens to an individual feature.

```text
Proposal
   ↓
Incubation
   ↓
Specification
   ↓
Interoperability Testing
   ↓
Finalization
   ↓
Deprecation
```

---

## Proposal

A problem is identified and a possible solution is proposed.

The proposal may begin as:

* GitHub issue
* Explainer
* Technical discussion

---

## Incubation

The proposal is discussed and tested conceptually.

Developers and browser vendors can:

* Discuss use cases
* Explore alternatives
* Identify problems
* Test different approaches

Some proposals stop during this stage.

---

## Specification

A surviving proposal becomes a formal specification.

The specification defines:

* Behavior
* Edge cases
* Errors
* Interactions
* Security considerations

---

## Interoperability Testing

The feature must work consistently across browsers.

The **Web Platform Tests (WPT)** suite is used to test web platform features.

The goal is interoperability between browsers such as:

* Chrome
* Firefox
* Safari

```text
Specification
      ↓
Implementation
      ↓
Web Platform Tests
      ↓
Chrome / Firefox / Safari
      ↓
Consistent Behavior
```

---

## Finalization

Once implementations are stable and tests pass, the feature becomes part of the web platform.

Different organizations use different terminology:

```text
W3C
Recommendation

TC39
Stage 4

WHATWG
Living Standard
```

---

## Deprecation

Some web features eventually become outdated or are replaced by better alternatives.

A feature may be **deprecated**, meaning developers are encouraged to stop using it.

Deprecated features may remain supported for a long time because browsers prioritize **backwards compatibility**.

---

# Principles of Web Standards

Web standards are built around several important principles.

---

## Openness

Web standards are developed openly and implemented royalty-free.

This allows:

* Developers to read specifications
* Browser vendors to implement standards
* Developers to build web technologies
* Different organizations to participate

---

## Accessibility

The web should be usable by people with different abilities.

Accessibility affects:

* HTML
* CSS
* Browser behavior
* User interfaces
* Assistive technologies

Important accessibility concepts include:

* Screen readers
* Keyboard navigation
* Assistive technology

The W3C's **WCAG** guidelines provide accessibility guidance.

---

## Interoperability

A website should behave consistently across different browsers and platforms.

For example:

```text
Chrome
   ↓
Firefox
   ↓
Safari
   ↓
Same Web Standard
   ↓
Consistent Behavior
```

Interoperability prevents developers from having to create completely different implementations for every browser.

---

## Backwards Compatibility

The web aims to avoid breaking existing websites.

Older websites should continue to work in modern browsers.

This is one reason deprecated technologies can remain supported for many years.

---

## Privacy and Security

Modern web standards consider:

* User privacy
* Data protection
* Security
* Tracking
* Sensitive information

New APIs and features can receive additional scrutiny when they could expose user information or create security risks.

---

## Layering

The web is built from different layers.

```text
HTML
Structure
   ↓
CSS
Presentation
   ↓
JavaScript
Behavior
```

This separation allows technologies to work together without requiring everything to depend on one layer.

---

## Progressive Enhancement

Progressive enhancement means a website should provide a functional experience first and then improve when additional capabilities are available.

Simplified:

```text
Basic Experience
      ↓
CSS Enhancement
      ↓
JavaScript Enhancement
      ↓
Advanced Browser Features
```

A feature should ideally degrade gracefully when it is not supported.

---

# What Is a Server?

A **server** is a computer or program that provides services or resources to clients.

A web server can:

* Receive HTTP requests
* Process requests
* Run application code
* Access databases
* Retrieve files
* Generate responses
* Send responses back to clients

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

# Client and Server

A **client** requests resources or services.

Examples:

* Web browser
* Mobile application
* Desktop application
* API client

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

# DNS

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

DNS allows users to access websites using domain names rather than remembering IP addresses.

---

# Why DNS Is Needed

Computers communicate using IP addresses.

Humans prefer domain names.

```text
Human
  ↓
example.com
  ↓
DNS
  ↓
IP Address
  ↓
Server
```

DNS acts as a naming system for internet resources.

---

# TCP/IP

**TCP/IP** is the fundamental networking protocol suite used for communication across the internet.

## IP

**Internet Protocol**

Responsible for:

* Addressing
* Routing packets between devices

## TCP

**Transmission Control Protocol**

Provides:

* Reliable delivery
* Ordered delivery
* Communication between applications

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

# HTTP

**HTTP** stands for:

**Hypertext Transfer Protocol**

HTTP is an application-layer protocol used for communication between clients and servers.

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

* HTML
* CSS
* JavaScript
* Images
* JSON
* XML
* Plain text
* Other resources

---

# HTTP Request

A request is sent by the client to the server.

Basic request structure:

```http
GET /index.html HTTP/1.1
Host: example.com
```

An HTTP request can contain:

* Method
* URL/path
* HTTP version
* Headers
* Optional body

---

# HTTP Methods

| Method    | Purpose                                    |
| --------- | ------------------------------------------ |
| `GET`     | Retrieve data                              |
| `POST`    | Submit/create data                         |
| `PUT`     | Replace/update a resource                  |
| `PATCH`   | Partially update a resource                |
| `DELETE`  | Delete a resource                          |
| `HEAD`    | Retrieve headers without the response body |
| `OPTIONS` | Discover supported communication options   |

Example:

```http
GET /users
```

This means the client is requesting the users resource.

---

# HTTP Request Example

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
HTTP Method

/users
  ↓
Requested Resource

Host
  ↓
Target Server

Content-Type
  ↓
Type of Request Body

JSON
  ↓
Data Being Sent
```

---

# HTTP Response

The server responds to the request.

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html

<h1>Hello World</h1>
```

An HTTP response contains:

* Status code
* Status message/reason phrase
* Headers
* Optional body

---

# Request-Response Model

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

# HTTP Headers

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

Example:

```http
GET /api/users HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer token
```

---

# Content-Type

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

This means the body contains JSON data.

---

# HTTP Status Codes

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

# Common 2xx Status Codes

## 200 OK

Request succeeded.

```http
HTTP/1.1 200 OK
```

## 201 Created

A new resource was successfully created.

```http
HTTP/1.1 201 Created
```

## 204 No Content

Request succeeded but there is no response body.

---

# Common 3xx Status Codes

## 301 Moved Permanently

The resource has permanently moved to another URL.

## 302 Found

The resource is temporarily available at another URL.

## 304 Not Modified

The cached version can be used because the resource has not changed.

---

# Common 4xx Status Codes

These generally indicate a problem with the client's request.

## 400 Bad Request

The request is invalid or malformed.

## 401 Unauthorized

Authentication is required or has failed.

## 403 Forbidden

The server understood the request but refuses access.

## 404 Not Found

The requested resource could not be found.

## 405 Method Not Allowed

The HTTP method is not supported for the requested resource.

## 429 Too Many Requests

The client has sent too many requests in a given period.

---

# Common 5xx Status Codes

These generally indicate a server-side problem.

## 500 Internal Server Error

A generic server-side error.

## 502 Bad Gateway

A server acting as a gateway or proxy received an invalid response from an upstream server.

## 503 Service Unavailable

The server is temporarily unable to handle the request.

## 504 Gateway Timeout

An upstream server did not respond within the required time.

---

# Status Code Quick Reference

| Code  | Meaning               |
| ----- | --------------------- |
| `200` | OK                    |
| `201` | Created               |
| `204` | No Content            |
| `301` | Moved Permanently     |
| `302` | Found                 |
| `304` | Not Modified          |
| `400` | Bad Request           |
| `401` | Unauthorized          |
| `403` | Forbidden             |
| `404` | Not Found             |
| `405` | Method Not Allowed    |
| `429` | Too Many Requests     |
| `500` | Internal Server Error |
| `502` | Bad Gateway           |
| `503` | Service Unavailable   |
| `504` | Gateway Timeout       |

---

# HTTP Request Cycle

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

# HTTP and APIs

HTTP is widely used for APIs.

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

# XHR

**XHR** stands for:

**XMLHttpRequest**

It is a browser API that allows JavaScript to communicate with a server without requiring a full page reload.

XHR can:

* Send requests
* Receive data
* Update webpages dynamically
* Communicate with APIs
* Work asynchronously

Despite its name, XHR is not limited to XML.

It can work with:

* JSON
* HTML
* CSS
* XML
* Plain text
* Other data formats

---

# AJAX

**AJAX** stands for:

**Asynchronous JavaScript and XML**

It describes the technique of using JavaScript to communicate with a server asynchronously and update a webpage without a full reload.

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

# Complete Web Communication Model

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

# Important Distinctions

## DNS

```text
Domain Name → IP Address
```

## IP

```text
Addressing + Routing
```

## TCP

```text
Reliable Transport
```

## HTTP

```text
Application-Level Web Communication
```

## Server

```text
Receives Requests
       ↓
Processes Requests
       ↓
Returns Responses
```

---

# Key Takeaways

The most important concepts:

* Web standards define how web technologies should behave.
* W3C works on areas including CSS, SVG, accessibility, and web technologies.
* WHATWG maintains HTML and the DOM as living standards.
* ECMA International publishes the ECMAScript standard.
* TC39 develops the JavaScript language standard.
* Khronos works on graphics standards including WebGL.
* Web standards generally move through proposal, specification, implementation, testing, and finalization.
* Web features can eventually be deprecated.
* Openness, accessibility, interoperability, backwards compatibility, privacy, security, layering, and progressive enhancement are important web principles.
* HTTP enables communication between clients and servers.
* A client sends requests.
* A server processes requests and sends responses.
* DNS translates domain names into IP addresses.
* IP handles addressing and routing.
* TCP provides reliable, ordered transport.
* HTTP requests contain methods, paths, headers, and sometimes bodies.
* HTTP responses contain status codes, headers, and sometimes bodies.
* `GET` retrieves resources.
* `POST` submits or creates data.
* `PUT` replaces a resource.
* `PATCH` partially updates a resource.
* `DELETE` removes a resource.
* `2xx` indicates success.
* `3xx` indicates redirection.
* `4xx` generally indicates client-side request errors.
* `5xx` generally indicates server-side errors.
* XHR allows browser JavaScript to communicate with servers without a full page reload.
* AJAX describes asynchronous browser-server communication.
* APIs commonly use HTTP to exchange data such as JSON.

---

# Practical Skills

By completing this milestone, I should be able to:

* Explain how web standards are created
* Identify major web standards bodies
* Explain the role of W3C
* Explain the role of WHATWG
* Explain the role of ECMA and TC39
* Explain the role of Khronos
* Explain the lifecycle of a web standard feature
* Explain interoperability
* Explain backwards compatibility
* Explain progressive enhancement
* Explain the role of a server
* Explain DNS at a high level
* Explain TCP/IP at a high level
* Explain HTTP
* Understand the HTTP request-response model
* Identify HTTP request components
* Identify HTTP response components
* Understand common HTTP methods
* Understand HTTP headers
* Interpret common HTTP status codes
* Understand browser-server communication
* Understand XHR
* Understand AJAX
* Understand how HTTP is used by APIs

---

# Learning Checklist

## Web Standards

* [x] Understanding how standards bodies operate
* [x] Understanding the process for creating web standards
* [x] Understanding the lifecycle of web standard features
* [x] Understanding the key principles of web standards
* [x] W3C
* [x] WHATWG
* [x] ECMA / TC39
* [x] Khronos Group
* [x] Web Platform Tests
* [x] Interoperability
* [x] Backwards compatibility
* [x] Progressive enhancement

## Networking and HTTP

* [x] Understanding how HTTP, DNS and TCP/IP work
* [x] What Is a Server and How Does It Work?
* [x] What Is DNS?
* [x] What Are TCP/IP and HTTP?
* [x] Basic HTTP Syntax
* [x] Common HTTP Response Codes
* [x] Understanding the HTTP Request-Response Model
* [x] HTTP Requests
* [x] HTTP Responses
* [x] HTTP Methods
* [x] HTTP Headers
* [x] XHR
* [x] AJAX
* [x] HTTP and APIs
* [x] HTTP and Web Standards Review
* [x] HTTP and Web Standards Quiz

---

# Certification Progress

**Course:** freeCodeCamp Back-End Development and APIs

**Section:** HTTP and Web Standards

**Status:** Completed

---

# Core Principle

> **Web standards define how the web should behave, while HTTP provides the communication system through which clients and servers exchange resources and data.**

```text
Web Standards
      ↓
Consistent Web Behavior
      ↓
DNS
      ↓
TCP/IP
      ↓
HTTP
      ↓
Request → Server → Response
      ↓
Web Application
```
