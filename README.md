# json-api-builder-create-app

[![npm version](https://img.shields.io/npm/v/json-api-builder-create-app?color=cb3837&style=flat-square)](https://www.npmjs.com/package/json-api-builder-create-app)
[![license: MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](LICENSE)
[![Node.js](https://img.shields.io/badge/node-%3E%3D20-brightgreen.svg?style=flat-square)](package.json)
[![GitHub Repository](https://img.shields.io/badge/GitHub-keshavsoft%2Fjson-api-builder-create-app-181717.svg?style=flat-square&logo=github)](https://github.com/keshavsoft/json-api-builder-create-app)
[![Documentation](https://img.shields.io/badge/docs-live_portal-amber.svg?style=flat-square)](https://keshavsoft.github.io/json-api-builder-create-app/)

> **Stage 5 of 8**: Stage 5: Root Application Bootstrap, Strategy Middleware & Server Lifecycle

Part of the modular **[JSON API Builder](https://github.com/keshavsoft/json-api-builder-orchestrator)** ecosystem by [KeshavSoft](https://github.com/keshavsoft).

---

## The Story

Creates the root app.js application entry point, mounts top-level API routes and middleware strategies, and provides @hono/node-server startup capabilities.

### The Problem It Solves
Developers frequently struggle with boilerplate integration: connecting routers, mounting file sync endpoints, setting up CORS, and configuring the Node HTTP server.

### The Solution
Assembles the root app.js, mounts all top-level routes (/api, /fs), injects application middleware strategies, and provides an optional startServer helper to boot the app instantly.

---

## Architecture & Pipeline Position

```
[1. Folders] ──▶ [2. Files] ──▶ [3. Content] ──▶ [4. Hook Routes]
                                                         │
[8. Orchestrator] ◀── [7. Validate] ◀── [6. Endpoints] ◀── [5. App]
```

**This repository implements Stage 5 in isolation.** It can be used independently in custom build workflows or composed automatically via `json-api-builder`.

---

## Installation

```bash
npm install json-api-builder-create-app
```

---

## Quick Start

```js
import { createApp, hookAppStrategies } from "json-api-builder-create-app";

createApp({ outputRoot: "./output" });
hookAppStrategies({ outputRoot: "./output" });
```

---

## Input Specification

Application runtime and middleware configuration parameters.

```json
{
  "port": 3000,
  "strategies": ["cors", "logger", "file-sync"]
}
```

---

## Output Transformation

Production-ready root application entrypoint app.js.

```text
import { Hono } from "hono";
import apiRoutes from "./api/routes.js";
import fsRoutes from "./endpoints/fs/routes.js";

const app = new Hono();

app.route("/api", apiRoutes);
app.route("/fs", fsRoutes);

export default app;
```

---

## API Reference

### `createApp`, `hookAppStrategies`, `startServer`

Accepts an options object with the following configuration:

| Option | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `clientRoot` | `string` | `process.cwd()` | Root path of the client project. |
| `outputRoot` | `string` | `path.join(clientRoot, 'output')` | Target output directory. |
| `port` | `number` | `3000` | Port for @hono/node-server when startServer() is called. |

---

## Sibling Pipeline Packages

| Stage | Package | Description |
| :---: | :--- | :--- |
| **01** | [json-api-builder-create-folders](https://github.com/keshavsoft/json-api-builder-create-folders) | Directory hierarchy scaffolding |
| **02** | [json-api-builder-create-files](https://github.com/keshavsoft/json-api-builder-create-files) | Non-destructive placeholder file creation |
| **03** | [json-api-builder-insert-content](https://github.com/keshavsoft/json-api-builder-insert-content) | ESTree template to JavaScript insertion |
| **04** | [json-api-builder-alter-content](https://github.com/keshavsoft/json-api-builder-alter-content) | Hierarchical route hooking & AST imports |
| **05** | [json-api-builder-create-app](https://github.com/keshavsoft/json-api-builder-create-app) | Root app.js assembly & server runtime |
| **06** | [json-api-builder-create-endpoints](https://github.com/keshavsoft/json-api-builder-create-endpoints) | CRUD endpoints & local JSON file sync |
| **07** | [json-api-builder-validation](https://github.com/keshavsoft/json-api-builder-validation) | Specification linting & artifact checks |
| **08** | [json-api-builder](https://github.com/keshavsoft/json-api-builder-orchestrator) | Master orchestrator coordinating all stages |

---

## Development & Testing

```bash
# Install dependencies
npm install

# Run automated tests
npm test

# Run syntax check
npm run check

# Prepublish verification
npm run prepublishOnly
```

---

## License

[MIT](LICENSE) © 2026 [KeshavSoft](https://github.com/keshavsoft)
