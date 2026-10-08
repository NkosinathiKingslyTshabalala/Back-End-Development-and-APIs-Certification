# Express.js

Express.js is a minimal, flexible web framework built on top of **Node.js** for building web applications, servers, and APIs.

It simplifies HTTP server development by providing routing, middleware, request/response handling, static file serving, and other useful features.

---

# What Is Express.js?

Express is:

* Built on Node.js
* Minimal and flexible
* Lightweight and fast
* Unopinionated
* Extensible through middleware
* Supported by a large ecosystem of packages
* Well suited for RESTful APIs

Express provides a thin layer over Node.js while still allowing access to Node's features.

### Main Features

* Routing
* HTTP request handling
* Middleware
* Static file serving
* Error handling
* Template engines
* API development

---

# Installing Express

Check Node.js and npm:

```bash
node -v
npm -v
```

Create a project:

```bash
mkdir my-app
cd my-app
npm init -y
npm install express
```

Express is added to `package.json` as a dependency.

---

# Basic Express App

```javascript
const express = require("express");

const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

Run:

```bash
node index.js
```

Open:

```text
http://localhost:3000
```

---

# Basic Express Structure

```text
Express Application
       │
       ├── express()
       │      ↓
       │   app object
       │
       ├── Routes
       │      ↓
       │   Request
       │      ↓
       │   Route Handler
       │      ↓
       │   Response
       │
       ├── Middleware
       │
       └── app.listen()
              ↓
           Server
```

---

# Important Express Objects

## `express`

Loads the Express library:

```javascript
const express = require("express");
```

## `app`

Creates an Express application:

```javascript
const app = express();
```

`app` provides methods such as:

```javascript
app.get()
app.post()
app.put()
app.delete()
app.use()
app.listen()
```

## `req`

The request object contains information about the incoming request.

Examples:

```javascript
req.params
req.query
req.body
req.headers
```

## `res`

The response object is used to send a response to the client.

Examples:

```javascript
res.send()
res.json()
res.status()
res.redirect()
res.render()
```

---

# `app.listen()`

Starts the Express server and listens for incoming requests.

```javascript
app.listen(3000, () => {
  console.log("Server running");
});
```

The number `3000` is the port.

---

# Routing

Routing determines how an application responds to requests made to specific URLs.

General structure:

```javascript
app.METHOD(PATH, HANDLER);
```

Example:

```javascript
app.get("/about", (req, res) => {
  res.send("About page");
});
```

---

# HTTP Route Methods

| Method   | Purpose       |
| -------- | ------------- |
| `GET`    | Retrieve data |
| `POST`   | Create data   |
| `PUT`    | Update data   |
| `DELETE` | Delete data   |

Express:

```javascript
app.get()
app.post()
app.put()
app.delete()
```

Example:

```javascript
app.get("/users", (req, res) => {
  res.send("Get users");
});

app.post("/users", (req, res) => {
  res.send("Create user");
});

app.put("/users", (req, res) => {
  res.send("Update user");
});

app.delete("/users", (req, res) => {
  res.send("Delete user");
});
```

---

# Route Paths

A route path determines which URL a route responds to.

## Static Route

```javascript
app.get("/home", (req, res) => {
  res.send("Welcome home");
});
```

Responds to:

```text
GET /home
```

Another example:

```javascript
app.get("/menu/drinks", (req, res) => {
  res.send("Drinks menu");
});
```

---

# Root Route

The root URL is:

```text
/
```

Example:

```javascript
app.get("/", (req, res) => {
  res.send("Homepage");
});
```

---

# Route Parameters

Route parameters allow dynamic values to be captured from the URL.

Syntax:

```text
:paramName
```

Example:

```javascript
app.get("/post/:postId", (req, res) => {
  const postId = req.params.postId;

  res.send(`Viewing post with ID: ${postId}`);
});
```

Request:

```text
GET /post/42
```

Result:

```text
req.params.postId
        ↓
       "42"
```

Response:

```text
Viewing post with ID: 42
```

---

## Multiple Route Parameters

```javascript
app.get("/users/:userId/books/:bookId", (req, res) => {
  res.send(
    `User: ${req.params.userId}, Book: ${req.params.bookId}`
  );
});
```

URL:

```text
/users/10/books/25
```

Parameters:

```javascript
req.params.userId   // 10
req.params.bookId   // 25
```

---

# Query Parameters

Query parameters appear after `?` in a URL.

Example:

```text
/search?q=express&category=framework
```

Access them using:

```javascript
req.query
```

Example:

```javascript
app.get("/search", (req, res) => {
  const { q, category } = req.query;

  res.send(`Search: ${q}, Category: ${category}`);
});
```

URL:

```text
/search?q=express&category=framework
```

Values:

```javascript
req.query.q
// express

req.query.category
// framework
```

---

# Route Parameters vs Query Parameters

| Type            | Example        | Access          |
| --------------- | -------------- | --------------- |
| Route parameter | `/users/42`    | `req.params.id` |
| Query parameter | `/users?id=42` | `req.query.id`  |

### Remember

```text
URL PATH
/users/:id
       ↓
   req.params

QUERY STRING
/users?id=42
       ↓
   req.query
```

---

# Route Handlers

A route handler is the function that executes when a request matches a route.

```javascript
app.get("/menu", (req, res) => {
  res.send("Welcome to the menu!");
});
```

Here:

```javascript
(req, res) => {
  res.send("Welcome to the menu!");
}
```

is the route handler.

The handler can:

* Process requests
* Perform calculations
* Query databases
* Validate data
* Send responses

---

# Response Methods

## `res.send()`

Sends a response.

```javascript
res.send("Hello World!");
```

Can send:

* Text
* HTML
* JSON
* Other supported data

---

## `res.json()`

Sends JSON data.

```javascript
app.get("/user", (req, res) => {
  res.json({
    name: "John",
    age: 30
  });
});
```

Useful for APIs.

---

## `res.status()`

Sets the HTTP status code.

```javascript
res.status(404).send("Not Found");
```

Common pattern:

```javascript
res.status(201).json(data);
```

---

## `res.redirect()`

Redirects the client to another URL.

```javascript
res.redirect("/newpage");
```

---

## `res.render()`

Renders a template using a template engine.

```javascript
res.render("profile", {
  username: "john_doe"
});
```

Common template engines:

* EJS
* Pug
* Handlebars

---

# `app.route()`

`app.route()` groups multiple HTTP methods for the same route.

Instead of:

```javascript
app.get("/user", handler);
app.post("/user", handler);
app.put("/user", handler);
```

You can use:

```javascript
app
  .route("/user")
  .get((req, res) => {
    res.send("Get user");
  })
  .post((req, res) => {
    res.send("Create user");
  })
  .put((req, res) => {
    res.send("Update user");
  })
  .delete((req, res) => {
    res.send("Delete user");
  });
```

### Benefits

* Less repetition
* Cleaner code
* Groups related operations
* Useful for REST APIs

---

# Express Router

`express.Router()` creates a modular router.

```javascript
const router = express.Router();
```

A router behaves like a smaller Express application for organizing routes.

---

## Router Example

### `userRoutes.js`

```javascript
const express = require("express");

const router = express.Router();

router.get("/", (req, res) => {
  res.send("List of users");
});

router.post("/", (req, res) => {
  res.send("Create user");
});

router.get("/:id", (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});

module.exports = router;
```

### `app.js`

```javascript
const express = require("express");

const app = express();

const userRoutes = require("./userRoutes");

app.use("/users", userRoutes);

app.listen(3000);
```

The router is mounted at:

```text
/users
```

Therefore:

```text
router.get("/")
        ↓
GET /users

router.post("/")
        ↓
POST /users

router.get("/:id")
        ↓
GET /users/:id
```

---

# Benefits of `express.Router()`

* Separation of concerns
* Cleaner main application file
* Easier maintenance
* Better scalability
* Groups related routes
* Allows router-specific middleware

Typical structure:

```text
project/
│
├── app.js
│
├── routes/
│   ├── users.js
│   ├── products.js
│   └── auth.js
│
└── public/
```

---

# Middleware

Middleware is a function that runs during the **request-response cycle**.

Middleware has access to:

```javascript
req
res
next
```

Basic structure:

```javascript
app.use((req, res, next) => {
  // middleware logic

  next();
});
```

Middleware can:

* Execute code
* Modify `req`
* Modify `res`
* End the request-response cycle
* Call the next middleware

Middleware acts as a processing layer between the incoming request and the final route handler.

---

# Middleware Flow

```text
Client Request
      ↓
 Middleware 1
      ↓
 Middleware 2
      ↓
 Route Handler
      ↓
 Response
      ↓
Client
```

Middleware executes in the order it is added.

Example:

```javascript
app.use((req, res, next) => {
  console.log("First middleware");
  next();
});

app.use((req, res, next) => {
  console.log("Second middleware");
  next();
});

app.get("/", (req, res) => {
  res.send("Hello World!");
});
```

Request flow:

```text
Request
   ↓
Middleware 1
   ↓
next()
   ↓
Middleware 2
   ↓
next()
   ↓
Route Handler
   ↓
Response
```

---

# `next()`

`next()` passes control to the next middleware or route handler.

```javascript
app.use((req, res, next) => {
  console.log("Processing request");
  next();
});
```

### Important

If middleware:

```javascript
next();
```

is called:

```text
Continue to next middleware/handler
```

If middleware sends a response and does not call `next()`:

```text
Request-response cycle ends
```

Do not call `next()` after already sending the response.

---

# Simple Middleware Example

```javascript
const express = require("express");

const app = express();

app.use((req, res, next) => {
  console.log("Request URL:", req.url);
  console.log("Request Method:", req.method);

  next();
});

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(3000);
```

The middleware logs information about every request before the route handler runs.

---

# Types of Middleware

Express middleware can be categorized by scope and purpose.

Main types:

```text
1. Application-level
2. Router-level
3. Error-handling
4. Built-in
5. Third-party
6. Custom
```

---

# Application-level Middleware

Application-level middleware is bound to the main Express application.

Usually added with:

```javascript
app.use()
```

or:

```javascript
app.get()
app.post()
app.put()
app.delete()
```

Example:

```javascript
app.use((req, res, next) => {
  console.log("Request received");
  next();
});
```

When added with `app.use()` without a route restriction, it can run for incoming requests across the application.

### Common Uses

* Logging
* Authentication
* Request parsing
* Security
* General request processing

### Example

```javascript
const express = require("express");

const app = express();

app.use((req, res, next) => {
  console.log("Time:", new Date());
  next();
});

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(3000);
```

---

# Router-level Middleware

Router-level middleware is bound to an instance of:

```javascript
express.Router()
```

Instead of applying middleware to the whole application, it can be applied to a group of related routes.

Example:

```javascript
const express = require("express");

const app = express();
const router = express.Router();

router.use((req, res, next) => {
  console.log("Router middleware");
  next();
});

router.get("/drinks", (req, res) => {
  res.send("Drinks menu");
});

app.use("/menu", router);

app.listen(3000);
```

The middleware applies to routes handled by the router.

For example:

```text
/menu/drinks
```

### Key Methods

```javascript
router.use()
router.get()
router.post()
router.put()
router.delete()
```

### Why Use Router-level Middleware?

* Modular routing
* Cleaner code
* Group-specific middleware
* Separation of concerns
* Easier maintenance

---

# Application-level vs Router-level Middleware

| Type              | Bound To           | Typical Scope        |
| ----------------- | ------------------ | -------------------- |
| Application-level | `app`              | Whole application    |
| Router-level      | `express.Router()` | Specific route group |

Remember:

```text
app.use()
   ↓
Application-level

router.use()
   ↓
Router-level
```

---

# Route-specific Middleware

Middleware can also be attached directly to a specific route.

```javascript
function authenticate(req, res, next) {
  console.log("Checking authentication");
  next();
}

app.get("/protected", authenticate, (req, res) => {
  res.send("Protected data");
});
```

Flow:

```text
GET /protected
      ↓
authenticate
      ↓
Route Handler
      ↓
Response
```

This is useful when middleware should only run for selected routes.

---

# Error-handling Middleware

Error-handling middleware handles errors during the request-response cycle.

It has **four parameters**:

```javascript
(err, req, res, next)
```

Example:

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);

  res.status(500).send("Something went wrong!");
});
```

### Important

Error-handling middleware:

* Uses exactly four parameters
* Is normally placed after routes and other middleware
* Centralizes error handling
* Can pass errors using `next(err)`

---

# Passing Errors with `next(err)`

Example:

```javascript
app.get("/error", (req, res, next) => {
  try {
    throw new Error("Something went wrong!");
  } catch (error) {
    next(error);
  }
});
```

The error is passed to:

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);

  res.status(500).json({
    message: "An error occurred"
  });
});
```

Flow:

```text
Route
  ↓
Error occurs
  ↓
next(error)
  ↓
Error Middleware
  ↓
HTTP 500 Response
```

---

# Built-in Middleware

Express includes middleware for common tasks.

### Common Built-in Middleware

```javascript
express.json()
express.urlencoded()
express.static()
express.Router()
```

---

## `express.json()`

Parses incoming JSON request bodies.

```javascript
app.use(express.json());
```

Example:

```javascript
app.post("/users", (req, res) => {
  console.log(req.body);

  res.status(201).json(req.body);
});
```

---

## `express.urlencoded()`

Parses URL-encoded request bodies, commonly used by HTML forms.

```javascript
app.use(
  express.urlencoded({
    extended: true
  })
);
```

Parsed form data becomes available through:

```javascript
req.body
```

---

## `express.static()`

Serves static files such as:

* HTML
* CSS
* JavaScript
* Images
* Fonts

Example:

```javascript
app.use(express.static("public"));
```

Project:

```text
my-app/
│
├── app.js
│
└── public/
    ├── index.html
    ├── styles.css
    └── image.png
```

---

# Static File Mount Paths

You can mount a static directory under a custom URL path.

```javascript
app.use(
  "/images",
  express.static("images")
);
```

Then:

```text
/images/logo.png
```

maps to:

```text
images/logo.png
```

Using an absolute path:

```javascript
const path = require("path");

app.use(
  "/assets",
  express.static(
    path.join(__dirname, "public")
  )
);
```

---

# Third-party Middleware

Third-party middleware packages extend Express functionality.

Common examples:

| Package         | Purpose                       |
| --------------- | ----------------------------- |
| `morgan`        | HTTP request logging          |
| `helmet`        | Security-related HTTP headers |
| `cors`          | Cross-Origin Resource Sharing |
| `compression`   | Response compression          |
| `cookie-parser` | Cookie handling               |

Install:

```bash
npm install helmet morgan cors compression cookie-parser
```

Example:

```javascript
const morgan = require("morgan");
const helmet = require("helmet");
const cors = require("cors");

app.use(morgan("dev"));
app.use(helmet());
app.use(cors());
```

---

# Built-in vs Third-party Middleware

| Built-in               | Third-party   |
| ---------------------- | ------------- |
| `express.json()`       | `cors`        |
| `express.urlencoded()` | `morgan`      |
| `express.static()`     | `helmet`      |
| `express.Router()`     | `compression` |

### Remember

```text
Express provides:
express.json()
express.urlencoded()
express.static()

Packages provide:
cors
morgan
helmet
compression
```

---

# Custom Middleware

You can create your own middleware for application-specific functionality.

Basic example:

```javascript
function requestLogger(req, res, next) {
  const timestamp = new Date().toISOString();

  console.log(
    `${timestamp} - ${req.method} ${req.url}`
  );

  next();
}

app.use(requestLogger);
```

### Good Custom Middleware Should Be:

* Focused
* Reusable
* Testable
* Configurable
* Easy to understand
* Based on a single responsibility

---

# Authentication Middleware

Middleware can check whether a user is authenticated before allowing access to a route.

Example:

```javascript
function authenticate(req, res, next) {
  const authHeader = req.headers.authorization;

  if (!authHeader) {
    return res
      .status(401)
      .send("Authentication required");
  }

  const token = authHeader.split(" ")[1];

  if (token === "secret-token") {
    req.user = {
      id: 123,
      username: "john"
    };

    next();
  } else {
    res.status(403).send("Invalid token");
  }
}
```

Apply it to a route:

```javascript
app.get(
  "/api/protected",
  authenticate,
  (req, res) => {
    res.json({
      message: "Protected data",
      user: req.user
    });
  }
);
```

Important idea:

```text
Authentication passes
        ↓
      next()
        ↓
Route handler runs

Authentication fails
        ↓
Response sent
        ↓
Request ends
```

---

# Request Validation Middleware

Middleware can validate incoming data before it reaches the route handler.

Example:

```javascript
function validateUserCreation(req, res, next) {
  const {
    username,
    email,
    password
  } = req.body;

  if (!username || username.length < 3) {
    return res.status(400).json({
      error: "Username must be at least 3 characters"
    });
  }

  if (!email || !email.includes("@")) {
    return res.status(400).json({
      error: "Valid email is required"
    });
  }

  if (!password || password.length < 6) {
    return res.status(400).json({
      error: "Password must be at least 6 characters"
    });
  }

  next();
}
```

Apply it:

```javascript
app.post(
  "/api/users",
  validateUserCreation,
  (req, res) => {
    res.status(201).json({
      message: "User created successfully"
    });
  }
);
```

---

# Conditional Middleware

Middleware can decide whether the request continues.

Example:

```javascript
function rateLimit(req, res, next) {
  const ip = req.ip;

  if (tooManyRequests(ip)) {
    return res
      .status(429)
      .send("Too many requests");
  }

  next();
}
```

Important:

```text
Condition fails
      ↓
Send response
      ↓
No next()

Condition passes
      ↓
next()
      ↓
Continue
```

---

# Middleware Execution Order

Middleware executes in the order it is added.

Therefore:

```javascript
app.use(firstMiddleware);

app.use(secondMiddleware);

app.get("/", routeHandler);
```

runs as:

```text
Request
   ↓
firstMiddleware
   ↓
secondMiddleware
   ↓
routeHandler
   ↓
Response
```

Order matters.

---

# Recommended Middleware Order

A common structure is:

```text
1. Application-wide middleware
2. Route-specific middleware
3. Routes
4. 404 handler
5. Error handler
```

Example:

```javascript
// 1. Application-wide middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(morgan("dev"));
app.use(helmet());

// 2. Route-specific middleware
app.use("/api", authenticate);

// 3. Routes
app.use("/api/users", userRoutes);
app.use("/api/products", productRoutes);

// 4. 404 handler
app.use((req, res) => {
  res.status(404).json({
    message: "Not found"
  });
});

// 5. Error handler
app.use((err, req, res, next) => {
  console.error(err);

  res.status(500).json({
    message: "Server error"
  });
});
```

### Key Rule

```text
Specific routes and middleware
        ↓
        first

Error handling
        ↓
       last
```

---

# 404 Middleware

A catch-all middleware can handle requests that do not match any route.

```javascript
app.use((req, res) => {
  res.status(404).send("Not found");
});
```

Place it after the application routes.

---

# Async Middleware Errors

Asynchronous middleware should properly handle rejected promises and pass errors to error-handling middleware.

Example:

```javascript
app.get("/async-data", async (req, res, next) => {
  try {
    const data = await fetchDataFromDatabase();

    res.json(data);
  } catch (error) {
    next(error);
  }
});
```

The important pattern is:

```text
Async operation
      ↓
Error?
      ↓
catch(error)
      ↓
next(error)
      ↓
Error middleware
```

---

# Middleware Factory

A middleware factory is a function that creates middleware with specific configuration.

Example:

```javascript
function requireRole(role) {
  return (req, res, next) => {
    if (req.user && req.user.role === role) {
      next();
    } else {
      res.status(403).send("Access denied");
    }
  };
}
```

Use it:

```javascript
app.get(
  "/admin",
  authenticate,
  requireRole("admin"),
  (req, res) => {
    res.send("Admin dashboard");
  }
);

app.get(
  "/editor",
  authenticate,
  requireRole("editor"),
  (req, res) => {
    res.send("Editor dashboard");
  }
);
```

---

# Middleware Best Practices

## 1. Keep Middleware Focused

Each middleware should have one main responsibility.

```text
Logging middleware
        ↓
Only logging

Authentication middleware
        ↓
Only authentication

Validation middleware
        ↓
Only validation
```

---

## 2. Use `next()` Correctly

```javascript
next();
```

Use `next()` when the middleware should continue the request.

Do not:

```javascript
res.send("Done");
next();
```

after already sending the response.

For errors:

```javascript
next(error);
```

---

## 3. Handle Async Errors

Catch asynchronous errors and pass them to error-handling middleware.

```javascript
try {
  // async operation
} catch (error) {
  next(error);
}
```

---

## 4. Do Not Overuse Middleware

Too many middleware functions can make an application harder to understand and may add unnecessary processing.

Use middleware where it adds clear value.

---

## 5. Organize Middleware

A typical structure:

```text
project/
│
├── app.js
│
├── middleware/
│   ├── auth.js
│   ├── validation.js
│   └── logging.js
│
├── routes/
│   ├── users.js
│   └── products.js
│
└── controllers/
```

---

# Complete Request Flow

```text
Client
  │
  │ HTTP Request
  ↓
Express Server
  │
  ↓
Application Middleware
  │
  ├── JSON parsing
  ├── Logging
  ├── Security
  └── CORS
  │
  ↓
Route-specific Middleware
  │
  ├── Authentication
  ├── Validation
  └── Authorization
  │
  ↓
Router
  │
  ↓
Route Handler
  │
  ├── Business Logic
  ├── Database
  └── Processing
  │
  ↓
Response
  │
  ├── res.send()
  ├── res.json()
  ├── res.status()
  ├── res.redirect()
  └── res.render()
  │
  ↓
Client
```

Error path:

```text
Any stage
   ↓
Error
   ↓
next(error)
   ↓
Error-handling middleware
   ↓
HTTP Error Response
```

---

# Template Engines

Express can generate dynamic HTML using template engines.

Example with EJS:

```bash
npm install ejs
```

Configure:

```javascript
app.set("view engine", "ejs");
app.set("views", "./views");
```

Render:

```javascript
app.get("/", (req, res) => {
  res.render("index", {
    title: "Home",
    message: "Hello from Express!"
  });
});
```

Typical structure:

```text
project/
│
├── app.js
│
└── views/
    └── index.ejs
```

---

# RESTful APIs

Express is commonly used to build RESTful APIs.

Typical pattern:

```text
GET     /users       → Get users
POST    /users       → Create user
GET     /users/:id   → Get one user
PUT     /users/:id   → Update user
DELETE  /users/:id   → Delete user
```

---

# Express Application Generator

Express provides a generator for creating an application skeleton.

Install:

```bash
npm install -g express-generator
```

Create an application:

```bash
express --view=ejs myapp
```

Then:

```bash
cd myapp
npm install
npm start
```

Typical structure:

```text
myapp/
├── app.js
├── bin/
│   └── www
├── package.json
├── public/
├── routes/
│   ├── index.js
│   └── users.js
└── views/
```

---

# Express Best Practices

## Project Structure

Organize code by feature or component.

```text
routes/
controllers/
models/
middleware/
services/
```

## Environment Variables

Use environment variables for configuration and secrets.

## Error Handling

Centralize error handling.

## Logging

Use logging tools such as:

```text
morgan
winston
```

## Validation

Validate user input.

Example library:

```text
express-validator
```

## Security

Common security practices include:

* Helmet
* HTTPS
* Input validation
* CORS configuration
* Rate limiting
* Environment variables
* Proper error handling

## Performance

Consider:

* Compression
* Caching
* Reverse proxy
* Database query optimization
* Clustering

---

# Quick Reference

| Concept             | Express                      |
| ------------------- | ---------------------------- |
| Create app          | `express()`                  |
| GET route           | `app.get()`                  |
| POST route          | `app.post()`                 |
| PUT route           | `app.put()`                  |
| DELETE route        | `app.delete()`               |
| Middleware          | `app.use()`                  |
| Router              | `express.Router()`           |
| Router middleware   | `router.use()`               |
| Start server        | `app.listen()`               |
| Request params      | `req.params`                 |
| Query parameters    | `req.query`                  |
| Request body        | `req.body`                   |
| Request headers     | `req.headers`                |
| Continue middleware | `next()`                     |
| Pass error          | `next(error)`                |
| Send response       | `res.send()`                 |
| JSON response       | `res.json()`                 |
| Status code         | `res.status()`               |
| Redirect            | `res.redirect()`             |
| Render template     | `res.render()`               |
| Static files        | `express.static()`           |
| JSON parser         | `express.json()`             |
| URL-encoded parser  | `express.urlencoded()`       |
| Error middleware    | `(err, req, res, next)`      |
| 404 handler         | `app.use((req, res) => ...)` |

---

# Middleware Type Quick Reference

| Type              | Purpose                        | Typical Syntax                         |
| ----------------- | ------------------------------ | -------------------------------------- |
| Application-level | Whole application              | `app.use()`                            |
| Router-level      | Group of routes                | `router.use()`                         |
| Route-specific    | One or selected routes         | `app.get(path, middleware, handler)`   |
| Error-handling    | Handle errors                  | `app.use((err, req, res, next) => {})` |
| Built-in          | Express-provided functionality | `express.json()`                       |
| Third-party       | External packages              | `cors`, `morgan`, `helmet`             |
| Custom            | Application-specific logic     | `function middleware(...) {}`          |

---

# Important Exam Points

## Express

```text
Express = Web framework built on Node.js
```

## Route

```javascript
app.get("/path", handler);
```

## Request

```javascript
req.params
req.query
req.body
req.headers
```

## Response

```javascript
res.send()
res.json()
res.status()
res.redirect()
res.render()
```

## Middleware

```javascript
(req, res, next)
```

## `next()`

```text
Passes control to the next middleware/handler.
```

## Application-level Middleware

```javascript
app.use(...)
```

## Router-level Middleware

```javascript
router.use(...)
```

## Router

```javascript
const router = express.Router();

app.use("/users", router);
```

## Static Files

```javascript
app.use(express.static("public"));
```

## Built-in Middleware

```javascript
express.json()
express.urlencoded()
express.static()
```

## Third-party Middleware

```text
morgan
helmet
cors
compression
cookie-parser
```

## Error Middleware

```javascript
(err, req, res, next)
```

## Middleware Order

```text
Application middleware
        ↓
Route-specific middleware
        ↓
Routes
        ↓
404 handler
        ↓
Error handler
```

---

# Key Takeaways

* Express is a Node.js web framework.
* `express()` creates the application.
* `app.listen()` starts the server.
* Routes define how requests are handled.
* `GET`, `POST`, `PUT`, and `DELETE` represent common HTTP operations.
* `req.params` accesses route parameters.
* `req.query` accesses query parameters.
* `req.body` accesses parsed request-body data.
* Route handlers contain the logic for requests.
* `res.send()` sends a response.
* `res.json()` sends JSON.
* `res.status()` sets the HTTP status code.
* `app.route()` groups methods for one path.
* `express.Router()` organizes routes into modules.
* Middleware runs during the request-response cycle.
* Middleware has access to `req`, `res`, and `next`.
* Middleware executes in the order it is added.
* `next()` continues the middleware chain.
* Sending a response without calling `next()` ends the cycle.
* Application-level middleware uses `app.use()`.
* Router-level middleware uses `router.use()`.
* Route-specific middleware can protect individual routes.
* `express.json()` parses JSON.
* `express.urlencoded()` parses URL-encoded data.
* `express.static()` serves static files.
* Third-party packages extend Express functionality.
* Custom middleware handles application-specific tasks.
* Error middleware uses `(err, req, res, next)`.
* Error-handling middleware belongs at the end of the middleware stack.
* `next(error)` passes errors to error-handling middleware.
* Middleware can perform authentication and validation.
* Express is commonly used for RESTful APIs.
* Good middleware should be focused, reusable, and properly ordered.

---

# Practical Skills

After this section, you should be able to:

* Install Express
* Create an Express server
* Create GET/POST/PUT/DELETE routes
* Understand route paths
* Use route parameters
* Use query parameters
* Access request data
* Send different response types
* Chain routes with `app.route()`
* Create modular routers
* Understand middleware
* Create application-level middleware
* Create router-level middleware
* Create route-specific middleware
* Use `next()`
* Create custom middleware
* Parse JSON requests
* Parse URL-encoded requests
* Serve static files
* Use third-party middleware
* Create authentication middleware
* Create validation middleware
* Handle errors
* Understand middleware order
* Create 404 handlers
* Handle asynchronous errors
* Use template engines
* Structure an Express application
* Build the foundation of a REST API

---

# Learning Checklist

## Express.js

* [x] Understand Express.js
* [x] Install Express
* [x] Create a basic Express application
* [x] Start an Express server
* [x] Understand routing
* [x] Use HTTP route methods
* [x] Use static route paths
* [x] Use route parameters
* [x] Use query parameters
* [x] Understand route handlers
* [x] Use response methods
* [x] Use `app.route()`
* [x] Use `express.Router()`

## Middleware

* [x] Understand middleware
* [x] Understand `req`, `res`, and `next`
* [x] Understand middleware flow
* [x] Understand `next()`
* [x] Understand application-level middleware
* [x] Understand router-level middleware
* [x] Understand route-specific middleware
* [x] Understand error-handling middleware
* [x] Understand built-in middleware
* [x] Understand third-party middleware
* [x] Create custom middleware
* [x] Create authentication middleware
* [x] Create validation middleware
* [x] Understand middleware execution order
* [x] Handle 404 responses
* [x] Understand async error handling
* [x] Apply middleware best practices

## Express Application

* [x] Serve static files
* [x] Understand template engines
* [x] Understand RESTful API structure
* [x] Understand Express project structure
* [x] Know basic Express best practices

---

# Core Principle

```text
Node.js
   ↓
Express
   ↓
Middleware
   ↓
Routing
   ↓
Business Logic
   ↓
Database / Services
   ↓
HTTP Response
```

Middleware sits between the incoming request and the final response.

It can:

```text
Inspect
   ↓
Modify
   ↓
Validate
   ↓
Authenticate
   ↓
Continue
   ↓
Route Handler
```

The key concept is:

```text
Request
   ↓
Middleware
   ↓
next()
   ↓
Next Middleware / Route
   ↓
Response
```

Or:

```text
Request
   ↓
Middleware
   ↓
Response
   ↓
END
```

Express makes it easier to build the server-side layer that connects HTTP requests to application logic, databases, and APIs.
