# REST APIs, Web Services and Microservices

These notes cover three topics from the freeCodeCamp Back-End Development and APIs Certification:

1. How Web Services Work
2. REST Architecture and How It Works
3. Microservices

---

# 1. Web Services

## What Is an API?

**API** stands for **Application Programming Interface**.

An API allows different software applications to communicate with each other.

Example:

A weather application requests weather information from a server through an API.

```text
Weather App
     ↓
    API
     ↓
Weather Server
     ↓
 Weather Data
     ↓
Weather App
```

## What Is a Web Service?

A **web service** is a type of API that uses web technologies to exchange data over a network, usually the internet.

A web service acts as a bridge between software applications.

It focuses on exchanging data and functionality rather than providing a user interface for people to interact with directly.

### API vs Web Service

- **API:** A general interface that allows software to communicate.
- **Web service:** A type of API that uses web technologies to communicate over a network.

**Remember:** Every web service is an API, but not every API is a web service.

## Characteristics of Web Services

| Characteristic | Meaning |
|---|---|
| Runs on a server | Hosted on a server and exposes data or functionality |
| Machine-to-machine communication | Allows software applications to exchange information |
| Language-agnostic | Applications written in different programming languages can communicate |
| Platform-agnostic | Different operating systems can communicate with the service |
| Uses standard protocols | Commonly uses HTTP/HTTPS to exchange data |

Example:

A mobile app written in Java can communicate with a web service written in JavaScript.

The applications do not need to use the same programming language.

## Types of Web Services

### REST

REST stands for **Representational State Transfer**.

- Uses standard web technologies, including HTTP.
- Organizes data around resources.
- Commonly returns JSON.
- Widely used for modern web and mobile applications.

### SOAP

SOAP stands for **Simple Object Access Protocol**.

- A messaging protocol.
- Uses XML messages.
- Often used in enterprise systems that require structured communication standards.

Example:

```xml
<soapenv:Envelope>
  <soapenv:Body>
    <getUser>
      <userId>20</userId>
    </getUser>
  </soapenv:Body>
</soapenv:Envelope>
```

### XML-RPC

- Uses XML to encode requests and responses.
- Allows applications to invoke operations remotely.

### UDDI

**UDDI** stands for Universal Description, Discovery, and Integration.

It is a directory for describing and discovering web services, rather than a service that directly handles ordinary application data exchange.

---

# 2. REST Architecture

## What Is REST?

REST stands for **Representational State Transfer**.

REST is an architectural style that defines guidelines for communication between clients and servers.

**REST is not a protocol.** It uses existing technologies such as HTTP and URLs.

REST APIs are commonly used to build web services.

## What Is a REST API?

A REST API exposes **resources** that clients can access or modify through HTTP requests.

A resource is a piece of data or an entity in an application.

Examples:

```text
/users
/products
/orders
```

Individual resources can be identified using IDs:

```text
/users/20
/products/5
/orders/100
```

### Resource Examples

| URL | Resource |
|---|---|
| `/users` | Collection of users |
| `/users/20` | User with ID 20 |
| `/products` | Collection of products |
| `/products/5` | Product with ID 5 |
| `/users/20/orders` | Orders associated with user 20 |

## JSON and XML Representations

A resource can be represented in different formats.

### JSON

```json
{
  "id": 20,
  "name": "John Doe",
  "email": "john@example.com",
  "role": "admin"
}
```

### XML

```xml
<user>
  <id>20</id>
  <name>John Doe</name>
  <email>john@example.com</email>
  <role>admin</role>
</user>
```

JSON is commonly used by REST APIs, but REST is not limited to JSON.

## HTTP Headers

HTTP headers carry additional information about a request or response.

The `Accept` header tells the server which response formats the client can accept.

Requesting JSON:

```http
Accept: application/json
```

Requesting XML:

```http
Accept: application/xml
```

The server uses this information when deciding which representation to return, if it supports the requested format.

---

# 3. Core REST Principles

## 3.1 Client-Server Architecture

The client and server have separate responsibilities.

- **Client:** Requests resources and displays or processes responses.
- **Server:** Processes requests and provides resources.

```text
Client
  │
  │ HTTP Request
  ↓
Server
  │
  │ HTTP Response
  ↓
Client
```

This separation allows the client and server to be developed independently.

## 3.2 Statelessness

**Statelessness means every request must contain the information needed to process it independently.**

The server does not retain client-specific session context between requests as part of the REST interaction.

For example, if a request requires authentication, the client must provide the required authentication credentials or token with each request.

```text
Request 1 + Required Information
              ↓
            Server

Request 2 + Required Information
              ↓
            Server
```

The second request must not depend on the server remembering the first request.

**Exam point:** Statelessness does not mean the server cannot store data. It means the server does not rely on stored client request context to understand a later request.

## 3.3 Resource-Based Design

REST focuses on resources rather than actions.

Prefer:

```text
GET /users
GET /products
POST /orders
```

Avoid designing resource endpoints primarily as action names:

```text
/getUsers
/createProduct
/deleteOrder
```

HTTP methods express the intended action; URLs identify the resources.

## 3.4 Uniform Interface

REST uses a consistent way to identify, access and manipulate resources.

For example:

```text
GET    /users
GET    /users/20
POST   /users
PUT    /users/20
DELETE /users/20
```

Consistent patterns make an API easier to understand.

## 3.5 Cacheability

Responses should indicate whether they can be cached.

Caching can reduce repeated requests and improve performance.

## 3.6 Layered System

A client does not need to know every component between itself and the destination server.

Requests may pass through intermediaries such as proxies or gateways.

---

# 4. HTTP Methods and CRUD

REST APIs commonly use HTTP methods to perform CRUD operations.

CRUD means:

- **Create**
- **Read**
- **Update**
- **Delete**

| HTTP Method | Purpose | CRUD Operation |
|---|---|---|
| `GET` | Retrieve data | Read |
| `POST` | Create a resource | Create |
| `PUT` | Replace a resource or update it completely | Update |
| `PATCH` | Modify part of a resource | Update |
| `DELETE` | Remove a resource | Delete |

### Example

```text
GET     /api/users       → Retrieve users
GET     /api/users/20    → Retrieve user 20
POST    /api/users       → Create a user
PUT     /api/users/20    → Replace user 20
PATCH   /api/users/20    → Modify part of user 20
DELETE  /api/users/20    → Delete user 20
```

## Safe and Idempotent Methods

A **safe method** should not modify the server's resource state.

Common safe methods include:

- `GET`
- `HEAD`
- `OPTIONS`

An **idempotent method** has the same intended effect on server state when the same request is repeated.

Common idempotent methods include:

- `GET`
- `PUT`
- `DELETE`

`POST` is generally not idempotent. Repeating the same request may create multiple resources.

`PATCH` is not guaranteed to be idempotent; its behavior depends on the operation being performed.

---

# 5. HTTP Status Codes

A server uses HTTP status codes to indicate the outcome of a request.

| Status Code | Meaning | Example |
|---|---|---|
| `200 OK` | Request succeeded | Users retrieved |
| `201 Created` | Resource created | New user created |
| `400 Bad Request` | Invalid request | Missing required fields |
| `401 Unauthorized` | Authentication required or failed | Missing or invalid credentials |
| `403 Forbidden` | Access denied | User lacks permission |
| `404 Not Found` | Resource does not exist | User ID not found |
| `429 Too Many Requests` | Too many requests | Rate limit exceeded |
| `500 Internal Server Error` | Unexpected server error | Server-side failure |

### Example in Express

```javascript
res.status(200).json(users);
```

Returns a successful response containing the users.

```javascript
res.status(201).json(newUser);
```

Returns a resource-created response.

```javascript
res.status(404).json({
  message: "User not found"
});
```

Returns a not-found response.

```javascript
res.status(500).json({
  message: "Internal server error"
});
```

Returns a server-error response.

---

# 6. How a REST API Works

A REST API request follows a sequence.

## Step 1: Client Sends a Request

The client sends an HTTP request.

It may contain:

- HTTP method
- URL
- Headers
- Query parameters
- Request body

Example:

```http
POST /api/users
Content-Type: application/json
```

Request body:

```json
{
  "name": "John",
  "email": "john@example.com"
}
```

## Step 2: Server Receives the Request

The server:

- Identifies the requested resource.
- Checks the HTTP method.
- Validates the request.
- Checks authentication and permissions when required.

## Step 3: Server Performs the Operation

The server may:

- Retrieve data.
- Create a record.
- Update a record.
- Delete a record.
- Execute other business logic.

## Step 4: Server Builds the Response

The server selects an appropriate status code and prepares the response data.

Example:

```json
{
  "id": 21,
  "name": "John",
  "email": "john@example.com"
}
```

## Step 5: Server Sends the Response

The response can contain:

- Status code
- Headers
- Response body

## Step 6: Client Processes the Response

The client checks the status code and uses the returned data.

### Complete Flow

```text
Client
  ↓
HTTP Request
  ↓
Express Server
  ↓
Middleware
  ↓
Route
  ↓
Validation / Authentication
  ↓
Business Logic
  ↓
Database
  ↓
HTTP Status + Response Data
  ↓
Client
```

---

# 7. Building a REST API with Express

Express provides routing and middleware for implementing REST APIs in Node.js.

## Basic Setup

Install Express:

```bash
npm init -y
npm install express
```

Create `app.js`:

```javascript
const express = require("express");

const app = express();
const port = 3000;

// Parse incoming JSON request bodies
app.use(express.json());

app.get("/", (req, res) => {
  res.send("REST API is running");
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

Run:

```bash
node app.js
```

## Complete CRUD Example

This example stores users in an in-memory array. The data resets when the server restarts; it is not a persistent database.

```javascript
const express = require("express");

const app = express();
const port = 3000;

app.use(express.json());

let users = [
  {
    id: 1,
    name: "John Doe",
    email: "john@example.com"
  },
  {
    id: 2,
    name: "Jane Smith",
    email: "jane@example.com"
  }
];

// GET: Retrieve all users
app.get("/api/users", (req, res) => {
  res.status(200).json(users);
});

// GET: Retrieve one user
app.get("/api/users/:id", (req, res) => {
  const id = Number(req.params.id);
  const user = users.find(user => user.id === id);

  if (!user) {
    return res.status(404).json({
      message: "User not found"
    });
  }

  res.status(200).json(user);
});

// POST: Create a user
app.post("/api/users", (req, res) => {
  const { name, email } = req.body;

  if (!name || !email) {
    return res.status(400).json({
      message: "Name and email are required"
    });
  }

  const newUser = {
    id: Math.max(0, ...users.map(user => user.id)) + 1,
    name,
    email
  };

  users.push(newUser);

  res.status(201).json(newUser);
});

// PUT: Replace a user's data
app.put("/api/users/:id", (req, res) => {
  const id = Number(req.params.id);
  const user = users.find(user => user.id === id);

  if (!user) {
    return res.status(404).json({
      message: "User not found"
    });
  }

  const { name, email } = req.body;

  if (!name || !email) {
    return res.status(400).json({
      message: "Name and email are required"
    });
  }

  user.name = name;
  user.email = email;

  res.status(200).json(user);
});

// PATCH: Partially update a user
app.patch("/api/users/:id", (req, res) => {
  const id = Number(req.params.id);
  const user = users.find(user => user.id === id);

  if (!user) {
    return res.status(404).json({
      message: "User not found"
    });
  }

  const { name, email } = req.body;

  if (name !== undefined) user.name = name;
  if (email !== undefined) user.email = email;

  res.status(200).json(user);
});

// DELETE: Remove a user
app.delete("/api/users/:id", (req, res) => {
  const id = Number(req.params.id);
  const index = users.findIndex(user => user.id === id);

  if (index === -1) {
    return res.status(404).json({
      message: "User not found"
    });
  }

  const deletedUser = users.splice(index, 1)[0];

  res.status(200).json(deletedUser);
});

app.listen(port, () => {
  console.log(`REST API running on port ${port}`);
});
```

## API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/api/users` | Retrieve all users |
| `GET` | `/api/users/1` | Retrieve user 1 |
| `POST` | `/api/users` | Create a user |
| `PUT` | `/api/users/1` | Replace user 1's data |
| `PATCH` | `/api/users/1` | Partially update user 1 |
| `DELETE` | `/api/users/1` | Delete user 1 |

---

# 8. REST API Design Best Practices

## Use Nouns for Resources

Prefer resource names instead of action names.

Good:

```text
/api/users
/api/products
/api/orders
```

Avoid:

```text
/api/getUsers
/api/createProduct
/api/deleteOrder
```

## Use Plural Resource Names

Prefer:

```text
/api/users
/api/products
```

Use consistent naming conventions throughout the API.

## Represent Relationships Clearly

Example:

```text
/api/users/20/orders
/api/products/5/reviews
```

These URLs show relationships between resources.

## Use Query Parameters for Filtering

Example:

```text
/api/products?category=electronics
/api/products?sort=price
/api/products?limit=10&page=2
```

Query parameters can support filtering, sorting and pagination.

## Validate Incoming Data

Check the request body and other input before processing it.

Validate:

- Required fields
- Data types
- Email formats
- Allowed values
- Input length
- Access permissions

Libraries such as Joi or `express-validator` can help validate requests.

## Handle Errors Consistently

Return appropriate status codes and clear error messages.

Avoid exposing sensitive internal details or stack traces in production responses.

## Use HTTPS

Use HTTPS to protect data sent between clients and production APIs.

## Apply Rate Limiting

Rate limiting can reduce abuse by restricting how frequently clients make requests.

## Document and Test APIs

API documentation helps developers understand endpoints and expected data formats.

Common tools include:

- Swagger / OpenAPI for documentation
- Jest for testing
- Mocha for testing
- Supertest for testing HTTP endpoints

---

# 9. API Versioning

Versioning allows an API to evolve while helping existing clients continue using older versions.

Common approaches include:

### URL Versioning

```text
/api/v1/users
/api/v2/users
```

### Query Parameter Versioning

```text
/api/users?version=1
```

### Custom Header Versioning

```http
X-API-Version: 1
```

The correct strategy depends on the API's requirements.

---

# 10. REST API Project Structure

For a larger Express API, separate responsibilities into different files.

```text
project/
│
├── app.js
├── routes/
│   ├── users.js
│   └── products.js
├── controllers/
│   ├── userController.js
│   └── productController.js
├── models/
│   ├── User.js
│   └── Product.js
├── middleware/
│   ├── auth.js
│   └── validation.js
├── services/
├── config/
└── tests/
```

### Responsibilities

| Component | Responsibility |
|---|---|
| Routes | Define endpoints and HTTP methods |
| Controllers | Handle requests and responses |
| Models | Represent data and interact with its storage |
| Middleware | Process requests before handlers |
| Services | Contain reusable business logic |
| Config | Store application configuration |
| Tests | Verify application behavior |

Example route file:

```javascript
// routes/users.js
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.json({
    message: "List of users"
  });
});

router.get("/:id", (req, res) => {
  res.json({
    message: "Retrieve user",
    id: req.params.id
  });
});

module.exports = router;
```

Mount the router in `app.js`:

```javascript
const express = require("express");
const app = express();

const userRoutes = require("./routes/users");

app.use(express.json());
app.use("/api/users", userRoutes);

app.listen(3000);
```

---

# 11. What Are Microservices?

## Monolithic Architecture

A **monolith** is an application where the main components are built and deployed together as one system.

These components may include:

- User interface
- API
- Authentication
- Business logic
- Database access
- Payment processing

Example: An e-commerce application where products, checkout, authentication and payments are part of one codebase and deployment unit.

### Monolith Structure

```text
E-commerce Application
          │
          ├── Users
          ├── Products
          ├── Cart
          ├── Orders
          ├── Payments
          ├── Authentication
          └── API
```

### Advantages

- Simple to start developing
- Straightforward deployment
- Easier to manage for smaller applications
- Components can communicate directly within the application

### Challenges as the Application Grows

- Code can become harder to maintain.
- Small changes may require redeploying the whole application.
- Scaling one feature may require scaling the entire application.
- Components can become tightly coupled.

A monolith is not automatically bad. It can be a good choice for smaller projects.

---

## Microservices Architecture

**Microservices** is an architectural approach in which a large application is divided into smaller, independent services.

Each service handles a particular business capability.

Examples:

- User service
- Product service
- Order service
- Payment service
- Authentication service

Services communicate through APIs or message-based systems.

### Microservices Structure

```text
             E-commerce Application
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
   User Service   Product Service  Order Service
        │              │              │
        ↓              ↓              ↓
   User Data      Product Data     Order Data

                       │
                       ↓
                Payment Service
                       │
                       ↓
                  Payment Data
```

Services may have their own codebases and databases, although the exact design depends on the application.

## Characteristics of Microservices

- Services are independently organized.
- Each service has a specific responsibility.
- Services communicate through APIs or messaging.
- Services can be developed and deployed independently.
- Different services can use different programming languages or frameworks.
- Services can be scaled separately.

Example:

```text
Product Service → Node.js
Search Service  → Java
Auth Service    → .NET
```

The services can still work together as one application.

---

# 12. Monolith vs Microservices

| Feature | Monolith | Microservices |
|---|---|---|
| Structure | One main application | Multiple independent services |
| Codebase | Commonly one codebase | Often separate codebases |
| Deployment | Usually deployed as one unit | Services can be deployed independently |
| Scaling | Often scales the whole application | Individual services can be scaled |
| Programming languages | Commonly one main stack | Different services can use different stacks |
| Development | Simpler to start | More distributed coordination |
| Debugging | Often simpler within one process | Harder across multiple services |
| Infrastructure | Usually simpler | More complex to manage |
| Communication | Often direct in-process calls | Network calls or messaging |
| Fault isolation | A failure can affect the whole application | Services can isolate some failures, depending on design |

---

# 13. Advantages and Challenges of Microservices

## Advantages

### Independent Deployment

A service can be updated without necessarily redeploying the entire application.

### Independent Scaling

A high-demand service can be scaled without scaling every other service.

### Technology Flexibility

Different teams can select technologies suited to their services.

### Fault Isolation

A failure can be isolated to one service if the system is designed to handle failures appropriately.

### Team Independence

Different teams can develop separate services in parallel.

## Challenges

### Complex Debugging

A single request may pass through several services, making problems harder to trace.

### Infrastructure Complexity

More services require more deployment, monitoring and operational management.

### Network Overhead

Services communicating over a network introduce latency and possible communication failures.

### Data Management

Data distributed between services can be harder to coordinate consistently.

### More Operational Work

The system may need service discovery, centralized logging, monitoring, security and other infrastructure.

**Important:** Microservices are not always better than monoliths. The best architecture depends on the application's complexity, scale and team requirements.

---

# 14. Quick Reference

## Web Services

| Term | Meaning |
|---|---|
| API | Interface through which software communicates |
| Web service | API using web technologies to exchange data over a network |
| REST | Architectural style for networked applications |
| SOAP | Protocol using structured messages, commonly XML |
| XML-RPC | Remote procedure calls encoded using XML |
| UDDI | Directory for describing and discovering web services |

## REST

| Concept | Key Point |
|---|---|
| Resources | Data identified by URLs |
| Statelessness | Each request contains the information needed to process it |
| `GET` | Retrieve data |
| `POST` | Create a resource |
| `PUT` | Replace a resource |
| `PATCH` | Partially modify a resource |
| `DELETE` | Remove a resource |
| `200` | Success |
| `201` | Created |
| `400` | Bad request |
| `404` | Not found |
| `500` | Server error |

## Microservices

| Term | Meaning |
|---|---|
| Monolith | Application built and deployed as one main unit |
| Microservices | Application divided into smaller independent services |
| Independent deployment | Services can be deployed separately |
| Independent scaling | Individual services can be scaled as needed |
| Service communication | APIs or messaging |
| Fault isolation | Limiting the effects of a service failure |

---

# 15. Exam Questions and Answers

## Lesson 1: Web Services

**1. What does SOAP stand for?**

Answer: **Simple Object Access Protocol.**

**2. What does REST expose that clients can interact with, such as `/users` or `/users/20`?**

Answer: **Resources.**

**3. Which is NOT a characteristic of a web service?**

Answer: **It must have a user interface for humans to interact with.**

Web services focus on software-to-software communication and do not require a human-facing interface.

## Lesson 2: REST Architecture

**4. What does statelessness mean?**

Answer: **Each request is independent and contains all necessary information.**

**5. How does the REST architecture work?**

Answer: **The client sends a request, the server processes it, performs an operation, and sends a response.**

**6. What does REST stand for?**

Answer: **Representational State Transfer.**

## Lesson 3: Microservices

**7. What does monolith mean?**

Answer: **A single, large codebase containing the entire application.**

**8. What is a key characteristic of microservices?**

Answer: **Each service is independent, with its own codebase and sometimes its own database.**

**9. Which is a benefit of microservices?**

Answer: **Different services can use different programming languages or frameworks.**

---

# 16. Practical Skills Checklist

After studying these topics, you should be able to:

- [ ] Explain APIs and web services.
- [ ] Distinguish APIs from web services.
- [ ] Explain REST and SOAP.
- [ ] Identify resources and resource URLs.
- [ ] Understand JSON and XML representations.
- [ ] Explain REST statelessness.
- [ ] Match HTTP methods to CRUD operations.
- [ ] Recognize common HTTP status codes.
- [ ] Explain the client-server request-response cycle.
- [ ] Create basic REST endpoints with Express.
- [ ] Implement GET, POST, PUT, PATCH and DELETE routes.
- [ ] Validate incoming request data.
- [ ] Handle missing resources and invalid requests.
- [ ] Design consistent resource-based URLs.
- [ ] Explain API versioning and documentation.
- [ ] Distinguish a monolith from microservices.
- [ ] Explain the advantages and challenges of microservices.

---

# Core Principles

```text
WEB SERVICE
Software Application
        ↓
HTTP / Other Web Technologies
        ↓
Software Application
```

```text
REST API
Client
  ↓ HTTP Request
Server
  ↓ Process Resource
Database / Business Logic
  ↓
HTTP Response
  ↓
Client
```

```text
MONOLITH
One Main Application
        ↓
Users + Products + Orders + Payments
```

```text
MICROSERVICES
Application
    │
    ├── User Service
    ├── Product Service
    ├── Order Service
    └── Payment Service
```

**Remember:**

- Web services allow software applications to communicate over a network.
- REST organizes interactions around resources and standard HTTP methods.
- Statelessness means each request carries the information needed to process it.
- HTTP status codes describe the outcome of a request.
- Microservices divide an application into independently organized services.
- Monoliths can be simpler to build and operate, while microservices can provide more independent deployment and scaling at the cost of greater complexity.