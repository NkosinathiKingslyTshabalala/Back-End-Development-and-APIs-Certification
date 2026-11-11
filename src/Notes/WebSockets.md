# WebSockets

WebSockets allow a client and server to communicate in real time through a persistent, bidirectional connection.

They are commonly used in:

- Chat applications
- Multiplayer games
- Live sports updates
- Stock market dashboards
- Notifications
- Collaborative applications
- IoT applications

---

# 1. What Are WebSockets?

A **WebSocket** is a communication protocol that allows a client and server to exchange data in real time over an open connection.

Unlike the traditional HTTP request-response model, WebSockets allow both the client and server to send messages whenever necessary.

## HTTP Communication

HTTP normally follows a request-response model.

1. The client sends a request.
2. The server processes the request.
3. The server sends a response.

```text
Client
   |
   | Request
   ↓
Server
   |
   | Response
   ↓
Client
```

For real-time applications, the client may need to repeatedly send requests to check whether new information is available.

This is known as polling.

### Problem with HTTP Polling

Imagine a chat application using HTTP.

The client repeatedly asks the server:

```text
Client → Any new messages?
Server → No.

Client → Any new messages?
Server → Yes. Here is a message.

Client → Any new messages?
Server → No.
```

This creates repeated requests, even when there is no new information.

## WebSocket Communication

WebSockets solve this problem by keeping a connection open.

Once connected:

- The client can send messages.
- The server can send messages.
- Both sides can communicate independently.
- The connection remains open until it is closed.

```text
Client  ←──────────────→  Server

       Bidirectional
       Communication
```

### Main Benefits of WebSockets

| Benefit | Meaning |
|---|---|
| Real-time updates | Data can be delivered immediately |
| Persistent connection | The connection remains open |
| Bidirectional | Client and server can both send messages |
| Efficient | Avoids repeatedly requesting updates |
| Low latency | Messages can travel over the existing connection |

---

# 2. WebSockets vs HTTP

| Feature | WebSockets | HTTP |
|---|---|---|
| Communication | Bidirectional | Request-response |
| Connection | Persistent | Requests and responses |
| Data flow | Both sides can send data | Client initiates requests |
| Overhead | Less repeated request overhead after handshake | HTTP headers accompany requests |
| Best use | Real-time applications | Traditional web pages and APIs |
| Examples | Chat and live updates | Loading pages and submitting forms |

### Easy Way to Remember

**HTTP = Exchanging letters**

- Send a request.
- Wait for a response.
- Send another request when needed.

**WebSockets = Phone call**

- Establish a connection.
- Both parties can communicate.
- Communication continues until someone ends the connection.

---

# 3. How a WebSocket Connection Starts

Even though WebSockets and HTTP are different protocols, a WebSocket connection initially starts with an HTTP handshake.

This process upgrades the connection from HTTP to WebSocket.

## WebSocket Handshake

1. The client connects to the server using HTTP.
2. The client requests an upgrade to WebSocket.
3. The server accepts the upgrade.
4. The server responds with HTTP status `101 Switching Protocols`.
5. The connection becomes a WebSocket connection.
6. Both sides can exchange messages in real time.

```text
Client
   |
   | HTTP Connection
   ↓
Server
   |
   | Upgrade Request
   ↓
Server Accepts Upgrade
   |
   | 101 Switching Protocols
   ↓
WebSocket Connection
   |
   | ←──── Messages ────→
   |
   ↓
Connection Closes
```

### Important Exam Point

`101 Switching Protocols` means the server has accepted the protocol upgrade.

### WebSocket URLs

| Protocol | URL Prefix |
|---|---|
| WebSocket | `ws://` |
| Secure WebSocket | `wss://` |

Example:

```text
ws://localhost:3000
wss://example.com
```

Use `wss://` for secure WebSocket connections.

---

# 4. Real-World Uses of WebSockets

WebSockets are useful when applications need immediate updates.

| Application | How WebSockets Are Used |
|---|---|
| Chat applications | Instant message delivery |
| Multiplayer games | Exchange player actions and game events |
| Live sports | Display goals and match updates |
| Stock market dashboards | Deliver changing market information |
| Collaborative tools | Synchronise changes between users |
| Notifications | Send updates without repeated polling |
| IoT applications | Monitor and control connected devices |

### Example: Live Football Scores

```text
Football Match
      ↓
Goal Scored
      ↓
Server Sends Update
      ↓
WebSocket Connection
      ↓
Connected Users
      ↓
Score Updates Instantly
```

A live football score application benefits more from WebSockets than a static blog because the score changes while users are viewing the application.

---

# 5. Pub/Sub Architecture

## What Does Pub/Sub Mean?

**Pub/Sub** stands for **Publish/Subscribe**.

It is a messaging architecture that allows different parts of a system to communicate without needing to know about each other directly.

Instead of sending messages directly to individual recipients, publishers send messages to topics.

Subscribers receive messages from the topics they follow.

## Three Main Parts of Pub/Sub

### 1. Publishers

Publishers produce and send messages to topics.

Example:

A sports application publishes a message when a goal is scored.

### 2. Topics

Topics are channels or groups where messages are published.

Examples:

```text
football-updates
chelsea-fc
room-a
room-b
```

### 3. Subscribers

Subscribers subscribe to topics and receive messages published to those topics.

## Pub/Sub Flow

1. A subscriber subscribes to a topic.
2. A publisher sends a message to the topic.
3. The messaging system receives the message.
4. The messaging system delivers the message to subscribers of that topic.

```text
Publisher
    |
    | Publish Message
    ↓
  Topic
    |
    | Distribute Message
    ↓
Subscribers
    ├── Subscriber 1
    ├── Subscriber 2
    └── Subscriber 3
```

---

# 6. Example of Pub/Sub

Imagine a sports news application.

Users subscribe to updates for their favourite football teams.

Topics:

```text
football-updates
chelsea-fc
arsenal-fc
```

When Chelsea scores:

```text
Chelsea Goal
     ↓
Publisher
     ↓
Topic: chelsea-fc
     ↓
Subscribers of chelsea-fc
     ├── User 1
     ├── User 2
     └── User 3
```

Only users subscribed to `chelsea-fc` receive the update.

Users subscribed to `arsenal-fc` do not receive the Chelsea update.

The publisher does not need to know who the subscribers are.

It only needs to publish the message to the correct topic.

## Pub/Sub in Chat Applications

Imagine an application with two chat rooms.

```text
Room A → room-a
Room B → room-b
```

When someone sends a message in Room A:

```text
User Sends Message
        ↓
     Publisher
        ↓
    Topic: room-a
        ↓
   Room A Subscribers
```

Only people subscribed to Room A receive the message.

Room B users do not receive it.

---

# 7. Advantages of Pub/Sub

## Separation of Concerns

Publishers and subscribers do not need to communicate directly.

The messaging system handles delivery.

## Reduced Dependency

Without Pub/Sub:

```text
Application A
      |
      ↓
Application B
```

Application A directly depends on Application B.

With Pub/Sub:

```text
Application A
      |
      ↓
    Topic
      |
      ↓
  Subscribers
```

Application A only needs to publish messages.

It does not need to know who receives them.

## Maintainability

Applications can be changed more independently.

## Expandability

New subscribers can be added without changing the publisher.

## Scalability

Messages can be distributed to multiple subscribers through the messaging system.

### Key Idea

Pub/Sub separates the sender from the receivers.

---

# 8. Pub/Sub vs WebSockets

These technologies are related, but they are not the same.

| WebSockets | Pub/Sub |
|---|---|
| Communication protocol | Messaging architecture |
| Provides an open communication channel | Defines how messages are distributed |
| Allows real-time bidirectional communication | Allows publishers and subscribers to communicate indirectly |
| Connects clients and servers | Connects publishers, topics and subscribers |

### WebSockets

Provide the communication channel through which data moves between a client and server.

### Pub/Sub

Determines which subscribers should receive particular messages.

### Easy Way to Remember

```text
WEBSOCKETS = THE ROAD

PUB/SUB = THE TRAFFIC SYSTEM
```

WebSockets allow messages to travel.

Pub/Sub decides where messages should go.

## Using Both Together

Many real-time applications use both technologies.

```text
Publisher
    |
    ↓
Pub/Sub Topic
    |
    ↓
Messaging System
    |
    ↓
WebSocket Server
    |
    ↓
WebSocket Connections
    |
    ├── Client 1
    ├── Client 2
    └── Client 3
```

Pub/Sub manages message distribution, while WebSockets deliver messages to connected clients.

---

# 9. WebSockets in Node.js

Node.js does not have a built-in WebSocket server.

Developers commonly use external packages such as **`ws`** to implement WebSocket communication.

## What Is the `ws` Library?

`ws` is a lightweight WebSocket library for Node.js.

It provides functionality to:

- Create WebSocket servers.
- Connect WebSocket clients.
- Send messages.
- Receive messages.
- Handle connection events.
- Broadcast messages.

## Installing `ws`

Create a project:

```bash
mkdir websocket-demo
cd websocket-demo
npm init -y
```

Install the package:

```bash
npm install ws
```

The package is added to `package.json`.

---

# 10. Creating a WebSocket Server

Import the `ws` library:

```javascript
const WebSocket = require("ws");
```

Create a WebSocket server on port 3000:

```javascript
const WebSocket = require("ws");

const server = new WebSocket.Server({
  port: 3000
});
```

The server listens for WebSocket connections on port `3000`.

## Complete Basic Server

```javascript
const WebSocket = require("ws");

const server = new WebSocket.Server({
  port: 3000
});

console.log("WebSocket server running on port 3000");

server.on("connection", (socket) => {
  console.log("Client connected");

  socket.send("Hello from the server");

  socket.on("message", (message) => {
    console.log("Received:", message.toString());
  });

  socket.on("close", () => {
    console.log("Client disconnected");
  });

  socket.on("error", (error) => {
    console.error("WebSocket error:", error);
  });
});
```

---

# 11. Handling Connection Events

When a client connects, the server emits a `connection` event.

```javascript
server.on("connection", (socket) => {
  console.log("Client connected");
});
```

### Important

- `server` represents the WebSocket server.
- `socket` represents the connection with an individual client.

You use the socket to send and receive messages.

---

# 12. Receiving Messages

When a connected client sends data, the socket emits a `message` event.

```javascript
server.on("connection", (socket) => {

  socket.on("message", (message) => {
    console.log(message.toString());

  });

});
```

### Important

`message` is triggered when the server receives data from the connected client.

The example converts the received message to a string using:

```javascript
message.toString()
```

---

# 13. Sending Messages

The `send()` method sends a message through an open WebSocket connection.

```javascript
socket.send("Hello from the server");
```

The client can also send messages:

```javascript
ws.send("Hello from the client");
```

As long as the connection remains open, both sides can continue exchanging messages.

---

# 14. Handling Close and Error Events

WebSockets use events to manage connections.

## Close Event

The `close` event is triggered when a connection closes.

```javascript
socket.on("close", () => {
  console.log("Disconnected");
});
```

## Error Event

The `error` event is triggered when a connection encounters an error.

```javascript
socket.on("error", (error) => {
  console.error(error);
});
```

### Important WebSocket Events

| Event | Meaning |
|---|---|
| `connection` | Server receives a new client connection |
| `open` | Client connection is established |
| `message` | A message is received |
| `close` | Connection is closed |
| `error` | An error occurs |

---

# 15. Checking Connection State

Every WebSocket connection has a `readyState` property.

It represents the current connection state.

Important WebSocket states:

| State | Meaning |
|---|---|
| `CONNECTING` | Connection is being established |
| `OPEN` | Connection is open and ready |
| `CLOSING` | Connection is closing |
| `CLOSED` | Connection is closed |

Check whether a connection is open:

```javascript
if (client.readyState === WebSocket.OPEN) {
  client.send("Hello");
}
```

### Why Check `WebSocket.OPEN`?

Before sending a message, the server should check whether the connection is ready.

This prevents attempts to send messages to connections that are not open.

---

# 16. Broadcasting Messages

## What Is Broadcasting?

Broadcasting means sending a message to multiple connected clients instead of just one.

Example:

A chat room has three users:

- John Doe
- Jane Doe
- Wes Smith

When John sends a message, the server can forward it to all connected users.

## Broadcasting with `ws`

```javascript
server.on("connection", (socket) => {

  socket.on("message", (message) => {

    server.clients.forEach((client) => {

      if (client.readyState === WebSocket.OPEN) {

        client.send(message.toString());

      }

    });

  });

});
```

### How It Works

1. A client connects.
2. The client sends a message.
3. The server receives the message.
4. The server loops through `server.clients`.
5. It checks whether each connection is open.
6. It sends the message to each open connection.

### Broadcasting Flow

```text
Client 1 Sends Message
        |
        ↓
   WebSocket Server
        |
        ↓
 server.clients
        |
        ├── Client 1
        ├── Client 2
        └── Client 3

Message sent to open connections
```

**Important:** This example broadcasts to all open clients, including the sender.

---

# 17. Complete WebSocket Broadcast Server

```javascript
const WebSocket = require("ws");

const server = new WebSocket.Server({
  port: 3000
});

console.log("Server running on port 3000");

server.on("connection", (socket) => {

  console.log("Client connected");

  socket.on("message", (message) => {

    console.log("Received:", message.toString());

    server.clients.forEach((client) => {

      if (client.readyState === WebSocket.OPEN) {

        client.send(message.toString());

      }

    });

  });

  socket.on("close", () => {
    console.log("Client disconnected");
  });

  socket.on("error", (error) => {
    console.error(error);
  });

});
```

This server:

- Creates a WebSocket server.
- Accepts client connections.
- Receives messages.
- Broadcasts messages to open connections.
- Handles disconnections.
- Handles errors.

---

# 18. Creating a WebSocket Client

A client connects to the WebSocket server using its WebSocket URL.

Example Node.js client:

```javascript
const WebSocket = require("ws");

const ws = new WebSocket("ws://localhost:3000");
```

## Client Connection

```javascript
ws.on("open", () => {
  console.log("Connected to server");
});
```

## Receiving Server Messages

```javascript
ws.on("message", (message) => {
  console.log("Server:", message.toString());
});
```

## Sending a Message

```javascript
ws.send("Hello from the client");
```

## Handling Errors

```javascript
ws.on("error", (error) => {
  console.error("WebSocket error:", error);
});
```

## Handling Disconnection

```javascript
ws.on("close", () => {
  console.log("Disconnected from server");
});
```

---

# 19. Browser WebSocket Client

Browsers provide a built-in WebSocket API.

You do not need to install the Node.js `ws` package in browser JavaScript.

Connect:

```javascript
const ws = new WebSocket("ws://localhost:3000");
```

## Browser Events

### Connection Opens

```javascript
ws.onopen = () => {
  console.log("Connected to server");
};
```

### Receive Messages

```javascript
ws.onmessage = (event) => {
  console.log("Server:", event.data);
};
```

### Send Messages

```javascript
ws.send("Hello from the browser");
```

### Handle Errors

```javascript
ws.onerror = (error) => {
  console.error("WebSocket error:", error);
};
```

### Connection Closes

```javascript
ws.onclose = () => {
  console.log("Disconnected from server");
};
```

## Browser Client Flow

```text
Browser
   |
   | new WebSocket(url)
   ↓
WebSocket Server
   |
   | Connection Established
   ↓
    open
   |
   | Send Message
   ↓
   ws.send()
   |
   | Receive Message
   ↓
  onmessage
```

---

# 20. Testing a WebSocket Application

To test a basic WebSocket application:

1. Save the server code as `server.js`.
2. Start the server.
3. Connect a client.
4. Open multiple clients to test broadcasting.
5. Send messages from different clients.
6. Confirm that connected clients receive the messages.

Run the server:

```bash
node server.js
```

Example:

```text
Server running on port 3000
Client connected
Client connected
Received: Hello everyone
```

### Testing Multiple Clients

```text
          WebSocket Server
                 |
       ┌─────────┼─────────┐
       ↓         ↓         ↓
    Client 1  Client 2  Client 3
```

When one client sends a message, the server can broadcast it to every connected client.

---

# 21. Binary Data Transfer

WebSockets can transfer binary data as well as text.

Binary data is useful when sending data such as buffers or other non-text information.

## Sending Binary Data

```javascript
const buffer = Buffer.from([
  0x48,
  0x65,
  0x6c,
  0x6c,
  0x6f
]);

ws.send(buffer, {
  binary: true
});
```

The buffer represents the word `Hello` in binary byte values.

## Receiving Binary Data in a Browser

```javascript
ws.binaryType = "arraybuffer";

ws.onmessage = (event) => {

  if (event.data instanceof ArrayBuffer) {

    const view = new Uint8Array(event.data);

    console.log("Received binary data:", view);

  }

};
```

### Key Point

WebSockets support both:

- Text messages
- Binary messages

---

# 22. Heartbeats and Connection Monitoring

A heartbeat mechanism helps the server identify connections that are no longer responding.

The `ping` and `pong` frames can be used to check whether a connection is alive.

## Heartbeat Example

```javascript
function setupHeartbeat(ws) {

  ws.isAlive = true;

  ws.on("pong", () => {
    ws.isAlive = true;
  });

}
```

## Checking Connected Clients

```javascript
const interval = setInterval(() => {

  server.clients.forEach((ws) => {

    if (ws.isAlive === false) {
      return ws.terminate();
    }

    ws.isAlive = false;

    ws.ping();

  });

}, 30000);
```

### How It Works

1. The server sends a ping.
2. The client responds with a pong.
3. The server marks the connection as alive.
4. If the connection does not respond, the server can terminate it.

Clear the interval when the server closes:

```javascript
server.on("close", () => {
  clearInterval(interval);
});
```

**Purpose:** Detect and clean up disconnected or unresponsive clients.

---

# 23. WebSocket Security

WebSocket applications should implement security measures.

## Authentication

Authenticate connections so that only authorized users can access protected functionality.

The uploaded reference demonstrates using JWT verification during the WebSocket upgrade process.

General flow:

```text
Client Connection Request
          ↓
Check Authentication Token
          ↓
Is Token Valid?
      /       \
    Yes        No
     |          |
     ↓          ↓
Establish    Reject
Connection  Connection
```

## Rate Limiting

Rate limiting restricts how many messages a client can send within a given time.

Example configuration from the reference:

```javascript
const rateLimit = require("ws-rate-limit");

const limiter = rateLimit({
  windowMs: 60 * 1000,
  max: 100,
  message: "Too many messages, please slow down!"
});
```

Apply it:

```javascript
server.on("connection", (ws) => {

  limiter(ws);

});
```

The example allows up to 100 messages per minute per connection.

## Input Validation

Always validate incoming messages before processing them.

Example using Joi:

```javascript
const Joi = require("joi");

const messageSchema = Joi.object({

  type: Joi.string()
    .valid("chat", "join", "leave")
    .required(),

  username: Joi.string()
    .alphanum()
    .min(3)
    .max(30),

  message: Joi.string()
    .max(1000),

  room: Joi.string()
    .alphanum()
    .max(50)

});
```

Validate messages:

```javascript
ws.on("message", (data) => {

  try {

    const message = JSON.parse(data);

    const { error, value } =
      messageSchema.validate(message);

    if (error) {
      throw new Error("Invalid message");
    }

    // Process valid message

  } catch (err) {

    ws.send(JSON.stringify({
      error: err.message
    }));

  }

});
```

### Security Checklist

- Authenticate connections.
- Validate incoming messages.
- Apply rate limiting.
- Use secure WebSocket connections (`wss://`).
- Handle errors safely.
- Avoid exposing sensitive server information.

---

# 24. Performance Optimisation

## Compression

WebSocket messages can be compressed to reduce bandwidth usage.

The `ws` library supports per-message compression.

Example:

```javascript
const WebSocket = require("ws");

const server = new WebSocket.Server({

  port: 8080,

  perMessageDeflate: {
    zlibDeflateOptions: {
      chunkSize: 1024,
      memLevel: 7,
      level: 3
    },

    zlibInflateOptions: {
      chunkSize: 10 * 1024
    },

    clientNoContextTakeover: true,
    serverNoContextTakeover: true,
    concurrencyLimit: 10

  }

});
```

### Purpose

Compression can:

- Reduce message size.
- Reduce bandwidth usage.
- Improve efficiency for suitable workloads.

Compression also uses CPU and memory, so it should be configured based on the application.

## Socket.IO

Socket.IO is another library used for real-time communication.

It provides additional features, including fallback mechanisms and other connection-management functionality.

**Important:** Socket.IO and the native WebSocket protocol are not identical and are not directly interchangeable. They use different protocols and APIs.

---

# 25. Quick Reference

## WebSockets vs HTTP

| Concept | WebSockets | HTTP |
|---|---|---|
| Communication | Bidirectional | Request-response |
| Connection | Persistent | Request-based |
| Real-time updates | Yes | Usually requires repeated requests or another mechanism |
| Main use | Chat, live updates, games | Web pages and APIs |

## WebSocket Handshake

| Term | Meaning |
|---|---|
| HTTP handshake | Initial connection process |
| Upgrade | Request to change protocol |
| `101` | Switching Protocols |
| `ws://` | WebSocket connection |
| `wss://` | Secure WebSocket connection |

## Pub/Sub

| Term | Meaning |
|---|---|
| Publisher | Sends messages |
| Topic | Channel that receives messages |
| Subscriber | Receives messages |
| Publish | Send a message to a topic |
| Subscribe | Listen to a topic |

## `ws` Library

| Code | Purpose |
|---|---|
| `require("ws")` | Import library |
| `new WebSocket.Server({ port: 3000 })` | Create server |
| `server.on("connection", ...)` | Handle connections |
| `socket.on("message", ...)` | Receive messages |
| `socket.send()` | Send messages |
| `socket.on("close", ...)` | Handle disconnection |
| `socket.on("error", ...)` | Handle errors |
| `WebSocket.OPEN` | Check open connection |
| `server.clients` | Access connected clients |
| `client.readyState` | Check connection state |

## WebSocket Events

| Event | Meaning |
|---|---|
| `connection` | Client connects to server |
| `open` | Client connection opens |
| `message` | Message is received |
| `close` | Connection closes |
| `error` | Connection error occurs |

## Connection States

| State | Meaning |
|---|---|
| `CONNECTING` | Connecting |
| `OPEN` | Connection open |
| `CLOSING` | Closing |
| `CLOSED` | Closed |

---

# 26. Important Exam Points

**1. What problem do WebSockets solve?**

HTTP requires clients to repeatedly ask the server for new data when using polling. WebSockets allow data to be exchanged over a persistent connection.

**2. How does a WebSocket connection begin?**

It starts with an HTTP handshake. The client requests an upgrade, and the server responds with `101 Switching Protocols` when accepting it.

**3. Which application benefits most from WebSockets?**

A live football score update application.

**4. What does Pub/Sub stand for?**

Publish/Subscribe.

**5. What are the three main parts of Pub/Sub?**

Publishers, topics and subscribers.

**6. What is the main advantage of Pub/Sub?**

It separates publishers and subscribers, reducing their direct dependency on each other.

**7. How do WebSockets and Pub/Sub differ?**

WebSockets provide the communication channel, while Pub/Sub provides the messaging pattern.

**8. Which event is triggered when a WebSocket connection closes?**

`close`.

**9. What is required to broadcast messages to connected clients?**

Loop through `server.clients` and send only when `client.readyState === WebSocket.OPEN`.

**10. How do you create a WebSocket server on port 3000 using the supplied `ws` API?**

```javascript
const WebSocket = require("ws");

const server = new WebSocket.Server({
  port: 3000
});
```

---

# 27. Practical Skills Checklist

## WebSocket Fundamentals

- [ ] Understand WebSockets.
- [ ] Explain how WebSockets differ from HTTP.
- [ ] Understand persistent connections.
- [ ] Understand bidirectional communication.
- [ ] Explain the HTTP handshake.
- [ ] Understand `101 Switching Protocols`.
- [ ] Identify real-world uses of WebSockets.

## Pub/Sub Architecture

- [ ] Understand Publish/Subscribe.
- [ ] Identify publishers.
- [ ] Identify topics.
- [ ] Identify subscribers.
- [ ] Explain how messages are distributed.
- [ ] Explain separation of concerns.
- [ ] Distinguish Pub/Sub from WebSockets.

## Node.js and `ws`

- [ ] Install the `ws` package.
- [ ] Create a WebSocket server.
- [ ] Listen for connections.
- [ ] Receive messages.
- [ ] Send messages.
- [ ] Handle close events.
- [ ] Handle error events.
- [ ] Create a Node.js WebSocket client.
- [ ] Create a browser WebSocket client.
- [ ] Check connection states.
- [ ] Broadcast messages.
- [ ] Test multiple clients.

## Advanced WebSockets

- [ ] Understand binary data transfer.
- [ ] Understand heartbeats.
- [ ] Monitor connection health.
- [ ] Understand authentication.
- [ ] Apply rate limiting.
- [ ] Validate incoming messages.
- [ ] Understand compression.
- [ ] Understand Socket.IO.

---

# Core Principles

```text
HTTP
Client → Request → Server
Client ← Response ← Server
```

```text
WEBSOCKETS
Client ←────────→ Server
      Persistent
      Connection
```

```text
PUB/SUB
Publisher
    ↓
  Topic
    ↓
Subscribers
```

```text
NODE.JS WEBSOCKET SERVER
Create Server
     ↓
Listen for Connection
     ↓
Receive Message
     ↓
Process Message
     ↓
Send / Broadcast
     ↓
Handle Close and Error
```

**Final takeaway:**

- HTTP follows a request-response model.
- WebSockets provide persistent, bidirectional communication.
- Pub/Sub separates message publishers from subscribers.
- The `ws` library allows Node.js to create WebSocket servers and clients.
- Broadcasting sends messages to multiple connected clients.
- `readyState === WebSocket.OPEN` checks whether a connection can send messages.
- Authentication, validation, rate limiting and connection monitoring help make WebSocket applications safer and more reliable.