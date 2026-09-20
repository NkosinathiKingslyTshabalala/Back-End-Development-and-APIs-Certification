# Working with Node.js and Event-Driven Architecture

A focused study and practice repository covering the fundamentals of **Node.js**, its runtime environment, asynchronous programming, event-driven architecture, and the Event Loop.

This milestone is part of my **freeCodeCamp Back-End Development and APIs Certification** journey.

---

## Overview

Node.js is a JavaScript runtime built on Chrome's **V8 JavaScript engine** that allows JavaScript to run outside the browser.

Unlike browser-based JavaScript, Node.js is designed for **server-side development** and provides APIs for working with:

- Files
- Operating system resources
- Networking
- Databases
- Environment variables
- HTTP servers
- Command-line applications

Its **non-blocking, event-driven architecture** makes Node.js particularly effective for applications that handle many simultaneous I/O operations.

---

# What I Learned

## 1. Node.js vs Browser Runtime

Both Node.js and browsers execute JavaScript, but they operate in different environments.

### Node.js

- Designed for server-side applications
- Has file system access
- Provides networking APIs
- Can access environment variables
- Uses `global`
- Supports CommonJS and ES Modules
- Uses npm for package management
- Has greater access to the operating system

### Browser

- Designed for client-side applications
- Provides DOM APIs
- Provides browser UI APIs
- Uses `window` / `self`
- Runs inside a security sandbox
- Uses ES Modules and `<script>` tags
- Does not have direct operating-system file access

### Quick Comparison

| Feature | Node.js | Browser |
|---|---|---|
| File System | Yes | No direct access |
| Networking | TCP/UDP + HTTP APIs | Browser networking APIs |
| DOM | No | Yes |
| Global Object | `global` | `window` / `self` |
| Environment Variables | `process.env` | No |
| Security | Greater OS access | Sandboxed |
| Package Management | npm / yarn | CDN / bundler |

---

# 2. Why Use Node.js?

Node.js is well suited to applications that perform a large amount of **I/O work**.

Common use cases include:

- REST APIs
- Web servers
- Real-time applications
- Chat applications
- Microservices
- Data streaming
- Command-line tools
- Database-driven applications

### Advantages

- JavaScript can be used on both the front end and back end
- Non-blocking I/O
- Event-driven architecture
- Efficient handling of concurrent connections
- Large npm ecosystem
- Well suited for network applications

### Limitations

Node.js is not automatically the best choice for CPU-intensive workloads.

Heavy CPU operations can block the Event Loop and prevent other work from being processed efficiently.

Possible approaches include:

- Worker threads
- Separate microservices
- Native add-ons
- Moving CPU-intensive work to another suitable system

---

# 3. Installing Node.js

Download Node.js from the official Node.js website:

https://nodejs.org

For general development, use the **LTS (Long Term Support)** release.

After installation, verify Node.js and npm:

```bash
node --version
npm --version
```

Both commands should return version numbers.

### Troubleshooting

If the commands do not work:

- Restart the terminal
- Check that Node.js was added to the system `PATH`
- Restart the computer if necessary on Windows

---

# 4. Running Node.js Programs

Node.js programs normally use the `.js` extension.

Example:

```javascript
console.log('Hello from Node.js!');
```

Run the file from the terminal:

```bash
node app.js
```

The important pattern is:

```bash
node filename.js
```

---

# 5. Building a Basic HTTP Server

Node.js includes a built-in `http` module that can be used to create web servers.

```javascript
const http = require('http');

http.createServer((req, res) => {
  res.writeHead(200, {
    'Content-Type': 'text/plain'
  });

  res.end('Hello World!');
}).listen(8080);
```

Start the server:

```bash
node app.js
```

Then open:

```text
http://localhost:8080
```

The browser should display:

```text
Hello World!
```

### What happens?

```text
Browser
   ↓
HTTP Request
   ↓
Node.js Server
   ↓
Request Handler
   ↓
HTTP Response
   ↓
Browser
```

---

# 6. Asynchronous Programming

One of the most important concepts in Node.js is **non-blocking asynchronous programming**.

Node.js can start an operation and continue executing other code while waiting for the operation to finish.

For example:

```javascript
const fs = require('fs');

fs.readFile('myfile.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err);
    return;
  }

  console.log('File content:', data);
});

console.log('Reading file...');
```

The program does not stop and wait for the file operation.

Instead:

```text
Start
  ↓
Start file read
  ↓
Continue executing
  ↓
File finishes
  ↓
Callback executes
```

This is the foundation of Node.js's ability to efficiently handle many I/O operations.

---

# 7. Blocking vs Non-Blocking

## Blocking

```javascript
const data = fs.readFileSync('myfile.txt', 'utf8');

console.log(data);
```

Execution waits until the file has been completely read.

```text
Operation starts
      ↓
WAIT
      ↓
File finishes
      ↓
Continue
```

## Non-Blocking

```javascript
fs.readFile('myfile.txt', 'utf8', (err, data) => {
  console.log(data);
});

console.log('Continue running...');
```

Execution continues while the file is being read.

```text
Operation starts
      ↓
Continue executing
      ↓
Other work
      ↓
File finishes
      ↓
Callback executes
```

### Key idea

> **Blocking code waits. Non-blocking code continues.**

---

# 8. Node.js Architecture

Node.js uses an **event-driven, non-blocking architecture**.

The main concepts are:

- Single-threaded JavaScript execution
- Event Loop
- Event Queue
- Asynchronous operations
- Callbacks
- Thread Pool
- Non-blocking I/O

A simplified model:

```text
             Client Request
                    ↓
              Event Queue
                    ↓
                Event Loop
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
   Simple Task            I/O / Heavy Task
        ↓                       ↓
   Main Thread              Thread Pool
                                ↓
                           Completed Task
                                ↓
                         Callback Queue
                                ↓
                           Event Loop
                                ↓
                            Response
```

The Event Loop allows Node.js to continue processing other work instead of waiting for every I/O operation to finish.

---

# 9. Event Loop

The **Event Loop** is one of the core mechanisms behind Node.js's asynchronous behaviour.

It allows Node.js to process asynchronous operations without blocking the main JavaScript execution thread.

A simplified execution model is:

```text
1. Execute synchronous code
        ↓
2. Process microtasks
        ↓
3. Timers
        ↓
4. I/O callbacks
        ↓
5. Poll
        ↓
6. Check / setImmediate
        ↓
7. Close callbacks
```

Microtasks such as Promises and `process.nextTick()` are processed between Event Loop phases.

---

# 10. Event Loop Example

```javascript
console.log('First');

setTimeout(() => {
  console.log('Third');
}, 0);

Promise.resolve().then(() => {
  console.log('Second');
});

console.log('Fourth');
```

Output:

```text
First
Fourth
Second
Third
```

### Why?

Synchronous code runs first:

```text
First
Fourth
```

Then the Promise microtask:

```text
Second
```

Then the timer:

```text
Third
```

### General rule

```text
Synchronous code
       ↓
Microtasks
       ↓
Event Loop phases
```

---

# 11. Event Loop Phases

Important phases include:

### Timers

Handles:

```javascript
setTimeout()
setInterval()
```

### I/O Callbacks

Processes completed I/O operations.

Examples:

- File operations
- Network operations

### Poll

Handles incoming I/O events.

### Check

Handles:

```javascript
setImmediate()
```

### Close

Handles close events such as:

```javascript
socket.on('close')
```

---

# 12. Event-Driven Architecture

Node.js applications are built around **events**.

Instead of constantly waiting for an operation to finish, Node.js can respond when an event occurs.

Conceptually:

```text
Event occurs
     ↓
Event detected
     ↓
Callback / handler
     ↓
Execute response
```

Examples of events include:

- HTTP requests
- File completion
- Network activity
- Socket connections
- Timers
- Stream data

This architecture is particularly useful for:

- APIs
- Chat applications
- Real-time systems
- Streaming
- WebSockets
- Network applications

---

# 13. Node.js REPL

REPL stands for:

**Read → Evaluate → Print → Loop**

It provides an interactive Node.js environment.

Start it with:

```bash
node
```

Example:

```text
> 5 + 5
10

> console.log("Hello")
Hello
```

Exit with:

```text
.exit
```

The REPL is useful for quickly testing JavaScript and Node.js behaviour without creating a file.

---

# 14. Important Node.js Concepts

| Concept | Meaning |
|---|---|
| Node.js | JavaScript runtime outside the browser |
| V8 | JavaScript engine used by Node.js |
| Runtime | Environment where JavaScript executes |
| npm | Node.js package manager |
| Module | Reusable piece of code |
| `require()` | CommonJS module loading |
| Event Loop | Handles asynchronous operations |
| Callback | Function executed after an operation/event |
| Non-blocking | Code continues without waiting |
| Blocking | Execution waits for an operation |
| I/O | Input/output operations |
| REPL | Interactive Node.js environment |
| Thread Pool | Handles certain asynchronous tasks |
| `process.env` | Access to environment variables |

---

# Key Takeaways

```text
Node.js
   ↓
JavaScript outside the browser
   ↓
V8 Engine
   ↓
Event-Driven Architecture
   ↓
Non-Blocking I/O
   ↓
Event Loop
   ↓
High concurrency for I/O-heavy applications
```

The most important concepts from this milestone are:

- Node.js runs JavaScript outside the browser.
- Node.js is designed for server-side development.
- Node.js uses an event-driven architecture.
- Node.js uses non-blocking I/O.
- The Event Loop coordinates asynchronous work.
- Blocking operations can prevent the Event Loop from processing other work.
- Node.js is particularly effective for I/O-bound applications.
- Node.js can create HTTP servers and APIs.
- The Node.js REPL provides an interactive environment for testing code.
- The `http` and `fs` modules are examples of Node.js capabilities.

---

# Commands to Remember

```bash
node --version
npm --version
node
node app.js
```

Useful Node.js modules introduced:

```javascript
require('http');
require('fs');
```

---

# Practical Skills

By completing this milestone, I should be able to:

- Explain what Node.js is
- Explain Node.js vs browser JavaScript
- Install and verify Node.js
- Use the Node.js REPL
- Run JavaScript files with Node.js
- Create a basic HTTP server
- Understand blocking vs non-blocking operations
- Explain the Event Loop
- Explain event-driven architecture
- Understand callbacks and asynchronous operations
- Identify appropriate Node.js use cases
- Understand why CPU-heavy work can be problematic for the Event Loop

---

# Learning Checklist

- [x] Understand Node.js
- [x] Understand Node.js vs Browser
- [x] Understand Node.js advantages and disadvantages
- [x] Install Node.js
- [x] Verify Node and npm
- [x] Use Node.js REPL
- [x] Run a Node.js file
- [x] Create a basic HTTP server
- [x] Understand asynchronous programming
- [x] Understand blocking vs non-blocking code
- [x] Understand Node.js architecture
- [x] Understand the Event Loop
- [x] Understand Event Loop phases
- [x] Complete NodeJS Intro Review
- [x] Complete NodeJS Intro Quiz

---

# Certification Progress

**Course:** freeCodeCamp Back-End Development and APIs

**Section:** Introduction to Node.js

**Topic:** Working with Node.js and Event-Driven Architecture

**Status:** Completed

---

## Core Principle

> **Node.js does not become powerful because JavaScript is fast alone. Its strength comes from efficiently coordinating many I/O operations through asynchronous, non-blocking, event-driven execution.**