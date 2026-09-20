# Node Package Manager

A focused study and practice repository covering **npm (Node Package Manager)**, including package installation, dependency management, semantic versioning, `package.json`, `package-lock.json`, npm scripts, publishing packages, and JavaScript module imports/exports.

This milestone is part of my **freeCodeCamp Back-End Development and APIs Certification** journey.

---

## Overview

**npm** is the default package manager for Node.js.

It allows developers to:

- Install packages
- Remove packages
- Update dependencies
- Manage project dependencies
- Run project scripts
- Publish packages
- Manage package versions
- Share reusable JavaScript modules

The npm registry contains thousands of reusable packages.

---

# What I Learned

## 1. What Is npm?

npm stands for:

**Node Package Manager**

It is installed automatically with Node.js.

Check versions:

```bash
node --version
npm --version
```

npm allows projects to use external packages instead of building everything from scratch.

---

# 2. Packages

A **package** is a collection of files containing reusable code.

Install a package:

```bash
npm install package-name
```

Example:

```bash
npm install express
```

npm normally installs packages into:

```text
node_modules/
```

Example:

```text
my-project/
├── node_modules/
├── package.json
└── index.js
```

---

# 3. Installing Packages

Install a package:

```bash
npm install express
```

Install a specific version:

```bash
npm install express@4.17.1
```

Install globally:

```bash
npm install -g nodemon
```

Global packages are generally used for command-line tools.

---

# 4. Using an Installed Package

CommonJS:

```javascript
const express = require('express');
```

ES Modules:

```javascript
import express from 'express';
```

The package must be installed before it can normally be imported from `node_modules`.

---

# 5. Global vs Local Packages

### Local

```bash
npm install package-name
```

Installed inside the current project.

Used by the application.

### Global

```bash
npm install -g package-name
```

Installed system-wide.

Typically used for CLI tools.

Example:

```bash
npm install -g http-server
```

Then:

```bash
http-server
```

---

# 6. package.json

`package.json` is the central configuration file for a Node.js project.

It contains information such as:

- Project name
- Version
- Description
- Entry point
- Scripts
- Dependencies
- Development dependencies
- License
- Author
- Project metadata

Create one:

```bash
npm init
```

Create one with default values:

```bash
npm init -y
```

---

# 7. Basic package.json

Example:

```json
{
  "name": "my-node-app",
  "version": "1.0.0",
  "description": "A simple Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "Your Name",
  "license": "MIT"
}
```

---

# 8. Important package.json Fields

| Field | Purpose |
|---|---|
| `name` | Package/project name |
| `version` | Current version |
| `description` | Project description |
| `main` | Main entry point |
| `type` | Module system |
| `scripts` | Automation commands |
| `dependencies` | Production dependencies |
| `devDependencies` | Development-only dependencies |
| `keywords` | Search/discovery terms |
| `author` | Package author |
| `license` | License information |
| `engines` | Node.js/npm requirements |
| `repository` | Source repository |
| `bugs` | Issue tracker |

---

# 9. Module Type

CommonJS:

```json
{
  "type": "commonjs"
}
```

ES Modules:

```json
{
  "type": "module"
}
```

CommonJS:

```javascript
const fs = require('fs');
```

ES Modules:

```javascript
import fs from 'fs';
```

Exports also differ between the two module systems.

---

# 10. Dependencies

Dependencies are external packages required by an application.

Install one:

```bash
npm install express
```

This adds the package to:

```json
"dependencies": {
  "express": "^5.1.0"
}
```

Dependencies are normally required for the application to run.

---

# 11. Development Dependencies

Development dependencies are packages used during development rather than by the production application itself.

Install:

```bash
npm install jest --save-dev
```

or:

```bash
npm install jest -D
```

Example:

```json
"devDependencies": {
  "jest": "^29.5.0",
  "eslint": "^8.38.0"
}
```

Typical examples:

- Testing tools
- Linters
- Formatters
- Build tools
- Development servers

---

# 12. Types of Dependencies

### Regular Dependencies

```bash
npm install express
```

Used by the application.

### Development Dependencies

```bash
npm install jest --save-dev
```

Used during development/testing.

### Peer Dependencies

Declare packages that another package expects the user to provide.

```json
"peerDependencies": {
  "react": "^17.0.0"
}
```

### Optional Dependencies

Packages that provide additional functionality but are not essential.

```bash
npm install package-name --save-optional
```

---

# 13. Semantic Versioning

npm packages commonly use **Semantic Versioning (SemVer)**.

Format:

```text
MAJOR.MINOR.PATCH
```

Example:

```text
4.17.21
│  │  │
│  │  └── PATCH
│  └───── MINOR
└──────── MAJOR
```

### MAJOR

Breaking/incompatible changes.

```text
4.x.x → 5.x.x
```

### MINOR

Backward-compatible features.

```text
4.17.x → 4.18.x
```

### PATCH

Backward-compatible bug fixes.

```text
4.17.21 → 4.17.22
```

---

# 14. Version Ranges

| Syntax | Meaning |
|---|---|
| `^2.8.1` | Compatible releases within major version 2 |
| `~2.8.1` | Compatible patch releases within 2.8.x |
| `2.8.1` | Exact version |
| `>=2.8.1` | 2.8.1 or higher |
| `*` | Any version |
| `2.x` | Any compatible 2.x release |

Example:

```json
{
  "dependencies": {
    "express": "^4.18.2",
    "lodash": "~4.17.21",
    "axios": "1.2.3"
  }
}
```

---

# 15. Installing Dependencies

Install everything listed in `package.json`:

```bash
npm install
```

Install a specific package:

```bash
npm install express
```

Install an exact version:

```bash
npm install express@4.17.1
```

Install without modifying `package.json`:

```bash
npm install express --no-save
```

---

# 16. Removing Dependencies

Remove a local package:

```bash
npm uninstall package-name
```

Remove a global package:

```bash
npm uninstall -g package-name
```

Removing a dependency also updates the project's dependency information.

---

# 17. Updating Dependencies

Check outdated packages:

```bash
npm outdated
```

Update one package:

```bash
npm update package-name
```

Update all compatible dependencies:

```bash
npm update
```

Update npm itself:

```bash
npm install -g npm@latest
```

---

# 18. package-lock.json

`package-lock.json` records the exact dependency tree installed by npm.

It helps provide:

- Reproducible installations
- Consistent dependency versions
- Exact transitive dependencies
- More predictable deployments

Typical project:

```text
my-project/
├── node_modules/
├── package.json
├── package-lock.json
└── index.js
```

### Important

Commit:

```text
package-lock.json
```

to version control for applications.

---

# 19. package.json vs package-lock.json

```text
package.json
     ↓
Defines dependency requirements
     ↓
package-lock.json
     ↓
Records the exact resolved dependency tree
```

### Simple distinction

```text
package.json       → What the project needs
package-lock.json  → Exactly what was installed
```

---

# 20. Dependency Management

Dependency management includes:

- Installing packages
- Removing packages
- Updating packages
- Choosing versions
- Managing dependency types
- Auditing vulnerabilities
- Maintaining lock files

Useful commands:

```bash
npm install
npm update
npm uninstall package-name
npm outdated
npm ls
```

---

# 21. Security Auditing

Check dependencies for known vulnerabilities:

```bash
npm audit
```

Attempt automatic fixes:

```bash
npm audit fix
```

Force potentially breaking fixes:

```bash
npm audit fix --force
```

Use `--force` carefully because it can introduce major dependency changes.

---

# 22. NPM Cache and Troubleshooting

Clear npm cache when necessary:

```bash
npm cache clean --force
```

A common clean reinstall process:

```bash
rm -rf node_modules
rm package-lock.json
npm install
```

On Windows, the equivalent commands can differ depending on whether you're using Command Prompt, PowerShell, or Git Bash.

Check installed dependencies:

```bash
npm ls
```

Rebuild packages:

```bash
npm rebuild
```

---

# 23. npm Scripts

npm scripts automate common project tasks.

They are defined inside:

```json
"scripts": {
  "start": "node index.js",
  "test": "jest",
  "dev": "nodemon index.js"
}
```

Run a custom script:

```bash
npm run dev
```

Run the `start` script:

```bash
npm start
```

Run the `test` script:

```bash
npm test
```

---

# 24. Common npm Script Uses

npm scripts can automate:

- Starting applications
- Testing
- Building
- Linting
- Formatting
- Development servers
- Cleanup tasks
- Deployment workflows

Example:

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest",
    "lint": "eslint .",
    "build": "webpack --mode production"
  }
}
```

---

# 25. Publishing an npm Package

Publishing makes a Node.js package available through the npm registry.

Basic workflow:

```text
Create package
      ↓
npm init
      ↓
Create code
      ↓
Write README
      ↓
Test package
      ↓
npm login
      ↓
npm publish
```

---

# 26. Preparing a Package

Create a project:

```bash
mkdir my-package
cd my-package
npm init -y
```

Typical files:

```text
my-package/
├── index.js
├── package.json
├── README.md
├── LICENSE
└── .gitignore
```

Optional:

```text
.npmignore
```

can control files excluded from the published package.

---

# 27. npm Login

Log in through the CLI:

```bash
npm login
```

Check the currently logged-in account:

```bash
npm whoami
```

---

# 28. Publishing

Publish a package:

```bash
npm publish
```

Publish using a tag:

```bash
npm publish --tag beta
```

Before publishing, make sure:

- Package name is appropriate/available
- `package.json` is correct
- Documentation is included
- Tests pass
- Unnecessary files are excluded
- Version number is correct

---

# 29. Package Versions

Update the package version using SemVer:

### Patch

```bash
npm version patch
```

### Minor

```bash
npm version minor
```

### Major

```bash
npm version major
```

Then publish:

```bash
npm publish
```

---

# 30. Publishing Package Updates

Typical workflow:

```text
Make changes
     ↓
Test
     ↓
Update version
     ↓
npm version patch/minor/major
     ↓
npm publish
```

Use:

```text
PATCH → bug fixes
MINOR → new backward-compatible features
MAJOR → breaking changes
```

---

# 31. Deprecating Packages

Instead of removing a package completely, a version can be deprecated.

```bash
npm deprecate package-name@1.0.0 "Please upgrade to a newer version."
```

Deprecation warns users that a package/version should no longer be used.

---

# 32. CommonJS Imports and Exports

CommonJS uses:

```javascript
require()
```

Import:

```javascript
const math = require('./math');
```

Export:

```javascript
module.exports = {
  add,
  subtract
};
```

Example:

```javascript
// math.js

function add(a, b) {
  return a + b;
}

module.exports = {
  add
};
```

Then:

```javascript
// index.js

const { add } = require('./math');

console.log(add(2, 3));
```

---

# 33. ES Module Imports and Exports

ES Modules use:

```javascript
import
export
```

Named export:

```javascript
export function add(a, b) {
  return a + b;
}
```

Import:

```javascript
import { add } from './math.js';
```

Default export:

```javascript
export default function add(a, b) {
  return a + b;
}
```

Import:

```javascript
import add from './math.js';
```

---

# 34. CommonJS vs ES Modules

| CommonJS | ES Modules |
|---|---|
| `require()` | `import` |
| `module.exports` | `export` |
| `require('./file')` | `import ... from './file.js'` |
| Traditional Node.js module system | Modern JavaScript module system |

The project configuration determines how Node.js interprets modules.

---

# 35. Useful npm Commands

```bash
# Check npm version
npm --version

# Create package.json
npm init

# Create package.json with defaults
npm init -y

# Install package
npm install package-name

# Install specific version
npm install package-name@1.2.3

# Install development dependency
npm install package-name --save-dev

# Install globally
npm install -g package-name

# Remove package
npm uninstall package-name

# Update package
npm update package-name

# Update all packages
npm update

# Check outdated packages
npm outdated

# List dependencies
npm ls

# Audit dependencies
npm audit

# Fix vulnerabilities
npm audit fix

# Run script
npm run script-name

# Login
npm login

# Check account
npm whoami

# Publish package
npm publish
```

---

# Key Takeaways

```text
Node.js Project
       ↓
 package.json
       ↓
Dependencies + Scripts + Metadata
       ↓
 npm install
       ↓
 node_modules
       ↓
package-lock.json
       ↓
Reproducible dependency tree
```

The most important concepts:

- npm is Node.js's package manager.
- Packages provide reusable functionality.
- `package.json` describes the project.
- `dependencies` contain packages required by the application.
- `devDependencies` contain development-only packages.
- Semantic Versioning uses `MAJOR.MINOR.PATCH`.
- `^` allows compatible updates within the major version.
- `~` allows compatible patch updates.
- `package-lock.json` records the resolved dependency tree.
- npm scripts automate project tasks.
- `npm audit` checks for known vulnerabilities.
- npm can publish reusable packages to the registry.
- CommonJS uses `require()` and `module.exports`.
- ES Modules use `import` and `export`.
- Good dependency management improves stability and maintainability.

---

# Practical Skills

By completing this milestone, I should be able to:

- Explain what npm is
- Install Node.js packages
- Install specific package versions
- Install global packages
- Remove packages
- Update dependencies
- Understand `package.json`
- Create `package.json`
- Configure npm scripts
- Understand dependencies and devDependencies
- Understand peer and optional dependencies
- Understand Semantic Versioning
- Manage version ranges
- Understand `package-lock.json`
- Use npm audit
- Troubleshoot dependency issues
- Run npm scripts
- Understand CommonJS modules
- Understand ES Modules
- Create reusable packages
- Publish packages to npm
- Version published packages

---

# Learning Checklist

- [x] Introduction to npm
- [x] What Is npm?
- [x] What Is a `package.json` File?
- [x] Package Dependencies
- [x] Choosing External Packages
- [x] Semantic Versioning
- [x] Installing Dependencies
- [x] Removing Dependencies
- [x] Installing Specific Versions
- [x] Managing Dependencies
- [x] `package-lock.json`
- [x] npm Scripts
- [x] Publishing Packages
- [x] CommonJS Imports and Exports
- [x] ES Module Imports and Exports
- [x] NPM Review
- [x] NPM Quiz

---

# Certification Progress

**Course:** freeCodeCamp Back-End Development and APIs

**Section:** Node Package Manager

**Status:** Completed

---

## Core Principle

> **npm manages the packages, dependencies, scripts, and versions that make Node.js projects easier to build, maintain, share, and reproduce.**