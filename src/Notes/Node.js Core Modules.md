# Node.js Core Modules

A focused study and practice repository covering **Node.js Core Modules**, including the File System (`fs`), Operating System (`os`), and Crypto (`crypto`) modules.

This milestone is part of my **freeCodeCamp Back-End Development and APIs Certification** journey.

---

## Overview

Node.js includes built-in modules that provide functionality without requiring external packages.

Core modules can be imported directly using:

```javascript
const module = require('module');
```

Important core modules covered in this milestone:

- `fs` — File System
- `os` — Operating System
- `crypto` — Cryptography

---

# What I Learned

## 1. Node.js Core Modules

Core modules are built into Node.js.

They do not need to be installed with npm.

Examples:

```javascript
const fs = require('fs');
const os = require('os');
const crypto = require('crypto');
```

Core modules provide functionality for:

- File operations
- Operating system information
- Cryptography
- Networking
- Streams
- Paths
- Processes

---

# 2. File System Module — `fs`

The `fs` module allows Node.js applications to interact with the computer's file system.

Import:

```javascript
const fs = require('fs');
```

Promise-based API:

```javascript
const fs = require('fs').promises;
```

ES Modules:

```javascript
import fs from 'fs';
```

---

## Reading Files

### Asynchronous

```javascript
const fs = require('fs');

fs.readFile('myfile.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(data);
});
```

### Promise / Async-Await

```javascript
const fs = require('fs').promises;

async function readFile() {
  try {
    const data = await fs.readFile('myfile.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}

readFile();
```

### Synchronous

```javascript
const fs = require('fs');

const data = fs.readFileSync('myfile.txt', 'utf8');

console.log(data);
```

### Important

```text
readFile()       → asynchronous
readFileSync()   → synchronous / blocking
```

Avoid synchronous file operations in production servers when they could block the Event Loop.

---

# 3. Writing Files

Use `writeFile()` to create or overwrite a file.

```javascript
const fs = require('fs').promises;

await fs.writeFile(
  'myfile.txt',
  'Hello, World!',
  'utf8'
);
```

### Append

`appendFile()` adds content without replacing existing content.

```javascript
await fs.appendFile(
  'app.log',
  'Application started\n',
  'utf8'
);
```

### Key Difference

```text
writeFile()   → creates / overwrites
appendFile()  → adds to existing file
```

---

# 4. File Handles

File handles provide more control over file operations.

```javascript
const fs = require('fs').promises;

const fileHandle = await fs.open('output.txt', 'w');

await fileHandle.write('First line\n');

await fileHandle.close();
```

Always close file handles when finished.

---

# 5. Streams

Streams are useful when working with large amounts of data.

Instead of loading an entire file into memory, data can be processed in smaller pieces.

```javascript
const fs = require('fs');

const readable = fs.createReadStream('large-file.txt');
const writable = fs.createWriteStream('copy.txt');

readable.pipe(writable);
```

### Key idea

```text
Large File
    ↓
Read small chunks
    ↓
Process
    ↓
Write chunks
```

Streams help reduce memory usage when handling large files.

---

# 6. File Flags

Common file flags:

| Flag | Purpose |
|---|---|
| `w` | Write / create / truncate |
| `wx` | Write but fail if file exists |
| `w+` | Read and write |
| `a` | Append / create |
| `ax` | Append but fail if file exists |
| `r+` | Read and write existing file |

---

# 7. Deleting Files

Use `unlink()`.

```javascript
const fs = require('fs').promises;

await fs.unlink('file.txt');
```

Check whether a file exists:

```javascript
await fs.access('file.txt');
```

For errors, `ENOENT` commonly indicates that a file or directory does not exist.

---

# 8. Deleting Directories

Modern Node.js provides `fs.rm()`.

```javascript
await fs.rm('my-directory', {
  recursive: true,
  force: true
});
```

### Important

Be extremely careful with:

```javascript
recursive: true
```

Incorrect paths can result in unintended deletion.

---

# 9. Renaming and Moving Files

`fs.rename()` can rename or move files.

```javascript
const fs = require('fs').promises;

await fs.rename(
  'old-name.txt',
  'new-name.txt'
);
```

Moving between directories:

```javascript
await fs.rename(
  'source/file.txt',
  'destination/file.txt'
);
```

---

# 10. OS Module — `os`

The `os` module provides information about the operating system.

Import:

```javascript
const os = require('os');
```

It can provide information about:

- Operating system
- CPU
- Memory
- User
- Hostname
- Network interfaces
- Uptime
- Temporary directories

---

# 11. Important `os` Methods

### Architecture

```javascript
os.arch();
```

Example:

```text
x64
arm64
```

### Platform

```javascript
os.platform();
```

Examples:

```text
win32
linux
darwin
```

### OS Type

```javascript
os.type();
```

### OS Release

```javascript
os.release();
```

### Kernel Version

```javascript
os.version();
```

---

# 12. User Information

Get current user information:

```javascript
os.userInfo();
```

Home directory:

```javascript
os.homedir();
```

Hostname:

```javascript
os.hostname();
```

Temporary directory:

```javascript
os.tmpdir();
```

---

# 13. System Resources

### CPU

```javascript
os.cpus();
```

Returns information about logical CPU cores.

Number of CPUs:

```javascript
os.cpus().length;
```

### Memory

Total memory:

```javascript
os.totalmem();
```

Free memory:

```javascript
os.freemem();
```

Both values are returned in **bytes**.

### Uptime

```javascript
os.uptime();
```

Returns system uptime in seconds.

---

# 14. Network Information

Use:

```javascript
os.networkInterfaces();
```

This provides information about network interfaces and addresses.

Example:

```javascript
const os = require('os');

console.log(os.networkInterfaces());
```

---

# 15. OS Constants and Utilities

### Constants

```javascript
os.constants;
```

Provides operating-system-specific constants.

### End-of-Line

```javascript
os.EOL;
```

Useful for cross-platform line endings.

Example:

```javascript
const content = [
  'First line',
  'Second line',
  'Third line'
].join(os.EOL);
```

---

# 16. Cross-Platform Development

Avoid manually constructing file paths:

```javascript
`${os.homedir()}/app/config.json`
```

Use the `path` module instead:

```javascript
const path = require('path');

const filePath = path.join(
  os.homedir(),
  'app',
  'config.json'
);
```

This helps applications work correctly across:

- Windows
- macOS
- Linux

---

# 17. Crypto Module — `crypto`

The `crypto` module provides cryptographic functionality.

Import:

```javascript
const crypto = require('crypto');
```

It can be used for:

- Hashing
- Password security
- HMAC
- Encryption
- Decryption
- Digital signatures
- Random data generation
- Key generation

---

# 18. Hashing

Hashing converts data into a fixed-length value.

Example:

```javascript
const crypto = require('crypto');

const hash = crypto
  .createHash('sha256')
  .update('Hello, Node.js!')
  .digest('hex');

console.log(hash);
```

### Important Properties

- Same input → same hash
- Fixed-size output
- One-way
- Small input change → very different hash

---

# 19. Hash Algorithms

Common algorithms include:

```text
MD5
SHA-1
SHA-256
SHA-512
```

For security-critical applications:

```text
Avoid MD5
Avoid SHA-1
Prefer modern algorithms
```

SHA-256 and SHA-512 are examples of stronger general-purpose hash functions.

---

# 20. Password Security

Passwords should **never** be stored as plain text.

Simple hashing alone is not sufficient for password storage.

Important concepts:

### Salt

A random value added to a password before hashing.

```text
Password + Salt
       ↓
    Hashing
       ↓
Stored Hash
```

### Key Stretching

Makes password hashing intentionally expensive to slow down brute-force attacks.

Node.js provides functions such as:

```javascript
crypto.scryptSync()
```

Example:

```javascript
const crypto = require('crypto');

const salt = crypto.randomBytes(16).toString('hex');

const hash = crypto
  .scryptSync('myPassword', salt, 64)
  .toString('hex');
```

For production applications, established password-hashing libraries such as bcrypt or Argon2 are commonly used.

---

# 21. HMAC

HMAC stands for:

**Hash-based Message Authentication Code**

It combines:

```text
Message
   +
Secret Key
   ↓
HMAC
```

It provides:

- Integrity
- Authentication

Example:

```javascript
const crypto = require('crypto');

const hmac = crypto
  .createHmac('sha256', 'secret-key')
  .update('Hello, World!')
  .digest('hex');

console.log(hmac);
```

### Important

HMAC does **not** encrypt data.

It verifies that data:

- Has not been modified
- Was generated by someone who possesses the secret key

---

# 22. Symmetric Encryption

Symmetric encryption uses the **same key** for encryption and decryption.

```text
Plaintext
   ↓
Encryption + Secret Key
   ↓
Ciphertext
   ↓
Decryption + Same Key
   ↓
Plaintext
```

Common algorithms include:

- AES
- ChaCha20

AES-GCM is an example of authenticated encryption.

---

# 23. Initialization Vector — IV

Encryption modes may require an initialization vector.

Generate a random IV:

```javascript
const iv = crypto.randomBytes(16);
```

Important:

> Never reuse the same IV with the same key when the encryption mode requires unique IVs.

---

# 24. Asymmetric Encryption

Asymmetric cryptography uses two keys:

```text
Public Key
Private Key
```

The public key can be shared.

The private key must remain secret.

Common algorithms include:

- RSA
- ECDSA
- Ed25519

### Simplified model

```text
Public Key
    ↓
Encrypt
    ↓
Encrypted Data
    ↓
Private Key
    ↓
Decrypt
```

Asymmetric cryptography is generally slower than symmetric encryption.

A **hybrid approach** is often used:

```text
Generate symmetric key
        ↓
Encrypt large data
        ↓
Encrypt symmetric key
using public key
```

---

# 25. Digital Signatures

Digital signatures help verify:

- Authenticity
- Integrity

Simplified model:

```text
Message
   ↓
Private Key
   ↓
Digital Signature
```

Verification:

```text
Message + Signature + Public Key
              ↓
           Valid?
```

A modified message should cause signature verification to fail.

---

# 26. Secure Random Data

Use:

```javascript
crypto.randomBytes();
```

Example:

```javascript
const crypto = require('crypto');

const randomBytes = crypto.randomBytes(16);

console.log(randomBytes.toString('hex'));
```

Useful for generating:

- Salts
- Keys
- IVs
- Tokens
- Other cryptographic random values

---

# 27. Cryptography Security Rules

Remember:

```text
Use modern algorithms
        ↓
Protect secret keys
        ↓
Use random salts / IVs where required
        ↓
Use authenticated encryption when appropriate
        ↓
Use secure comparisons
        ↓
Never hardcode secrets
```

For security-sensitive applications, use well-established libraries and follow current cryptographic practices.

---

# Core Modules Quick Reference

| Module | Purpose | Example |
|---|---|---|
| `fs` | File system operations | `fs.readFile()` |
| `os` | Operating system information | `os.cpus()` |
| `crypto` | Cryptography | `crypto.createHash()` |
| `path` | File paths | `path.join()` |
| `http` | HTTP servers | `http.createServer()` |

---

# Most Important Methods

## `fs`

```javascript
fs.readFile()
fs.readFileSync()
fs.writeFile()
fs.appendFile()
fs.unlink()
fs.rm()
fs.rename()
fs.access()
fs.readdir()
fs.mkdir()
```

## `os`

```javascript
os.arch()
os.platform()
os.type()
os.release()
os.version()
os.userInfo()
os.homedir()
os.hostname()
os.tmpdir()
os.cpus()
os.totalmem()
os.freemem()
os.loadavg()
os.networkInterfaces()
os.uptime()
os.EOL
```

## `crypto`

```javascript
crypto.createHash()
crypto.createHmac()
crypto.randomBytes()
crypto.scryptSync()
crypto.createCipheriv()
crypto.createDecipheriv()
crypto.generateKeyPairSync()
crypto.createSign()
crypto.createVerify()
crypto.timingSafeEqual()
```

---

# Key Takeaways

```text
Node.js Core Modules
        ↓
 ┌──────┼──────┐
 ↓      ↓      ↓
 fs     os    crypto
 ↓      ↓      ↓
Files  System  Security
```

The most important concepts:

- Core modules are built into Node.js.
- `fs` handles files and directories.
- `fs.readFile()` is asynchronous.
- `fs.readFileSync()` is blocking.
- Streams are useful for large files.
- `os` provides operating-system information.
- `crypto` provides cryptographic functionality.
- Hashing is different from encryption.
- HMAC provides integrity and authentication, not encryption.
- Symmetric encryption uses one shared key.
- Asymmetric cryptography uses public/private keys.
- Passwords require specialized secure hashing.
- Random values are important for salts, keys, and IVs.
- Sensitive cryptographic operations require careful key management.

---

# Commands to Remember

```bash
node --version
npm --version
node
node app.js
```

Import core modules:

```javascript
const fs = require('fs');
const os = require('os');
const crypto = require('crypto');
```

---

# Practical Skills

By completing this milestone, I should be able to:

- Explain what Node.js core modules are
- Import Node.js core modules
- Read files
- Write files
- Append to files
- Delete files
- Create and delete directories
- Rename and move files
- Understand synchronous vs asynchronous file operations
- Use streams for large files
- Retrieve operating-system information
- Retrieve CPU and memory information
- Retrieve network information
- Use cryptographic hashing
- Understand salts and password hashing
- Create HMACs
- Understand symmetric encryption
- Understand asymmetric encryption
- Generate secure random data
- Understand digital signatures
- Apply basic cryptographic security practices

---

# Learning Checklist

- [x] Working with Node Core Modules
- [x] File System (`fs`)
- [x] Reading files
- [x] Writing files
- [x] Appending files
- [x] Deleting files
- [x] Renaming and moving files
- [x] File streams
- [x] Operating System (`os`)
- [x] CPU information
- [x] Memory information
- [x] Network information
- [x] User/system information
- [x] Crypto (`crypto`)
- [x] Hashing
- [x] Password security
- [x] HMAC
- [x] Symmetric encryption
- [x] Asymmetric encryption
- [x] Digital signatures
- [x] Random data generation
- [x] Node JS Core Modules Review
- [x] NodeJS Core Modules Quiz

---

# Certification Progress

**Course:** freeCodeCamp Back-End Development and APIs

**Section:** Node.js Core Modules

**Status:** Completed

---

## Core Principle

> **Node.js core modules give applications direct access to essential capabilities such as files, system information, networking, and cryptography without requiring external packages.**