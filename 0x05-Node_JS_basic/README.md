# 0x05-Node\_JS\_basic

A collection of small Node.js programs that progressively introduce core Node and Express concepts: standard I/O, synchronous vs asynchronous filesystem access, building HTTP servers with Node's `http` module, and finally structuring a tiny REST API with **Express**.
The repository follows the style & build constraints of the ALX **NodeJS Basics** curriculum.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Structure](#project-structure)
3. [Quick Start](#quick-start)
4. [Scripts overview](#scripts-overview)
5. [Full‑server endpoints](#full-server-endpoints)
6. [Coding style & linting](#coding-style--linting)
7. [Author](#author)

---

## Prerequisites

* **Node.js ≥ 18 LTS** (works with Node 14 + but 18 LTS is recommended)
* **npm** (bundled with Node) or **pnpm/yarn**
* A Unix‑like shell (Ubuntu 20.04 + or macOS recommended)

```bash
node -v     # v18.19.0 or later
npm -v      # 10.x or later
```


---

## Project Structure

```
0x05-Node_JS_basic/
├── 0-console.js              # Basic console logging
├── 1-stdin.js               # Read from STDIN synchronously
├── 2-read_file.js           # Synchronous file read
├── 3-read_file_async.js     # Async file read with Promises
├── 4-http.js                # Bare‑bones HTTP server
├── 5-http.js                # HTTP server reading a local DB (sync)
├── 6-http_express.js        # Express re‑implementation of 4‑http.js
├── 7-http_express.js        # Express with async file handling
└── full_server/
    ├── utils.js                     # CSV helper utilities
    ├── controllers/
    │   ├── AppController.js         # index & status
    │   └── StudentsController.js    # /students endpoints
    ├── routes/
    │   └── index.js                 # Express router
    └── server.js                    # Bootstrap the API server
```

---

## Quick Start

1. **Clone** the repo and install dependencies (only `express` is required).

   ```bash
   git clone <repo-url> && cd 0x05-Node_JS_basic
   npm ci          # or npm install
   ```

2. **Run individual mini‑programs**:

   ```bash
   node 0-console.js           # prints "Holberton School"
   echo "ALX" | node 1-stdin.js
   node 2-read_file.js database.csv
   node 3-read_file_async.js database.csv
   ```

3. **Fire up the HTTP servers**:

   * **Vanilla Node**

     ```bash
     node 4-http.js            # default: http://localhost:1245/
     node 5-http.js database.csv
     ```
   * **Express**

     ```bash
     node 6-http_express.js
     node 7-http_express.js database.csv
     ```
   * **Full‑blown API**

     ```bash
     cd full_server && node server.js --db=../database.csv
     # Server listens on PORT 1245 by default
     ```

4. **Hit the endpoints**:

   ```bash
   curl http://localhost:1245/                 # → Hello Holberton School!
   curl http://localhost:1245/students          # → CSV stats
   curl http://localhost:1245/students/SWE      # → Only SWE students
   ```

---

## Scripts overview

| File                                               | What it Demonstrates                                                     |
| -------------------------------------------------- | ------------------------------------------------------------------------ |
| **0-console.js**                                   | Usage of `console.log` and formatted printing                            |
| **1-stdin.js**                                     | Reading from standard input synchronously with `process.stdin`           |
| **2-read\_file.js**                                | Synchronous filesystem access with `fs.readFileSync`                     |
| **3-read\_file\_async.js**                         | Non‑blocking I/O using `fs.promises.readFile` + `async/await`            |
| **4-http.js**                                      | Manually crafting an HTTP server with Node’s built‑in `http` module      |
| **5-http.js**                                      | Building on 4‑http.js: reading a CSV database on each request (blocking) |
| **6-http\_express.js**                             | Re‑writing 4‑http.js using Express for routing/middleware                |
| **7-http\_express.js**                             | Express + async CSV parsing for better scalability                       |
| **full\_server/utils.js**                          | Promise‑based CSV parser that groups students by field                   |
| **full\_server/controllers/AppController.js**      | Handles `/` and `/status` routes                                         |
| **full\_server/controllers/StudentsController.js** | Handles `/students` + `/students/:major` routes                          |
| **full\_server/routes/index.js**                   | Wires controllers to an Express router                                   |
| **full\_server/server.js**                         | Entrypoint: creates Express app, binds port, injects CSV path            |

---

## Full‑server endpoints

Running `full_server/server.js` gives a tiny JSON API:

| Method | Route              | Description                                                   |
| ------ | ------------------ | ------------------------------------------------------------- |
| `GET`  | `/`                | Returns a short greeting string                               |
| `GET`  | `/status`          | Simple health‑check `{ "status": "OK" }`                      |
| `GET`  | `/students`        | Aggregated list & count of students per field                 |
| `GET`  | `/students/:major` | Students filtered by the specified `major` (case‑insensitive) |

* The path to the CSV database can be passed as `--db=path` or `DB_PATH` env var.
* **Major** must be one of: `CS`, `SWE`. The controller validates & 400s otherwise.

---

## Coding style & linting

This repo follows the ALX/Betty‑inspired constraints:

* **No linter warnings**: run `npm run lint` (ESLint + Prettier) before committing.
* **Functions ≤ 40 lines & 80 cols** where practical.
* Descriptive, JSDoc‑style comments on exported functions.
* No generated `*.o`/temp files committed.

```
# Automatic prettier pass
npm run format
```

---

## Author

**Thokozane Tshabalala**
Email: thokozanetek@gmail.com
cellphone: 0793859541
Pretoria, South Africa

> Pull requests are welcome – open an issue first to discuss what you’d like to change.

---

### License

This project is licensed under the **MIT License** – see `LICENSE` for details.

