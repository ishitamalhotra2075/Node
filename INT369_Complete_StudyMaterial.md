# 🎓 INT369: Advanced Web Programming
## Complete Lecture-wise Study Material (Units I–VI)
### B.Tech 3rd Year | L:3 T:0 P:2 | Credits: 4 | Session 2025-26

---

## 🗺️ Course at a Glance

```mermaid
flowchart LR
    U1["📘 Unit I
    Node.js Core
    and Data I/O"] --> U2["🌐 Unit II
    HTTP and Express"]
    U2 --> U3["🔌 Unit III
    Sockets and
    Middleware"]
    U3 --> U4["🍃 Unit IV
    MongoDB and
    Mongoose"]
    U4 --> U5["🐘 Unit V
    PostgreSQL"]
    U5 --> U6["🚀 Unit VI
    Test and Deploy"]
```

## 📑 Lecture Plan

| Unit | Title | Lectures | Global Lecture Nos. |
|---|---|---|---|
| I | Getting Started with Node.js and Handling Data I/O | 5 | 1 – 5 |
| II | Implementing HTTP Services and Basic Websites (Express) | 5 | 6 – 10 |
| III | Socket Services and Creating Middlewares | 5 | 11 – 15 |
| IV | MongoDB and Mongoose | 6 | 16 – 21 |
| V | Introduction to PostgreSQL | 4 | 22 – 25 |
| VI | Testing and Deployment | 4 | 26 – 29 |
| | **Total** | **29 × 50 min** | |

> The syllabus is planned for 45 lectures; the remaining 16 slots are left free for revision, class tests, doubt sessions and practical walkthroughs.

### 🧭 Lecture-by-Lecture Index

| # | Unit | Lecture Topic |
|---|---|---|
| 1 | I | Introducing Node.js, Installation, REPL, NPM, `npm init` |
| 2 | I | NPM Modules, EventEmitter, Callbacks |
| 3 | I | `fs` module and JSON |
| 4 | I | Streams and Zlib |
| 5 | I | Promises and async/await |
| 6 | II | HTTP module and basic server |
| 7 | II | Request/Response objects, basic routing |
| 8 | II | Response headers, status codes, intro to Express |
| 9 | II | GET and POST, body-parser |
| 10 | II | `express.Router`, express-validator |
| 11 | III | Network sockets, basic WebSocket server |
| 12 | III | Sending/receiving messages, broadcasting |
| 13 | III | Socket.IO chat server |
| 14 | III | Middleware, `app.use()`, `app.all()` |
| 15 | III | cookie-parser, cookie-session, express-session |
| 16 | IV | MongoDB intro, installation, terminology |
| 17 | IV | Documents, collections, shell create/drop |
| 18 | IV | Shell CRUD: insert, find, update, delete |
| 19 | IV | Node.js driver and CRUD |
| 20 | IV | Mongoose: schema and models |
| 21 | IV | Mongoose CRUD and mini REST API |
| 22 | V | PostgreSQL intro, installation, `psql` |
| 23 | V | CREATE TABLE, data types, INSERT |
| 24 | V | SELECT, UPDATE, DELETE |
| 25 | V | Aggregates, joins, `pg` with Node.js |
| 26 | VI | Testing REST APIs manually |
| 27 | VI | Automated tests: Jest and Supertest |
| 28 | VI | Deployment with GitHub and CI |
| 29 | VI | Third-party hosting and services |

## 🧪 Practical Mapping (from the syllabus)

| Practical | Covered In (Lecture) |
|---|---|
| Install Node.js and manage packages using NPM | 1 |
| Script using EventEmitter and callbacks | 2 |
| File operations using the `fs` module | 3 |
| Stream data and compress/decompress with Zlib | 4 |
| Basic HTTP server with routing and response handling | 6, 7 |
| Express routes for GET/POST with body-parser | 9 |
| Validate request data with express-validator | 10 |
| WebSocket server with Socket.IO for real-time messaging | 11, 12 |
| Simple chat application with Socket.IO | 13 |
| Custom middleware and session management in Express | 14, 15 |
| CRUD on MongoDB using Node.js | 19 |
| Schemas and CRUD using Mongoose | 20, 21 |
| Install PostgreSQL and run SQL CRUD commands | 22 – 24 |
| Test REST APIs and deploy using GitHub and third-party tools | 26 – 29 |

---

# 📚 Unit I — Getting Started with Node.js & Data I/O
### Lectures 1 – 5 (5 × 50 minutes)

---

> **Unit Roadmap**

```mermaid
flowchart LR
    L1["📘 Lecture 1
    Node.js Basics,
    Install, REPL, NPM"] --> L2["📦 Lecture 2
    NPM Modules,
    EventEmitter, Callbacks"]
    L2 --> L3["📁 Lecture 3
    fs module & JSON"]
    L3 --> L4["🌊 Lecture 4
    Streams & Zlib"]
    L4 --> L5["⏳ Lecture 5
    Promises &
    async/await"]
```

---

# 📘 LECTURE 1 (Unit I · L1): Introducing Node.js, Installation, REPL, NPM & `npm init`

## 🎯 What You Will Know By the End
- What Node.js is and why it exists
- How to install it and verify the install
- How to use the REPL as a scratchpad
- How to initialize a Node.js project with `npm init`

## 1.1 What is Node.js? 🤔

Node.js is a **JavaScript runtime** built on Chrome's **V8 engine** that lets you run JavaScript *outside the browser* — on servers, on your laptop, anywhere.

```mermaid
flowchart TD
    A["Browser JS
    (limited to browser sandbox)"] -->|"V8 Engine
    extracted"| B["Node.js
    (JS Runtime + libuv)"]
    B --> C["File System Access"]
    B --> D["Network / HTTP Servers"]
    B --> E["OS-level Operations"]
```

**Key traits:**
| Trait | Meaning |
|---|---|
| ⚡ Single-threaded | One main thread runs your JS |
| 🔄 Event-driven | Reacts to events instead of blocking |
| 🚫 Non-blocking I/O | Doesn't wait around for slow tasks (disk, network) |
| 📦 NPM ecosystem | Largest package registry in the world |

### ⚙️ How it Works Under the Hood

```mermaid
sequenceDiagram
    participant App as Your Code
    participant EL as Event Loop
    participant LU as libuv (Thread Pool / OS)

    App->>EL: readFile("data.txt", callback)
    EL->>LU: Delegate I/O task
    Note over App,EL: Node moves on immediately,<br/>does NOT wait
    LU-->>EL: File read complete
    EL-->>App: Executes callback(data)
```

## 1.2 Installing Node.js 🛠️

**Steps:**
1. Go to [nodejs.org](https://nodejs.org)
2. Download the **LTS** (Long Term Support) version ✅ — avoid "Current" for classroom/production use
3. Run the installer (Windows/macOS) or use a package manager (Linux)
4. Verify installation:

```bash
node -v      # e.g., v20.14.0
npm -v       # e.g., v10.7.0
```

> 💡 **Tip for students:** `npm` (Node Package Manager) is installed **automatically** with Node.js — you never install it separately.

## 1.3 The REPL — Your JS Playground 🎮

**REPL** = **R**ead **E**valuate **P**rint **L**oop. Type `node` in your terminal to enter it.

```bash
$ node
> let x = 10
undefined
> x * 2
20
> console.log("Hello INT369")
Hello INT369
undefined
> .exit
```

| REPL Command | Purpose |
|---|---|
| `.help` | List all REPL commands |
| `.exit` | Quit the REPL |
| `.clear` | Reset the current context |
| `.save filename` | Save session to a file |
| `.load filename` | Load a file into session |

## 1.4 Initializing a Project with `npm init` 📦

Every real Node.js project starts with a **`package.json`** — the project's ID card.

```bash
mkdir my-first-node-app
cd my-first-node-app
npm init -y        # -y = accept all defaults, skip Q&A
```

**Generated `package.json`:**
```json
{
  "name": "my-first-node-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

```mermaid
flowchart LR
    A["npm init"] --> B{"-y flag?"}
    B -->|Yes| C["Auto-fill defaults
    → package.json"]
    B -->|No| D["Interactive prompts
    (name, version, entry...)"]
    D --> C
```

### 🧪 Minimal Working Example
Create `index.js`:
```javascript
console.log("🎉 My first Node.js app is running!");
```
Run it:
```bash
node index.js
```

---

## ✅ CHECKPOINT — Lecture 1 (Unit I · L1)
- [ ] Explain Node.js in one sentence to a classmate
- [ ] Install Node.js and run `node -v` successfully
- [ ] Open REPL, compute `5 + 5`, and `.exit`
- [ ] Run `npm init -y` and inspect the generated `package.json`

---

# 📦 LECTURE 2 (Unit I · L2): NPM Modules, EventEmitter & Callbacks

## 🎯 What You Will Know By the End
- Difference between Core, Local, and Third-Party modules
- How to install and use an npm package
- How Node's `EventEmitter` powers event-driven programming
- How callbacks work (and why they matter)

## 2.1 Types of Modules in Node.js 🧩

```mermaid
flowchart TD
    M["Node.js Modules"] --> Core["🔧 Core Modules
    Built into Node
    (fs, http, path, os)"]
    M --> Local["📄 Local Modules
    Files you write
    (./myModule.js)"]
    M --> Third["🌍 Third-Party Modules
    Installed via npm
    (express, lodash)"]
```

### a) Core Modules (no install needed)
```javascript
const os = require('os');
console.log(os.platform());  // e.g., 'win32', 'linux'
```

### b) Local Modules (your own files)
**`greet.js`**
```javascript
function greet(name) {
  return `Hello, ${name}! 👋`;
}
module.exports = greet;
```
**`index.js`**
```javascript
const greet = require('./greet');
console.log(greet("INT369 Class"));
```

### c) Third-Party Modules (via NPM registry)
```bash
npm install lodash
```
```javascript
const _ = require('lodash');
console.log(_.capitalize("node.js is fun"));  // "Node.js is fun"
```

> 📌 Third-party packages get listed automatically in `package.json` → `"dependencies"`, and code is stored inside `node_modules/`.

## 2.2 EventEmitter — The Heart of Node.js 🔔

Node is **event-driven**. The `EventEmitter` class lets objects emit named events that trigger listener functions.

```mermaid
sequenceDiagram
    participant Emitter as EventEmitter
    participant L1 as Listener("order")

    Note over Emitter: .on("order", fn) → register
    Emitter->>Emitter: .emit("order", data)
    Emitter->>L1: fn(data) is called
```

### 🧪 Minimal Example
```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

// Register a listener
emitter.on('greet', (name) => {
  console.log(`Hi ${name}, welcome! 🎊`);
});

// Trigger (emit) the event
emitter.emit('greet', 'Ravi');
```
**Output:**
```
Hi Ravi, welcome! 🎊
```

## 2.3 Callbacks — "Call me when you're done" ☎️

A **callback** is a function passed as an argument, executed *after* another function completes — the original way Node handled async work.

```mermaid
flowchart LR
    A["doTask(callback)"] --> B["Task runs..."]
    B --> C["Task finishes"]
    C --> D["callback(result) executes"]
```

### 🧪 Minimal Example
```javascript
function fetchScore(studentId, callback) {
  console.log("Fetching score...");
  setTimeout(() => {
    callback(null, 92);   // simulate async delay (1 sec)
  }, 1000);
}

fetchScore(101, (err, score) => {
  if (err) return console.error(err);
  console.log(`Score: ${score}`);
});
```

> ⚠️ **Callback Hell:** Nesting too many callbacks creates unreadable "pyramid" code. This is the *motivation* for Promises (Lecture 5)!

```javascript
// 😱 Callback Hell example (for illustration only)
step1(a, (r1) => {
  step2(r1, (r2) => {
    step3(r2, (r3) => {
      console.log(r3);
    });
  });
});
```

---

## ✅ CHECKPOINT — Lecture 2 (Unit I · L2)
- [ ] List one example each of core, local, and third-party modules
- [ ] Install a package with `npm install` and `require()` it
- [ ] Write an `EventEmitter` that emits a custom event
- [ ] Write a function that accepts and calls a callback

---

# 📁 LECTURE 3 (Unit I · L3): Working with `fs` Module and JSON

## 🎯 What You Will Know By the End
- Reading/writing files synchronously and asynchronously with `fs`
- Parsing and writing JSON data
- Understanding blocking vs non-blocking file operations

## 3.1 The `fs` (File System) Module 🗄️

```mermaid
flowchart TD
    fs["fs module"] --> Sync["Synchronous
    (readFileSync)
    ⛔ Blocks execution"]
    fs --> Async["Asynchronous
    (readFile)
    ✅ Non-blocking"]
```

### 🧪 Reading a File (Async — preferred)
**`data.txt`** → `Hello from a file!`
```javascript
const fs = require('fs');

fs.readFile('data.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log("File content:", data);
});
console.log("This runs FIRST (non-blocking)!");
```
**Output order:**
```
This runs FIRST (non-blocking)!
File content: Hello from a file!
```

### 🧪 Writing a File
```javascript
fs.writeFile('output.txt', 'Written by Node.js 🖋️', (err) => {
  if (err) throw err;
  console.log('File saved!');
});
```

### 🧪 Synchronous Version (for comparison)
```javascript
const content = fs.readFileSync('data.txt', 'utf8');
console.log(content); // blocks until done
```

| Method | Blocking? | Use When |
|---|---|---|
| `readFileSync` | ✅ Yes | Simple scripts, startup config |
| `readFile` | ❌ No | Servers, production apps |

## 3.2 Working with JSON 📋

JSON = **J**ava**S**cript **O**bject **N**otation — the universal data-exchange format.

```mermaid
flowchart LR
    Obj["JS Object"] -->|"JSON.stringify()"| Str["JSON String"]
    Str -->|"JSON.parse()"| Obj2["JS Object"]
```

### 🧪 Minimal Example
```javascript
const student = { name: "Aman", course: "INT369", cgpa: 8.7 };

// Object → JSON string (for saving to file)
const jsonString = JSON.stringify(student, null, 2);
fs.writeFileSync('student.json', jsonString);

// JSON string → Object (reading back)
const raw = fs.readFileSync('student.json', 'utf8');
const parsedStudent = JSON.parse(raw);
console.log(parsedStudent.name);  // "Aman"
```

**`student.json` produced:**
```json
{
  "name": "Aman",
  "course": "INT369",
  "cgpa": 8.7
}
```

---

## ✅ CHECKPOINT — Lecture 3 (Unit I · L3)
- [ ] Read a text file asynchronously and log its content
- [ ] Write a string to a new file using `fs.writeFile`
- [ ] Convert a JS object to a JSON string with `JSON.stringify`
- [ ] Read a `.json` file and parse it with `JSON.parse`

---

# 🌊 LECTURE 4 (Unit I · L4): Streams & Zlib (Compression/Decompression)

## 🎯 What You Will Know By the End
- Why streams exist and how they differ from `fs.readFile`
- The four stream types
- How to compress/decompress files with `zlib`

## 4.1 Why Streams? 🤷

Reading a **10 GB file** with `readFile` loads the *whole thing* into memory first. **Streams** process data in small **chunks**, piece by piece.

```mermaid
flowchart LR
    Src["📄 Source File"] -->|chunk 1| Buf["Buffer"]
    Buf --> Dest["📥 Destination"]
    Src -->|chunk 2| Buf
    Src -->|chunk 3| Buf
```

### Four Types of Streams
| Type | Direction | Example |
|---|---|---|
| **Readable** | Read data | `fs.createReadStream()` |
| **Writable** | Write data | `fs.createWriteStream()` |
| **Duplex** | Both | TCP sockets |
| **Transform** | Modify while passing through | `zlib.createGzip()` |

## 4.2 Streaming Data Between Files 🧪

```javascript
const fs = require('fs');

const readStream = fs.createReadStream('bigfile.txt', 'utf8');
const writeStream = fs.createWriteStream('copy.txt');

readStream.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
});

readStream.pipe(writeStream);   // 🚰 pipe = read → write automatically

writeStream.on('finish', () => {
  console.log('✅ Copy complete!');
});
```

```mermaid
sequenceDiagram
    participant R as ReadStream
    participant W as WriteStream

    R->>R: read chunk
    R->>W: pipe() sends chunk
    W->>W: write chunk to disk
    R->>R: read next chunk
    R->>W: pipe() sends chunk
    Note over R,W: repeats until EOF
    R-->>W: end event → finish event
```

## 4.3 Compression & Decompression with `zlib` 🗜️

`zlib` is Node's built-in module for **gzip** compression — great for reducing file size or compressing HTTP responses.

### 🧪 Compress a File
```javascript
const fs = require('fs');
const zlib = require('zlib');

const readStream = fs.createReadStream('data.txt');
const gzip = zlib.createGzip();
const writeStream = fs.createWriteStream('data.txt.gz');

readStream.pipe(gzip).pipe(writeStream);
writeStream.on('finish', () => console.log('📦 Compressed successfully!'));
```

### 🧪 Decompress a File
```javascript
const gunzip = zlib.createGunzip();

fs.createReadStream('data.txt.gz')
  .pipe(gunzip)
  .pipe(fs.createWriteStream('data_restored.txt'))
  .on('finish', () => console.log('📂 Decompressed successfully!'));
```

```mermaid
flowchart LR
    A["data.txt"] -->|"createGzip()"| B["data.txt.gz
    (smaller size)"]
    B -->|"createGunzip()"| C["data_restored.txt"]
```

---

## ✅ CHECKPOINT — Lecture 4 (Unit I · L4)
- [ ] Explain why streams are better than `readFile` for large files
- [ ] Name the 4 stream types with one real example each
- [ ] Use `.pipe()` to copy one file's content into another
- [ ] Compress a file to `.gz` and decompress it back using `zlib`

---

# ⏳ LECTURE 5 (Unit I · L5): Promises and Async/Await

## 🎯 What You Will Know By the End
- Why Promises replaced callback-heavy code
- The 3 states of a Promise
- How `async`/`await` makes async code read like sync code

## 5.1 From Callback Hell to Promises 🕳️➡️🌟

```mermaid
flowchart TD
    CB["Callbacks
    (nested, hard to read)"] --> P["Promises
    (.then/.catch chains)"]
    P --> AA["async/await
    (cleanest, sync-looking)"]
```

## 5.2 Promise States 🚦

```mermaid
stateDiagram-v2
    [*] --> Pending
    Pending --> Fulfilled: resolve(value)
    Pending --> Rejected: reject(error)
    Fulfilled --> [*]
    Rejected --> [*]
```

### 🧪 Creating and Using a Promise
```javascript
function fetchScore(studentId) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (studentId > 0) {
        resolve(92);           // ✅ success
      } else {
        reject("Invalid ID");  // ❌ failure
      }
    }, 1000);
  });
}

fetchScore(101)
  .then((score) => console.log(`Score: ${score}`))
  .catch((err) => console.error(err));
```

## 5.3 `async` / `await` — Syntactic Sugar 🍬

`async/await` lets you write Promise-based code that *looks* synchronous.

```mermaid
sequenceDiagram
    participant Code as async function
    participant P as Promise

    Code->>P: await fetchScore(101)
    Note over Code: Execution PAUSES here<br/>(non-blocking to rest of app)
    P-->>Code: resolves with 92
    Note over Code: Execution RESUMES
```

### 🧪 Minimal Example
```javascript
async function getStudentScore() {
  try {
    const score = await fetchScore(101);
    console.log(`Score: ${score}`);
  } catch (err) {
    console.error("Error:", err);
  }
}

getStudentScore();
```

### 🔁 Comparison: Same Task, 3 Styles

| Style | Code |
|---|---|
| Callback | `fetchScore(101, (err, s) => {...})` |
| Promise | `fetchScore(101).then(s => {...}).catch(e => {...})` |
| async/await | `const s = await fetchScore(101);` (inside `try/catch`) |

### 🧪 Bonus: Running Tasks in Parallel
```javascript
async function getAllScores() {
  const [scoreA, scoreB] = await Promise.all([
    fetchScore(101),
    fetchScore(102)
  ]);
  console.log(scoreA, scoreB);
}
```

---

## ✅ CHECKPOINT — Lecture 5 (Unit I · L5)
- [ ] Draw/explain the 3 Promise states
- [ ] Write a function returning a Promise that resolves or rejects
- [ ] Convert a `.then()/.catch()` chain into `async/await` with `try/catch`
- [ ] Use `Promise.all()` to run two async tasks in parallel

---

# 🏁 Unit I Summary Map

```mermaid
mindmap
  root((Unit I: Node.js Basics))
    Introduction
      Install
      REPL
      npm init
    Modules
      Core
      Local
      Third-Party
    Events
      EventEmitter
      Callbacks
    File I/O
      fs module
      JSON
    Streams
      Readable/Writable
      pipe()
      Zlib gzip/gunzip
    Async Patterns
      Callbacks
      Promises
      async/await
```


---

# 📚 Unit II — Implementing HTTP Services & Basic Websites with Node.js
### Lectures 6 – 10 (5 × 50 minutes)

---

> **Unit Roadmap**

```mermaid
flowchart LR
    L1["📡 Lecture 1
    HTTP Module,
    Basic Server"] --> L2["📨 Lecture 2
    Request/Response,
    Basic Routing"]
    L2 --> L3["🚦 Lecture 3
    Headers, Status Codes
    + Intro to Express"]
    L3 --> L4["🛣️ Lecture 4
    GET/POST,
    body-parser"]
    L4 --> L5["🧩 Lecture 5
    express.Router,
    express-validator"]
```

---

# 📡 LECTURE 6 (Unit II · L1): Introduction to HTTP Module & Setting Up a Basic Server

## 🎯 What You Will Know By the End
- What the HTTP protocol is doing when a browser talks to a server
- What Node's built-in `http` module gives you
- How to spin up your first raw HTTP server

## 1.1 A Quick Refresher: What Happens When You Visit a Website? 🤔

```mermaid
sequenceDiagram
    participant B as Browser (Client)
    participant S as Node.js Server

    B->>S: HTTP Request (GET /home)
    S->>S: Process the request
    S-->>B: HTTP Response (HTML/JSON + status code)
    Note over B,S: This request-response cycle<br/>is the backbone of the web
```

**Key HTTP vocabulary:**
| Term | Meaning |
|---|---|
| 🧾 Request | What the client sends (method, URL, headers, body) |
| 📬 Response | What the server sends back (status, headers, body) |
| 🔤 Method | `GET`, `POST`, `PUT`, `DELETE`... — the "verb" of the request |
| 🎯 Status Code | 3-digit number telling the outcome (200, 404, 500...) |

## 1.2 The `http` Core Module 📦

Node ships with a built-in `http` module — **no installation needed**. It lets you create a web server with pure JavaScript.

```javascript
const http = require('http');
```

```mermaid
flowchart TD
    A["require('http')"] --> B["http.createServer(callback)"]
    B --> C["server.listen(port)"]
    C --> D["🎧 Server waits for requests"]
```

## 1.3 Setting Up a Basic HTTP Server 🛠️

### 🧪 Minimal Working Example
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Hello from my first Node.js server! 👋');
});

server.listen(3000, () => {
  console.log('🚀 Server running at http://localhost:3000');
});
```

**Run it:**
```bash
node server.js
```
Open `http://localhost:3000` in your browser — you'll see the greeting text.

### 🔍 Breaking It Down
| Piece | Role |
|---|---|
| `http.createServer(cb)` | Creates a server; `cb` runs on **every** incoming request |
| `req` | Incoming request object |
| `res` | Outgoing response object |
| `res.end()` | Finishes the response and sends it |
| `server.listen(port)` | Starts listening on the given port |

> 💡 **Classroom Tip:** Ask students to change the port number and message, then restart the server (`Ctrl+C` then `node server.js`) to see the change — this builds the "edit → restart → test" muscle memory early.

---

## ✅ CHECKPOINT — Lecture 6 (Unit II · L1)
- [ ] Explain the request-response cycle in your own words
- [ ] Import the `http` core module without installing anything
- [ ] Create a server using `http.createServer()`
- [ ] Start the server with `.listen()` and view it in a browser

---

# 📨 LECTURE 7 (Unit II · L2): Request & Response Objects, Basic Routing

## 🎯 What You Will Know By the End
- What information lives inside `req` and `res`
- How to inspect URL, method, and headers of a request
- How to implement simple routing manually with `if/else`

## 2.1 The Request Object (`req`) 📥

```mermaid
flowchart LR
    req["req object"] --> url["req.url
    e.g. '/about'"]
    req --> method["req.method
    e.g. 'GET'"]
    req --> headers["req.headers
    e.g. user-agent, host"]
```

### 🧪 Minimal Example
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  console.log('URL:', req.url);
  console.log('Method:', req.method);
  console.log('Headers:', req.headers);
  res.end('Check your terminal! 🖥️');
});

server.listen(3000);
```

## 2.2 The Response Object (`res`) 📤

| Method | Purpose |
|---|---|
| `res.write(data)` | Send a chunk of data (can call multiple times) |
| `res.end(data)` | Send final data and close the response |
| `res.setHeader(name, value)` | Set a response header |
| `res.statusCode = n` | Set the HTTP status code |

### 🧪 Minimal Example
```javascript
const server = http.createServer((req, res) => {
  res.write('Line 1... ');
  res.write('Line 2... ');
  res.end('Done! ✅');
});
```

## 2.3 Implementing Basic Routing 🛣️

**Routing** = deciding *what to send back* based on the requested URL and method.

```mermaid
flowchart TD
    Req["Incoming Request"] --> Check{"req.url === ?"}
    Check -->|"/"| Home["Send Home Page"]
    Check -->|"/about"| About["Send About Page"]
    Check -->|"anything else"| NotFound["Send 404 Not Found"]
```

### 🧪 Minimal Working Example
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.end('🏠 Welcome to the Home Page');
  } else if (req.url === '/about' && req.method === 'GET') {
    res.end('ℹ️ About Us Page');
  } else {
    res.statusCode = 404;
    res.end('🚫 404 - Page Not Found');
  }
});

server.listen(3000, () => console.log('Server on port 3000'));
```

> ⚠️ **Real talk for students:** Manual `if/else` routing gets messy fast for real apps — this is exactly the pain that **Express** (Lecture 3 onward) solves.

---

## ✅ CHECKPOINT — Lecture 7 (Unit II · L2)
- [ ] Print `req.url`, `req.method`, and `req.headers` to the console
- [ ] Use `res.write()` and `res.end()` together
- [ ] Build a raw router with `if/else` for at least 2 routes
- [ ] Return a 404 response for an unmatched route

---

# 🚦 LECTURE 8 (Unit II · L3): Response Headers, Status Codes & Introduction to Express

## 🎯 What You Will Know By the End
- How to set response headers (like `Content-Type`)
- The meaning of common HTTP status code ranges
- Why Express exists and how to install it

## 3.1 Setting Response Headers 📋

Headers tell the client **how to interpret** the response body.

```javascript
res.setHeader('Content-Type', 'text/html');
res.setHeader('X-Powered-By', 'INT369-Class');
```

### 🧪 Minimal Example — Sending JSON Correctly
```javascript
const server = http.createServer((req, res) => {
  res.setHeader('Content-Type', 'application/json');
  res.end(JSON.stringify({ message: 'Hello JSON! 📦' }));
});
```

## 3.2 HTTP Status Codes 🚥

```mermaid
flowchart LR
    S1["1xx
    ℹ️ Informational"] 
    S2["2xx
    ✅ Success"]
    S3["3xx
    🔀 Redirection"]
    S4["4xx
    ❌ Client Error"]
    S5["5xx
    💥 Server Error"]
```

| Code | Meaning | Common Use |
|---|---|---|
| `200` | OK | Successful GET request |
| `201` | Created | Successful POST that made a new resource |
| `301` | Moved Permanently | Redirects |
| `400` | Bad Request | Malformed client input |
| `404` | Not Found | Route/resource doesn't exist |
| `500` | Internal Server Error | Something broke server-side |

### 🧪 Minimal Example
```javascript
const server = http.createServer((req, res) => {
  if (req.url === '/secret') {
    res.statusCode = 403;
    res.end('⛔ Forbidden');
  } else {
    res.statusCode = 200;
    res.end('✅ OK');
  }
});
```

## 3.3 Why Express? Introducing the Framework 🚀

Writing raw `http` servers for real apps means **manually** handling routing, headers, parsing bodies, static files... Express wraps all this in a clean API.

```mermaid
flowchart TD
    Raw["Raw http module
    😓 Manual everything"] --> Ex["Express.js
    😌 Batteries included"]
    Ex --> R["Simple routing:
    app.get(), app.post()"]
    Ex --> MW["Middleware support"]
    Ex --> ST["Static file serving"]
```

## 3.4 Installing Express 📦

```bash
npm init -y
npm install express
```

### 🧪 Minimal Working Example
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('🎉 Hello from Express!');
});

app.listen(3000, () => console.log('Express server on port 3000'));
```

> 💡 **Compare:** This does the *same job* as the entire raw-`http` router from Lecture 2, in far fewer lines.

---

## ✅ CHECKPOINT — Lecture 8 (Unit II · L3)
- [ ] Set a custom response header and verify it in browser DevTools
- [ ] Match at least 3 status code ranges to their meaning
- [ ] Install Express via `npm install express`
- [ ] Create a "Hello World" Express server with `app.get()`

---

# 🛣️ LECTURE 9 (Unit II · L4): GET & POST Requests, body-parser

## 🎯 What You Will Know By the End
- How to define GET and POST routes in Express
- How to read form/JSON data sent by the client
- How to use `express.json()` / `body-parser` middleware

## 4.1 GET Requests in Express 📥

GET is used to **retrieve** data — parameters usually travel in the URL.

### 🧪 Minimal Example — Route Params & Query Strings
```javascript
const express = require('express');
const app = express();

// Route parameter: /student/23
app.get('/student/:id', (req, res) => {
  res.send(`📄 Student ID: ${req.params.id}`);
});

// Query string: /search?course=INT369
app.get('/search', (req, res) => {
  res.send(`🔍 Searching for: ${req.query.course}`);
});

app.listen(3000);
```

## 4.2 POST Requests & Reading the Body 📤

POST sends data in the **request body** — usually JSON or form data.

```mermaid
sequenceDiagram
    participant C as Client
    participant MW as body-parser Middleware
    participant R as Route Handler

    C->>MW: POST /register {name: "Riya"}
    MW->>MW: Parses raw body into req.body
    MW->>R: req.body = { name: "Riya" }
    R-->>C: 201 Created
```

## 4.3 `body-parser` (and Express's Built-in Equivalent) 🧩

Historically you needed the separate `body-parser` package. Modern Express includes the same functionality built in as `express.json()` / `express.urlencoded()`.

```bash
npm install body-parser
```

### 🧪 Minimal Working Example
```javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

app.use(bodyParser.json());                       // parse JSON bodies
app.use(bodyParser.urlencoded({ extended: true })); // parse form bodies

app.post('/register', (req, res) => {
  const { name, email } = req.body;
  res.status(201).send(`✅ Registered: ${name} (${email})`);
});

app.listen(3000, () => console.log('Server running...'));
```

> 📌 **Modern equivalent** (no extra package needed):
> ```javascript
> app.use(express.json());
> app.use(express.urlencoded({ extended: true }));
> ```

### 🧪 Testing with `curl`
```bash
curl -X POST http://localhost:3000/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Riya","email":"riya@lpu.in"}'
```

---

## ✅ CHECKPOINT — Lecture 9 (Unit II · L4)
- [ ] Create a GET route using a route parameter (`:id`)
- [ ] Create a GET route using a query string (`req.query`)
- [ ] Add `body-parser` (or `express.json()`) middleware
- [ ] Create a POST route that reads `req.body` and responds with status `201`

---

# 🧩 LECTURE 10 (Unit II · L5): `express.Router` & `express-validator`

## 🎯 What You Will Know By the End
- Why route files get messy in one giant `app.js`
- How to organize routes using `express.Router`
- How to validate incoming request data with `express-validator`

## 5.1 The Problem: One Giant File 😵

```mermaid
flowchart TD
    Bad["❌ app.js
    50+ routes,
    500+ lines"] --> Problem["Hard to maintain,
    merge conflicts,
    no separation of concerns"]
```

## 5.2 `express.Router` — Modular Routing 🗂️

```mermaid
flowchart LR
    App["app.js"] -->|"app.use('/students', ...)"| R1["studentRoutes.js
    (Router)"]
    App -->|"app.use('/courses', ...)"| R2["courseRoutes.js
    (Router)"]
```

### 🧪 Minimal Working Example

**`studentRoutes.js`**
```javascript
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('📋 List of all students');
});

router.get('/:id', (req, res) => {
  res.send(`👤 Student #${req.params.id}`);
});

module.exports = router;
```

**`app.js`**
```javascript
const express = require('express');
const studentRoutes = require('./studentRoutes');

const app = express();
app.use('/students', studentRoutes);   // mounts router at /students

app.listen(3000, () => console.log('Server running...'));
```

Now `GET /students/` and `GET /students/5` both work, cleanly separated from `app.js`. ✨

## 5.3 Validating Input with `express-validator` ✅

Never trust client input! `express-validator` checks incoming data **before** your route logic runs.

```bash
npm install express-validator
```

```mermaid
sequenceDiagram
    participant C as Client
    participant V as express-validator
    participant R as Route Handler

    C->>V: POST /register {email: "not-an-email"}
    V->>V: Runs validation rules
    alt Validation fails
        V-->>C: 400 Bad Request + error list
    else Validation passes
        V->>R: Request continues
        R-->>C: 201 Created
    end
```

### 🧪 Minimal Working Example
```javascript
const express = require('express');
const { body, validationResult } = require('express-validator');
const app = express();

app.use(express.json());

app.post(
  '/register',
  [
    body('name').notEmpty().withMessage('Name is required'),
    body('email').isEmail().withMessage('Valid email is required'),
  ],
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    res.status(201).send('✅ Registration successful!');
  }
);

app.listen(3000, () => console.log('Server running...'));
```

**Bad request → response:**
```json
{
  "errors": [
    { "msg": "Valid email is required", "path": "email", "location": "body" }
  ]
}
```

---

## ✅ CHECKPOINT — Lecture 10 (Unit II · L5)
- [ ] Move at least one route group into a separate `express.Router` file
- [ ] Mount that router in `app.js` with `app.use('/prefix', router)`
- [ ] Install `express-validator` and add a `notEmpty()` rule
- [ ] Return a `400` response with the error list when validation fails

---

# 🏁 Unit II Summary Map

```mermaid
mindmap
  root((Unit II: HTTP Services))
    Raw HTTP
      http module
      createServer
      req and res objects
      Manual routing
    Headers and Status Codes
      Content-Type
      2xx 3xx 4xx 5xx
    Express Basics
      Installation
      app.get and app.post
    Data Handling
      body-parser
      express.json
      req.body
    Modularity
      express.Router
      express-validator
```


---

# 📚 Unit III — Socket Services & Middlewares in Node.js
### Lectures 11 – 15 (5 × 50 minutes)

---

> **Unit Roadmap**

```mermaid
flowchart LR
    L1["🔌 Lecture 1
    Network Sockets,
    Basic WebSocket Server"] --> L2["💬 Lecture 2
    Sending and Receiving
    Messages, Broadcast"]
    L2 --> L3["🗨️ Lecture 3
    Socket.IO
    Chat Server"]
    L3 --> L4["🧱 Lecture 4
    Middleware, app.use,
    app.all"]
    L4 --> L5["🍪 Lecture 5
    cookie-parser,
    cookie-session,
    express-session"]
```

---

# 🔌 LECTURE 11 (Unit III · L1): Understanding Network Sockets & Creating a Basic WebSocket Server

## 🎯 What You Will Know By the End
- What a network socket is
- Why plain HTTP is not enough for real-time apps
- How to create a basic WebSocket server and connect to it from a browser

## 1.1 What is a Network Socket? 🤔

A **socket** is one endpoint of a two-way communication link between two programs over a network. It is identified by an **IP address + port number**.

```mermaid
flowchart LR
    A["💻 Client
    IP: 192.168.1.5
    Port: 51234"] <-->|"Connection"| B["🖥️ Server
    IP: 192.168.1.10
    Port: 3000"]
```

> 🧠 **Analogy:** IP address = building address, port = room number, socket = the open phone line between two rooms.

### 🧪 Minimal Example — A Raw TCP Socket (core `net` module)
```javascript
// tcp-server.js
const net = require('net');

const server = net.createServer((socket) => {
  console.log('🔗 Client connected');
  socket.write('Welcome to the TCP server!\n');

  socket.on('data', (data) => {
    console.log('Received:', data.toString());
    socket.write(`You said: ${data}`);
  });

  socket.on('end', () => console.log('❌ Client disconnected'));
});

server.listen(4000, () => console.log('TCP server on port 4000'));
```
Test it (in another terminal): `telnet localhost 4000` (or `nc localhost 4000`) and type something.

## 1.2 The Problem with HTTP for Real-Time Apps 😓

HTTP is **request → response**. The server can **never** talk first.

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    Note over C,S: HTTP - client must always ask first
    C->>S: Any new messages?
    S-->>C: No
    C->>S: Any new messages now?
    S-->>C: No
    C->>S: And now?
    S-->>C: Yes, one message
```
This repeated asking is called **polling** — wasteful and slow.

## 1.3 WebSocket — A Persistent, Two-Way Connection ⚡

**WebSocket** starts as an HTTP request, then **upgrades** to a permanent two-way channel. After that, *either side can send data at any time*.

```mermaid
sequenceDiagram
    participant C as Browser
    participant S as WebSocket Server

    C->>S: HTTP GET with Upgrade: websocket
    S-->>C: 101 Switching Protocols
    Note over C,S: Connection stays OPEN
    C->>S: Hello server
    S->>C: Hello client
    S->>C: Server can push data anytime
    C->>S: Client can send anytime
```

| | HTTP | WebSocket |
|---|---|---|
| Direction | Client → Server → Client | Full-duplex (both ways) |
| Connection | Opens and closes per request | Stays open |
| Server can push? | ❌ No | ✅ Yes |
| URL scheme | `http://` / `https://` | `ws://` / `wss://` |
| Typical use | Web pages, REST APIs | Chat, live scores, games, notifications |

## 1.4 Creating a Basic WebSocket Server 🛠️

Node has no built-in WebSocket server, so we use the popular **`ws`** package.

```bash
mkdir ws-demo && cd ws-demo
npm init -y
npm install ws
```

### 🧪 `server.js` — Minimal WebSocket Server
```javascript
const { WebSocketServer } = require('ws');

const wss = new WebSocketServer({ port: 8080 });

wss.on('connection', (ws) => {
  console.log('✅ New client connected');
  ws.send('👋 Welcome to the WebSocket server!');

  ws.on('close', () => console.log('❌ Client disconnected'));
});

console.log('🚀 WebSocket server running on ws://localhost:8080');
```

### 🧪 `client.html` — Browser Client (just double-click to open)
```html
<!DOCTYPE html>
<html>
<body>
  <h2>WebSocket Client</h2>
  <div id="log"></div>

  <script>
    const socket = new WebSocket('ws://localhost:8080');

    socket.onopen = () => console.log('Connected!');
    socket.onmessage = (event) => {
      document.getElementById('log').innerHTML += `<p>📩 ${event.data}</p>`;
    };
  </script>
</body>
</html>
```
Run `node server.js`, then open `client.html`. The welcome message appears instantly.

### Connection Lifecycle
```mermaid
flowchart LR
    A["connection"] --> B["message"]
    B --> B
    B --> C["close"]
    A --> D["error"]
```

---

## ✅ CHECKPOINT — Lecture 11 (Unit III · L1)
- [ ] Define a socket as IP + port endpoint
- [ ] Explain why HTTP polling is inefficient for real-time apps
- [ ] State two differences between HTTP and WebSocket
- [ ] Run the `ws` server and connect from the HTML client

---

# 💬 LECTURE 12 (Unit III · L2): Sending & Receiving Messages, Broadcasting

## 🎯 What You Will Know By the End
- How to receive messages on the server and reply
- How to send messages from the browser
- How to broadcast a message to all connected clients
- How to exchange structured JSON messages

## 2.1 Receiving and Replying (Echo Server) 🔁

```mermaid
sequenceDiagram
    participant B as Browser
    participant S as Server

    B->>S: socket.send Hello
    S->>S: on message event fires
    S-->>B: ws.send Echo Hello
    B->>B: onmessage event fires
```

### 🧪 `server.js`
```javascript
const { WebSocketServer } = require('ws');
const wss = new WebSocketServer({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (data) => {
    const text = data.toString();       // data arrives as a Buffer
    console.log('📥 Received:', text);
    ws.send(`Echo: ${text}`);
  });
});
```
> ⚠️ **Gotcha:** In `ws` v8+, incoming messages are **Buffers**. Always call `.toString()`.

### 🧪 `client.html`
```html
<input id="msg" placeholder="Type a message" />
<button onclick="sendMsg()">Send</button>
<div id="log"></div>

<script>
  const socket = new WebSocket('ws://localhost:8080');

  socket.onmessage = (e) => {
    document.getElementById('log').innerHTML += `<p>📩 ${e.data}</p>`;
  };

  function sendMsg() {
    const input = document.getElementById('msg');
    socket.send(input.value);
    input.value = '';
  }
</script>
```

## 2.2 Broadcasting to All Clients 📢

```mermaid
flowchart TD
    C1["👤 Client A sends Hi"] --> S["🖥️ Server"]
    S --> C1b["👤 Client A receives"]
    S --> C2["👤 Client B receives"]
    S --> C3["👤 Client C receives"]
```

`wss.clients` is a **Set** of all connected sockets. Loop over it and send.

```javascript
const { WebSocketServer, WebSocket } = require('ws');
const wss = new WebSocketServer({ port: 8080 });

wss.on('connection', (ws) => {
  ws.on('message', (data) => {
    const text = data.toString();

    wss.clients.forEach((client) => {
      if (client.readyState === WebSocket.OPEN) {   // only send to open connections
        client.send(text);
      }
    });
  });
});
```
Open `client.html` in **two browser tabs** — a message typed in one appears in both.

| `readyState` | Meaning |
|---|---|
| `0` CONNECTING | Handshake in progress |
| `1` OPEN | ✅ Safe to send |
| `2` CLOSING | Closing handshake |
| `3` CLOSED | Connection closed |

## 2.3 Sending Structured Data (JSON) 📦

Real apps send **objects**, not plain strings. Convert with `JSON.stringify` / `JSON.parse`.

```javascript
// Server
ws.on('message', (data) => {
  const msg = JSON.parse(data.toString());   // { user: 'Riya', text: 'Hello' }

  const out = JSON.stringify({
    user: msg.user,
    text: msg.text,
    time: new Date().toLocaleTimeString(),
  });

  wss.clients.forEach((c) => c.readyState === WebSocket.OPEN && c.send(out));
});
```
```javascript
// Browser
socket.send(JSON.stringify({ user: 'Riya', text: 'Hello' }));

socket.onmessage = (e) => {
  const m = JSON.parse(e.data);
  console.log(`[${m.time}] ${m.user}: ${m.text}`);
};
```

## 2.4 Why Do We Need Something More Than `ws`? 🤷
Raw WebSocket leaves you to build: reconnection, rooms, event names, fallbacks. **Socket.IO** adds these (next lecture).

---

## ✅ CHECKPOINT — Lecture 12 (Unit III · L2)
- [ ] Receive a message on the server and convert the Buffer to string
- [ ] Build an echo server and test it from the browser
- [ ] Broadcast a message to all clients (two browser tabs)
- [ ] Send and parse a JSON message in both directions

---

# 🗨️ LECTURE 13 (Unit III · L3): Socket.IO Chat Server

## 🎯 What You Will Know By the End
- What Socket.IO adds over plain WebSocket
- The `emit` / `on` event model
- How to build a complete working chat application

## 3.1 What is Socket.IO? 🧰

Socket.IO is a library for real-time, event-based communication. It uses WebSocket when possible and **falls back** to other transports if not.

| Feature | Raw `ws` | Socket.IO |
|---|---|---|
| Custom named events | ❌ | ✅ `emit('chat message')` |
| Auto-reconnect | ❌ | ✅ |
| Rooms / namespaces | ❌ | ✅ |
| Broadcast helpers | Manual loop | ✅ `io.emit()` |
| Fallback transport | ❌ | ✅ |

> 📌 Socket.IO client and server must **both** be Socket.IO — it is *not* a plain WebSocket endpoint.

## 3.2 The Core Idea: `emit` and `on` 🔔

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    C->>S: socket.emit chat message with Hello
    S->>S: socket.on chat message runs
    S->>C: io.emit chat message with Hello
    C->>C: socket.on chat message runs
```

| Method | Who gets it? |
|---|---|
| `socket.emit(...)` | Just this one client |
| `io.emit(...)` | **Everyone** connected |
| `socket.broadcast.emit(...)` | Everyone **except** the sender |
| `io.to(room).emit(...)` | Everyone in a room |

## 3.3 Project Setup 🛠️

```bash
mkdir chat-app && cd chat-app
npm init -y
npm install express socket.io
mkdir public
```

```
chat-app/
├── server.js
├── package.json
└── public/
    └── index.html
```

## 3.4 The Server — `server.js` 🖥️

```javascript
const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);   // Socket.IO needs the raw http server
const io = new Server(server);

app.use(express.static('public'));       // serves public/index.html

io.on('connection', (socket) => {
  console.log('✅ Connected:', socket.id);

  // 1. User joins with a name
  socket.on('join', (username) => {
    socket.username = username;
    socket.broadcast.emit('system message', `🟢 ${username} joined the chat`);
  });

  // 2. A chat message arrives -> send to everyone
  socket.on('chat message', (text) => {
    io.emit('chat message', { user: socket.username, text });
  });

  // 3. User disconnects
  socket.on('disconnect', () => {
    if (socket.username) {
      io.emit('system message', `🔴 ${socket.username} left the chat`);
    }
  });
});

server.listen(3000, () => console.log('🚀 Chat at http://localhost:3000'));
```

## 3.5 The Client — `public/index.html` 💻

```html
<!DOCTYPE html>
<html>
<head>
  <title>INT369 Chat</title>
  <style>
    body { font-family: sans-serif; max-width: 500px; margin: 30px auto; }
    #messages { list-style: none; padding: 0; height: 300px; overflow-y: auto;
                border: 1px solid #ccc; }
    #messages li { padding: 6px 10px; }
    .system { color: gray; font-style: italic; }
  </style>
</head>
<body>
  <h2>💬 Class Chat</h2>
  <ul id="messages"></ul>
  <form id="form">
    <input id="input" autocomplete="off" placeholder="Type a message..." />
    <button>Send</button>
  </form>

  <script src="/socket.io/socket.io.js"></script>
  <script>
    const socket = io();                       // connect to the same host
    const username = prompt('Your name?') || 'Anonymous';
    socket.emit('join', username);

    const messages = document.getElementById('messages');
    const form = document.getElementById('form');
    const input = document.getElementById('input');

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      if (input.value) {
        socket.emit('chat message', input.value);
        input.value = '';
      }
    });

    function addLine(html, cls) {
      const li = document.createElement('li');
      li.innerHTML = html;
      if (cls) li.className = cls;
      messages.appendChild(li);
      messages.scrollTop = messages.scrollHeight;
    }

    socket.on('chat message', (m) => addLine(`<b>${m.user}:</b> ${m.text}`));
    socket.on('system message', (t) => addLine(t, 'system'));
  </script>
</body>
</html>
```
> ⚠️ **Teaching note:** `innerHTML` with user text is vulnerable to XSS. In production use `textContent`. Good moment to mention input sanitization.

**Run:** `node server.js` → open `http://localhost:3000` in two tabs.

## 3.6 Full Flow at a Glance

```mermaid
sequenceDiagram
    participant A as Tab A - Riya
    participant S as Socket.IO Server
    participant B as Tab B - Aman

    A->>S: join Riya
    S->>B: system message Riya joined
    B->>S: chat message Hi Riya
    S->>A: chat message from Aman
    S->>B: chat message from Aman
    A->>S: disconnect
    S->>B: system message Riya left
```

## 3.7 Bonus: Rooms 🚪 (2-minute demo)
```javascript
socket.on('join room', (room) => {
  socket.join(room);
  io.to(room).emit('system message', `${socket.username} entered ${room}`);
});
```

---

## ✅ CHECKPOINT — Lecture 13 (Unit III · L3)
- [ ] Differentiate `socket.emit`, `io.emit`, `socket.broadcast.emit`
- [ ] Explain why `http.createServer(app)` is needed
- [ ] Run the chat in two tabs and exchange messages
- [ ] See join/leave notifications working

---

# 🧱 LECTURE 14 (Unit III · L4): Introduction to Middleware, `app.use()` & `app.all()`

## 🎯 What You Will Know By the End
- What middleware is and how the request pipeline works
- How to write and order custom middleware
- Difference between `app.use()`, `app.get()` and `app.all()`
- How error-handling middleware works

## 4.1 What is Middleware? 🧅

**Middleware** is a function that runs **between** the incoming request and the final response. It can read/modify `req` and `res`, end the cycle, or pass control on with `next()`.

```mermaid
flowchart LR
    Req["📥 Request"] --> M1["🧱 Logger"]
    M1 -->|"next"| M2["🧱 Auth Check"]
    M2 -->|"next"| M3["🧱 JSON Parser"]
    M3 -->|"next"| H["🎯 Route Handler"]
    H --> Res["📤 Response"]
```

Middleware signature:
```javascript
function myMiddleware(req, res, next) {
  // do something
  next();   // 👈 pass control to the next function
}
```

> ⚠️ **The #1 beginner bug:** forgetting `next()` — the request just **hangs** forever.

## 4.2 Implementing Basic Middleware 🛠️

### 🧪 Example 1 — Logger
```javascript
const express = require('express');
const app = express();

function logger(req, res, next) {
  console.log(`${new Date().toISOString()}  ${req.method}  ${req.url}`);
  next();
}

app.use(logger);

app.get('/', (req, res) => res.send('Home'));
app.get('/about', (req, res) => res.send('About'));

app.listen(3000);
```
Visiting `/about` prints: `2026-... GET /about`

### 🧪 Example 2 — Blocking Middleware (simple auth)
```javascript
function requireKey(req, res, next) {
  if (req.query.key === 'secret123') {
    next();                                   // allowed
  } else {
    res.status(401).send('⛔ Unauthorized');  // stops here, no next()
  }
}

app.get('/dashboard', requireKey, (req, res) => {
  res.send('📊 Welcome to the dashboard');
});
```
`/dashboard?key=secret123` ✅ works. `/dashboard` ❌ 401.

### 🧪 Example 3 — Modifying `req`
```javascript
app.use((req, res, next) => {
  req.requestTime = Date.now();    // attach data for later handlers
  next();
});

app.get('/time', (req, res) => res.send(`Request time: ${req.requestTime}`));
```

## 4.3 `app.use()` vs `app.get()` vs `app.all()` 🔍

| Method | Matches | Typical use |
|---|---|---|
| `app.use(fn)` | **Every** request, all methods, all paths | Logging, parsers, sessions |
| `app.use('/api', fn)` | Any request whose path **starts with** `/api` | Mounting routers |
| `app.get('/x', fn)` | Only `GET /x` exactly | A single route |
| `app.all('/x', fn)` | `/x` for **every** HTTP method | Run logic regardless of method |

```javascript
// Runs for GET, POST, PUT, DELETE ... on /admin
app.all('/admin', (req, res, next) => {
  console.log(`Admin accessed via ${req.method}`);
  next();
});

app.get('/admin', (req, res) => res.send('Admin GET'));
app.post('/admin', (req, res) => res.send('Admin POST'));
```

> 📌 **Version note:** In Express 4 a catch-all route is `app.all('*', ...)`. In Express 5 the wildcard syntax changed to `app.all('/{*splat}', ...)`. Check your installed version with `npm list express`.

## 4.4 Order Matters ⚠️

Middleware runs **top to bottom**, in the order registered.

```mermaid
flowchart TD
    A["app.use logger"] --> B["app.use express.json"]
    B --> C["app.get routes"]
    C --> D["404 handler"]
    D --> E["Error handler"]
```

```javascript
app.use(express.json());                 // 1. parse body FIRST
app.post('/data', (req, res) => {        // 2. then routes can use req.body
  res.json(req.body);
});
app.use((req, res) => {                  // 3. fallthrough 404
  res.status(404).send('🚫 Not Found');
});
```

## 4.5 Error-Handling Middleware 🚨

An error handler has **four** parameters. Express recognises it by that count.

```javascript
app.get('/crash', (req, res) => {
  throw new Error('Something broke!');
});

// must be registered AFTER all routes
app.use((err, req, res, next) => {
  console.error(err.message);
  res.status(500).json({ error: err.message });
});
```

### Types of Middleware (summary)
```mermaid
mindmap
  root((Middleware))
    Application level
      app.use
      app.get
    Router level
      router.use
    Built in
      express.json
      express.static
    Third party
      cookie-parser
      express-session
    Error handling
      four parameters
```

---

## ✅ CHECKPOINT — Lecture 14 (Unit III · L4)
- [ ] Write a logger middleware and register it with `app.use()`
- [ ] Explain what happens if `next()` is not called
- [ ] State the difference between `app.use()` and `app.all()`
- [ ] Write an error-handling middleware (4 parameters)

---

# 🍪 LECTURE 15 (Unit III · L5): `cookie-parser`, `cookie-session` & `express-session`

## 🎯 What You Will Know By the End
- What cookies are and how HTTP "remembers" users
- How to read/write cookies with `cookie-parser`
- How `cookie-session` and `express-session` differ
- How to build a simple login/logout flow with sessions

## 5.1 Why Do We Need Cookies and Sessions? 🤔

HTTP is **stateless** — the server forgets you after every response. Cookies let the browser carry a small piece of data back on every request.

```mermaid
sequenceDiagram
    participant B as Browser
    participant S as Server

    B->>S: GET /
    S-->>B: Set-Cookie name=Riya
    Note over B: Browser stores the cookie
    B->>S: GET /profile with Cookie name=Riya
    S-->>B: Hello Riya
```

| Term | Meaning |
|---|---|
| 🍪 **Cookie** | Small key-value data stored in the **browser** |
| 🗄️ **Session** | Data about a user kept by the **server**, linked by a session ID cookie |

## 5.2 `cookie-parser` 🧁

By default Express can **set** cookies but cannot easily **read** them. `cookie-parser` fills `req.cookies`.

```bash
npm install express cookie-parser
```

```javascript
const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();

app.use(cookieParser('my-secret-key'));    // secret enables signed cookies

// SET a cookie
app.get('/set', (req, res) => {
  res.cookie('username', 'Riya', {
    maxAge: 60 * 60 * 1000,   // 1 hour in ms
    httpOnly: true,           // JavaScript in browser cannot read it
  });
  res.cookie('role', 'student', { signed: true });   // tamper-proof
  res.send('🍪 Cookies set');
});

// READ cookies
app.get('/read', (req, res) => {
  res.json({
    plain: req.cookies,          // { username: 'Riya' }
    signed: req.signedCookies,   // { role: 'student' }
  });
});

// DELETE a cookie
app.get('/clear', (req, res) => {
  res.clearCookie('username');
  res.send('🗑️ Cookie cleared');
});

app.listen(3000);
```

| Cookie option | Purpose |
|---|---|
| `maxAge` / `expires` | Lifetime |
| `httpOnly` | Blocks `document.cookie` access (protects from XSS theft) |
| `secure` | Only sent over HTTPS |
| `signed` | Detects tampering using the secret |
| `sameSite` | Limits cross-site sending (CSRF protection) |

> 🚨 **Never store passwords or sensitive data in a plain cookie.**

## 5.3 `cookie-session` — Session Stored *in the Cookie* 📦

The whole session object is **serialized into the cookie itself** and sent to the browser (signed, so it can't be altered, but it **can** be read by the user).

```bash
npm install cookie-session
```

```javascript
const express = require('express');
const cookieSession = require('cookie-session');
const app = express();

app.use(cookieSession({
  name: 'session',
  keys: ['secretKey1', 'secretKey2'],   // used to sign the cookie
  maxAge: 24 * 60 * 60 * 1000,          // 24 hours
}));

app.get('/visit', (req, res) => {
  req.session.views = (req.session.views || 0) + 1;
  res.send(`👀 You visited ${req.session.views} times`);
});

app.listen(3000);
```
Refresh the page — the counter increases. **No server memory used.**

```mermaid
flowchart LR
    B["🌐 Browser holds
    ALL session data
    in the cookie"] <-->|"each request"| S["🖥️ Server
    stores nothing"]
```

## 5.4 `express-session` — Session Stored *on the Server* 🗄️

Only a random **session ID** goes in the cookie. The real data lives **on the server**.

```bash
npm install express-session
```

```javascript
const express = require('express');
const session = require('express-session');
const app = express();

app.use(express.urlencoded({ extended: true }));

app.use(session({
  secret: 'change-this-secret',
  resave: false,              // don't re-save if nothing changed
  saveUninitialized: false,   // don't create empty sessions
  cookie: { maxAge: 60 * 60 * 1000 },   // 1 hour
}));

// Home — who am I?
app.get('/', (req, res) => {
  if (req.session.user) {
    res.send(`👋 Hello ${req.session.user}! <a href="/logout">Logout</a>`);
  } else {
    res.send(`
      <form method="POST" action="/login">
        <input name="username" placeholder="username" />
        <button>Login</button>
      </form>`);
  }
});

// Login — store data in the session
app.post('/login', (req, res) => {
  req.session.user = req.body.username;
  res.redirect('/');
});

// Protected route
app.get('/profile', (req, res) => {
  if (!req.session.user) return res.status(401).send('⛔ Please login first');
  res.send(`📄 Profile page of ${req.session.user}`);
});

// Logout — destroy the session
app.get('/logout', (req, res) => {
  req.session.destroy(() => res.redirect('/'));
});

app.listen(3000, () => console.log('Running on http://localhost:3000'));
```

```mermaid
sequenceDiagram
    participant B as Browser
    participant S as Express Server
    participant M as Session Store

    B->>S: POST /login username Riya
    S->>M: Save session abc123 with user Riya
    S-->>B: Set-Cookie connect.sid abc123
    B->>S: GET /profile with cookie abc123
    S->>M: Look up abc123
    M-->>S: user Riya
    S-->>B: Profile page of Riya
```

## 5.5 Comparison 📊

| | `cookie-parser` | `cookie-session` | `express-session` |
|---|---|---|---|
| Purpose | Read/write cookies | Session in cookie | Session on server |
| Data stored | Browser | **Browser** (in cookie) | **Server** (only ID in browser) |
| Size limit | ~4 KB | ~4 KB | Practically unlimited |
| Scales across servers | ✅ | ✅ (no shared store needed) | Needs shared store (Redis, DB) |
| Sensitive data safe? | ❌ | ❌ (user can read it) | ✅ Better |

> ⚠️ `express-session`'s default **MemoryStore** is only for development — it leaks memory and loses all sessions on restart. Production apps use a store such as Redis or MongoDB.

---

## ✅ CHECKPOINT — Lecture 15 (Unit III · L5)
- [ ] Set, read and clear a cookie using `cookie-parser`
- [ ] Explain `httpOnly`, `secure` and `signed` options
- [ ] Build a visit counter with `cookie-session`
- [ ] Build login / protected route / logout with `express-session`
- [ ] State one key difference between `cookie-session` and `express-session`

---

# 🏁 Unit III Summary Map

```mermaid
mindmap
  root((Unit III))
    Sockets
      IP plus port
      TCP net module
      WebSocket upgrade
      ws package
    Messaging
      send and receive
      broadcast
      JSON messages
      Socket.IO emit and on
      Chat server
    Middleware
      next function
      app.use
      app.all
      Error handling
    State management
      cookie-parser
      cookie-session
      express-session
```


---

# 📚 Unit IV — MongoDB & Mongoose
### Lectures 16 – 21 (6 × 50 minutes)

---

> **Unit Roadmap**

```mermaid
flowchart LR
    L1["🍃 Lecture 1
    Intro, Install,
    Terminology"] --> L2["🗂️ Lecture 2
    Documents, Collections,
    Shell: create/drop"]
    L2 --> L3["✏️ Lecture 3
    Shell CRUD:
    insert, find,
    update, delete"]
    L3 --> L4["🔗 Lecture 4
    Node.js Driver
    CRUD"]
    L4 --> L5["📐 Lecture 5
    Mongoose:
    Schema and Models"]
    L5 --> L6["🚀 Lecture 6
    Mongoose CRUD
    plus Express API"]
```

---

# 🍃 LECTURE 16 (Unit IV · L1): Introduction to MongoDB, Installation & Terminology

## 🎯 What You Will Know By the End
- What MongoDB is and how it differs from SQL databases
- How to install MongoDB and the shell (`mongosh`)
- Core terms: database, collection, document, field

## 1.1 What is MongoDB? 🤔

MongoDB is a **NoSQL, document-oriented database**. Instead of rows and tables, it stores **JSON-like documents** (internally BSON) in **collections**.

```mermaid
flowchart LR
    subgraph SQL["🏛️ Relational - SQL"]
        T["Table: students"] --> R["Rows and Columns
        fixed schema"]
    end
    subgraph NoSQL["🍃 MongoDB"]
        C["Collection: students"] --> D["Documents
        flexible schema"]
    end
```

| Feature | SQL (MySQL/PostgreSQL) | MongoDB |
|---|---|---|
| Data unit | Row | **Document** |
| Group of data | Table | **Collection** |
| Schema | Fixed, defined upfront | Flexible, can vary per document |
| Data format | Rows/columns | JSON-like (BSON) |
| Relationships | Joins | Embedding or references |
| Scaling | Mostly vertical | Built for horizontal scaling |

### 🧪 One Student, Two Worlds
**SQL — spread across tables:**
```
students: | id | name | city   |
          | 1  | Riya | Jalandhar |
phones:   | student_id | number     |
          | 1          | 98xxxxxx01 |
          | 1          | 98xxxxxx02 |
```
**MongoDB — one self-contained document:**
```json
{
  "name": "Riya",
  "city": "Jalandhar",
  "phones": ["98xxxxxx01", "98xxxxxx02"]
}
```

## 1.2 MongoDB Terminology 📖

```mermaid
flowchart TD
    Server["🖥️ MongoDB Server"] --> DB1["🗄️ Database: college"]
    Server --> DB2["🗄️ Database: shop"]
    DB1 --> Col1["📁 Collection: students"]
    DB1 --> Col2["📁 Collection: courses"]
    Col1 --> Doc1["📄 Document
    name: Riya, cgpa: 8.9"]
    Col1 --> Doc2["📄 Document
    name: Aman, cgpa: 8.1"]
```

| MongoDB Term | SQL Equivalent | Meaning |
|---|---|---|
| **Database** | Database | Container for collections |
| **Collection** | Table | Group of related documents |
| **Document** | Row | One record, a set of key-value pairs |
| **Field** | Column | A single key-value pair inside a document |
| `_id` | Primary key | Unique ID, auto-added to every document |

## 1.3 Installing MongoDB 🛠️

You need **two** things:

1. **MongoDB Community Server** — the database engine (`mongod`)
2. **MongoDB Shell (`mongosh`)** — the command-line client

### Steps
1. Go to the MongoDB Download Center → download **MongoDB Community Server** for your OS and install it (on Windows, choose "Run as a Service").
2. Download and install **MongoDB Shell (mongosh)** from the same site's tools section.
3. Verify:
```bash
mongod --version
mongosh --version
```
4. Connect:
```bash
mongosh
```
Default connection: `mongodb://127.0.0.1:27017`

```mermaid
sequenceDiagram
    participant U as You
    participant SH as mongosh
    participant SV as mongod on port 27017

    U->>SH: type mongosh
    SH->>SV: connect
    SV-->>SH: connected
    U->>SH: show dbs
    SH->>SV: list databases
    SV-->>U: admin, config, local
```

> 💡 **No local install?** Use **MongoDB Atlas** (free cloud tier) and connect `mongosh` or Node.js with the connection string it provides. Installation steps and menus change over time, so follow the current on-screen instructions.

### First Commands
```javascript
show dbs          // list databases
db                // current database name
help              // list shell help
```

---

## ✅ CHECKPOINT — Lecture 16 (Unit IV · L1)
- [ ] Explain MongoDB as a document database in one sentence
- [ ] Map: database / collection / document / field to SQL terms
- [ ] Install Community Server and `mongosh` (or set up Atlas)
- [ ] Run `mongosh` and execute `show dbs`

---

# 🗂️ LECTURE 17 (Unit IV · L2): Documents, Collections & Shell Commands (Create / Drop)

## 🎯 What You Will Know By the End
- The structure of a MongoDB document (fields, types, nesting, arrays)
- How to create and drop databases and collections
- How `_id` and `ObjectId` work

## 2.1 Anatomy of a Document 📄

```javascript
{
  _id: ObjectId("665f1c2e9b1e8a0012345678"),   // auto-generated
  name: "Riya Sharma",                          // String
  age: 21,                                      // Number
  cgpa: 8.9,                                    // Number
  isHosteller: true,                            // Boolean
  skills: ["Node.js", "MongoDB"],               // Array
  address: { city: "Phagwara", state: "Punjab" }, // Embedded document
  joinedOn: new Date("2023-07-15")              // Date
}
```

```mermaid
flowchart TD
    D["📄 Document"] --> F1["name: String"]
    D --> F2["age: Number"]
    D --> F3["skills: Array"]
    D --> F4["address: Embedded Document"]
    D --> F5["_id: ObjectId"]
```

| Type | Example |
|---|---|
| String | `"Riya"` |
| Number | `21`, `8.9` |
| Boolean | `true` |
| Array | `["a", "b"]` |
| Object (embedded) | `{ city: "Phagwara" }` |
| Date | `new Date()` |
| ObjectId | `ObjectId("...")` |
| Null | `null` |

> 🧠 **Flexible schema:** two documents in the same collection may have *different* fields. That flexibility is MongoDB's strength — and a risk, which is why Mongoose (Lecture 5) exists.

## 2.2 Creating a Database 🗄️

In MongoDB, a database is created **lazily** — it appears only when you store data in it.

```javascript
show dbs                 // college is NOT listed yet
use college              // switch to (or prepare) 'college'
db                       // college
db.students.insertOne({ name: "Riya" })   // NOW the database exists
show dbs                 // college is listed
```

```mermaid
flowchart LR
    A["use college"] --> B["Database selected
    but not saved yet"]
    B --> C["insert first document"]
    C --> D["✅ Database and
    collection created"]
```

## 2.3 Creating Collections 📁

**Way 1 — Implicit** (most common): insert a document, collection is auto-created.
```javascript
db.courses.insertOne({ code: "INT369", title: "Advanced Web Programming" })
```

**Way 2 — Explicit:**
```javascript
db.createCollection("teachers")
```

**List collections:**
```javascript
show collections
```

## 2.4 Dropping Collections and Databases 🗑️

```javascript
db.teachers.drop()          // drop one collection  -> true
db.dropDatabase()           // drop the CURRENT database
```

> ⚠️ **Both are permanent.** Always run `db` first to confirm which database you are in.

### Cheat Sheet
| Task | Command |
|---|---|
| List databases | `show dbs` |
| Switch / create database | `use <name>` |
| Show current database | `db` |
| Create collection | `db.createCollection("name")` |
| List collections | `show collections` |
| Drop collection | `db.<name>.drop()` |
| Drop database | `db.dropDatabase()` |

---

## ✅ CHECKPOINT — Lecture 17 (Unit IV · L2)
- [ ] Write a document containing a string, number, array and embedded object
- [ ] Explain why `show dbs` doesn't list a new database until data is inserted
- [ ] Create a collection both implicitly and with `createCollection`
- [ ] Drop a collection and then the database

---

# ✏️ LECTURE 18 (Unit IV · L3): Data Manipulation in the Shell — Insert, Find, Update, Delete

## 🎯 What You Will Know By the End
- How to perform all four CRUD operations in `mongosh`
- Query operators (`$gt`, `$in`, `$or` ...) and update operators (`$set`, `$inc`)
- Sorting, limiting and projecting results

```mermaid
flowchart LR
    C["➕ Create
    insertOne
    insertMany"] --- R["🔍 Read
    find
    findOne"] --- U["✏️ Update
    updateOne
    updateMany"] --- D["🗑️ Delete
    deleteOne
    deleteMany"]
```

## 3.1 Create — Insert 🟢

```javascript
use college

db.students.insertOne({ name: "Riya", age: 21, cgpa: 8.9, city: "Jalandhar" })

db.students.insertMany([
  { name: "Aman",  age: 22, cgpa: 8.1, city: "Ludhiana" },
  { name: "Simran", age: 20, cgpa: 9.3, city: "Jalandhar" },
  { name: "Karan", age: 23, cgpa: 6.8, city: "Amritsar" }
])
```

## 3.2 Read — Find 🔵

```javascript
db.students.find()                        // all documents
db.students.find().pretty()               // formatted (default in mongosh)
db.students.findOne({ name: "Riya" })     // first match only
db.students.find({ city: "Jalandhar" })   // filter by equality
```

### Comparison & Logical Operators
| Operator | Meaning | Example |
|---|---|---|
| `$eq` | equal | `{ age: { $eq: 21 } }` |
| `$gt` / `$gte` | greater than / or equal | `{ cgpa: { $gt: 8 } }` |
| `$lt` / `$lte` | less than / or equal | `{ age: { $lt: 22 } }` |
| `$ne` | not equal | `{ city: { $ne: "Ludhiana" } }` |
| `$in` | in a list | `{ city: { $in: ["Jalandhar", "Amritsar"] } }` |
| `$and` / `$or` | combine conditions | `{ $or: [ {age: 20}, {cgpa: {$gt: 9}} ] }` |

```javascript
db.students.find({ cgpa: { $gt: 8 } })

db.students.find({ city: "Jalandhar", cgpa: { $gt: 9 } })   // implicit AND

db.students.find({ $or: [ { age: 20 }, { cgpa: { $lt: 7 } } ] })
```

### Projection, Sorting, Limiting
```javascript
db.students.find({}, { name: 1, cgpa: 1, _id: 0 })   // only name and cgpa
db.students.find().sort({ cgpa: -1 })                // highest first (-1 desc, 1 asc)
db.students.find().sort({ cgpa: -1 }).limit(2)       // top 2
db.students.countDocuments({ city: "Jalandhar" })    // count -> 2
```

## 3.3 Update — Modify ✏️

Always use an **update operator**. Without one, you may replace the whole document.

```javascript
// Set / change a field
db.students.updateOne({ name: "Riya" }, { $set: { cgpa: 9.1 } })

// Increment a number
db.students.updateOne({ name: "Aman" }, { $inc: { age: 1 } })

// Update many
db.students.updateMany({ city: "Jalandhar" }, { $set: { hostel: "BH-3" } })

// Add to an array / remove a field
db.students.updateOne({ name: "Riya" }, { $push: { skills: "Node.js" } })
db.students.updateOne({ name: "Riya" }, { $unset: { hostel: "" } })

// Upsert: update if exists, otherwise insert
db.students.updateOne({ name: "Neha" }, { $set: { cgpa: 8.5 } }, { upsert: true })
```

| Operator | Effect |
|---|---|
| `$set` | Set or add a field |
| `$unset` | Remove a field |
| `$inc` | Add to a number |
| `$push` | Append to an array |
| `$pull` | Remove from an array |

## 3.4 Delete — Remove 🔴

```javascript
db.students.deleteOne({ name: "Karan" })
db.students.deleteMany({ cgpa: { $lt: 7 } })
db.students.deleteMany({})          // ⚠️ removes ALL documents, keeps collection
```

### Shell Result Objects
```javascript
{ acknowledged: true, insertedId: ObjectId("...") }                        // insertOne
{ acknowledged: true, matchedCount: 1, modifiedCount: 1 }                  // updateOne
{ acknowledged: true, deletedCount: 1 }                                    // deleteOne
```

---

## ✅ CHECKPOINT — Lecture 18 (Unit IV · L3)
- [ ] Insert one and many documents
- [ ] Find students with `cgpa > 8` and sort by `cgpa` descending
- [ ] Use `$set` and `$inc` to update documents
- [ ] Delete using `deleteOne` and `deleteMany`
- [ ] Explain why `deleteMany({})` differs from `drop()`

---

# 🔗 LECTURE 19 (Unit IV · L4): Connecting MongoDB with Node.js (Native Driver) & CRUD

## 🎯 What You Will Know By the End
- How a Node.js app talks to MongoDB
- How to connect using the official `mongodb` driver
- How to perform CRUD operations with `async/await`

## 4.1 How Node.js Talks to MongoDB 🌉

```mermaid
flowchart LR
    App["🟩 Node.js App"] -->|"mongodb driver"| Server["🍃 MongoDB Server
    port 27017"]
    Server -->|"results"| App
```

```bash
mkdir mongo-driver-demo && cd mongo-driver-demo
npm init -y
npm install mongodb
```

> 💡 Use `127.0.0.1` instead of `localhost` in the URI. On newer Node versions `localhost` can resolve to IPv6 `::1` and the connection may fail.

## 4.2 Connect 🔌

```javascript
// connect.js
const { MongoClient } = require('mongodb');

const uri = 'mongodb://127.0.0.1:27017';
const client = new MongoClient(uri);

async function main() {
  try {
    await client.connect();
    console.log('✅ Connected to MongoDB');

    const db = client.db('college');            // database
    const students = db.collection('students'); // collection
    // ... CRUD goes here
  } finally {
    await client.close();                       // always close
  }
}

main().catch(console.error);
```

```mermaid
sequenceDiagram
    participant N as Node App
    participant M as MongoDB

    N->>M: client.connect
    M-->>N: connected
    N->>M: collection.insertOne
    M-->>N: insertedId
    N->>M: client.close
```

## 4.3 Full CRUD Example 🧪

```javascript
// crud.js
const { MongoClient, ObjectId } = require('mongodb');

const client = new MongoClient('mongodb://127.0.0.1:27017');

async function main() {
  try {
    await client.connect();
    const students = client.db('college').collection('students');

    // ➕ CREATE
    const ins = await students.insertOne({ name: 'Riya', cgpa: 8.9, city: 'Jalandhar' });
    console.log('Inserted ID:', ins.insertedId);

    await students.insertMany([
      { name: 'Aman', cgpa: 8.1, city: 'Ludhiana' },
      { name: 'Simran', cgpa: 9.3, city: 'Jalandhar' },
    ]);

    // 🔍 READ
    const all = await students.find({}).toArray();          // .toArray() is required
    console.log('All:', all);

    const topper = await students.find({ cgpa: { $gt: 9 } }).toArray();
    console.log('Toppers:', topper);

    const one = await students.findOne({ name: 'Riya' });
    console.log('One:', one);

    const byId = await students.findOne({ _id: new ObjectId(ins.insertedId) });
    console.log('By ID:', byId.name);

    // ✏️ UPDATE
    const upd = await students.updateOne(
      { name: 'Riya' },
      { $set: { cgpa: 9.1 } }
    );
    console.log('Modified:', upd.modifiedCount);

    // 🗑️ DELETE
    const del = await students.deleteOne({ name: 'Aman' });
    console.log('Deleted:', del.deletedCount);
  } finally {
    await client.close();
  }
}

main().catch(console.error);
```
Run: `node crud.js`, then verify in `mongosh` with `use college` and `db.students.find()`.

| Shell | Node.js driver |
|---|---|
| `db.students.find()` | `await students.find({}).toArray()` |
| `db.students.insertOne({...})` | `await students.insertOne({...})` |
| `db.students.updateOne(f, u)` | `await students.updateOne(f, u)` |
| `db.students.deleteOne(f)` | `await students.deleteOne(f)` |
| `ObjectId("...")` | `new ObjectId("...")` (imported from `mongodb`) |

> ⚠️ **Common mistakes:** forgetting `await`; forgetting `.toArray()` on `find()`; passing an ID **string** where an `ObjectId` is needed.

---

## ✅ CHECKPOINT — Lecture 19 (Unit IV · L4)
- [ ] Install the `mongodb` package and connect with `MongoClient`
- [ ] Insert a document and print its `insertedId`
- [ ] Read documents with `find().toArray()` and `findOne()`
- [ ] Update and delete a document, then verify in `mongosh`

---

# 📐 LECTURE 20 (Unit IV · L5): Introduction to Mongoose — Schema Definition & Models

## 🎯 What You Will Know By the End
- Why Mongoose exists (the problem with a fully flexible schema)
- How to define a Schema with types, validation and defaults
- How a Model connects a Schema to a collection

## 5.1 Why Mongoose? 🤔

MongoDB lets you insert **anything**. That causes bugs:

```javascript
db.students.insertOne({ name: "Riya", cgpa: "high" })   // ❌ string instead of number, accepted!
db.students.insertOne({ nmae: "Aman" })                   // ❌ typo field, accepted!
```

**Mongoose** is an **ODM (Object Data Modeling)** library that adds structure, validation and a friendlier API on top of the driver.

```mermaid
flowchart LR
    App["🟩 Node App"] --> M["📐 Mongoose
    Schema, Validation,
    Models"] --> D["🍃 MongoDB"]
```

| Native Driver | Mongoose |
|---|---|
| No schema enforcement | Schema with types and rules |
| Manual validation | Built-in validators |
| `collection.find()` | `Model.find()` |
| Low level | Higher level, more convenient |

## 5.2 Setup and Connection 🔌

```bash
mkdir mongoose-demo && cd mongoose-demo
npm init -y
npm install mongoose
```

```javascript
// db.js
const mongoose = require('mongoose');

async function connectDB() {
  try {
    await mongoose.connect('mongodb://127.0.0.1:27017/college');
    console.log('✅ Mongoose connected');
  } catch (err) {
    console.error('❌ Connection error:', err.message);
    process.exit(1);
  }
}

module.exports = connectDB;
```
> The database name (`college`) is part of the URI.

## 5.3 Schema Definition 📐

A **Schema** defines the shape of documents: field names, types, and rules.

```mermaid
flowchart TD
    S["📐 Schema"] --> F1["name: String, required"]
    S --> F2["email: String, unique"]
    S --> F3["age: Number, min 16"]
    S --> F4["cgpa: Number, 0 to 10"]
    S --> F5["createdAt: Date, default now"]
```

```javascript
// models/Student.js
const mongoose = require('mongoose');

const studentSchema = new mongoose.Schema({
  name: {
    type: String,
    required: [true, 'Name is required'],
    trim: true,
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true,
  },
  age: {
    type: Number,
    min: [16, 'Age must be at least 16'],
    max: 60,
  },
  cgpa: {
    type: Number,
    min: 0,
    max: 10,
    default: 0,
  },
  course: {
    type: String,
    enum: ['BTech', 'MTech', 'BCA', 'MCA'],   // only these values allowed
  },
  skills: [String],                           // array of strings
  createdAt: {
    type: Date,
    default: Date.now,
  },
});
```

### Common Schema Types and Options
| Type | Example |
|---|---|
| `String` | `name: String` |
| `Number` | `age: Number` |
| `Boolean` | `isActive: Boolean` |
| `Date` | `joinedOn: Date` |
| `[String]` | Array of strings |
| `ObjectId` | Reference to another document |

| Option | Purpose |
|---|---|
| `required` | Must be present |
| `default` | Value used if none supplied |
| `unique` | Creates a unique index (not a validator) |
| `min` / `max` | Number range |
| `minlength` / `maxlength` | String length |
| `enum` | Allowed values |
| `trim` / `lowercase` | Auto-clean strings |

## 5.4 Models 🏭

A **Model** is a constructor compiled from a Schema. It represents a **collection** and is what you use to run queries.

```javascript
const Student = mongoose.model('Student', studentSchema);
module.exports = Student;
```

```mermaid
flowchart LR
    S["📐 Schema
    studentSchema"] -->|"mongoose.model"| M["🏭 Model
    Student"] -->|"maps to"| C["📁 Collection
    students"]
    M -->|"new Student"| Doc["📄 Document"]
```

> 🧠 Mongoose automatically **lowercases and pluralizes** the model name: `Student` → `students`.

### 🧪 First Use — Create a Document
```javascript
// index.js
const connectDB = require('./db');
const Student = require('./models/Student');

async function main() {
  await connectDB();

  const s = new Student({
    name: '  Riya  ',
    email: 'RIYA@lpu.in',
    age: 21,
    cgpa: 8.9,
    course: 'BTech',
    skills: ['Node.js', 'MongoDB'],
  });

  await s.save();
  console.log('Saved:', s);
}

main();
```
Notice: name is **trimmed**, email **lowercased**, `createdAt` **auto-filled**, `_id` auto-created.

### 🧪 Validation in Action
```javascript
try {
  await Student.create({ name: 'Aman', email: 'a@lpu.in', age: 12 });
} catch (err) {
  console.log(err.message);
  // Student validation failed: age: Age must be at least 16
}
```

---

## ✅ CHECKPOINT — Lecture 20 (Unit IV · L5)
- [ ] Explain the problem Mongoose solves vs the native driver
- [ ] Connect to MongoDB with `mongoose.connect`
- [ ] Write a Schema using `required`, `default`, `min`, `enum`
- [ ] Create a Model and save one document
- [ ] Trigger a validation error deliberately

---

# 🚀 LECTURE 21 (Unit IV · L6): Mongoose CRUD Operations & a Mini REST API

## 🎯 What You Will Know By the End
- All CRUD methods on a Mongoose Model
- How to handle validation and "not found" cases
- How to wire Mongoose into Express to build a CRUD API

## 6.1 Mongoose CRUD Methods 🧰

```mermaid
flowchart LR
    C["➕ Create
    Student.create
    new Student + save"] --- R["🔍 Read
    find, findOne
    findById"] --- U["✏️ Update
    findByIdAndUpdate
    updateOne"] --- D["🗑️ Delete
    findByIdAndDelete
    deleteOne"]
```

### 🧪 All Operations in One Script
```javascript
const connectDB = require('./db');
const Student = require('./models/Student');

async function main() {
  await connectDB();

  // ➕ CREATE
  const riya = await Student.create({ name: 'Riya', email: 'riya@lpu.in', age: 21, cgpa: 8.9 });
  await Student.insertMany([
    { name: 'Aman',   email: 'aman@lpu.in',   age: 22, cgpa: 8.1 },
    { name: 'Simran', email: 'simran@lpu.in', age: 20, cgpa: 9.3 },
  ]);

  // 🔍 READ
  const all     = await Student.find();                         // all
  const toppers = await Student.find({ cgpa: { $gt: 9 } });     // filter
  const one     = await Student.findOne({ name: 'Riya' });      // first match
  const byId    = await Student.findById(riya._id);             // by _id
  const sorted  = await Student.find().sort({ cgpa: -1 }).limit(2).select('name cgpa');

  // ✏️ UPDATE
  const updated = await Student.findByIdAndUpdate(
    riya._id,
    { cgpa: 9.4 },
    { new: true, runValidators: true }    // return NEW doc, run schema rules
  );

  // 🗑️ DELETE
  await Student.findOneAndDelete({ name: 'Aman' });
  await Student.deleteMany({ cgpa: { $lt: 5 } });

  console.log(updated);
}

main();
```

| Operation | Method | Returns |
|---|---|---|
| Create | `Model.create(obj)` | Saved document |
| Read many | `Model.find(filter)` | Array |
| Read one | `Model.findOne(filter)` / `findById(id)` | Document or `null` |
| Update | `Model.findByIdAndUpdate(id, data, opts)` | Document (old by default) |
| Update many | `Model.updateMany(filter, data)` | Result summary |
| Delete | `Model.findByIdAndDelete(id)` | Deleted document or `null` |
| Delete many | `Model.deleteMany(filter)` | `{ deletedCount }` |

> ⚠️ **Gotchas:** by default `findByIdAndUpdate` returns the **old** document — pass `{ new: true }`. Validators do **not** run on updates unless `runValidators: true`. Mongoose 7+ methods return **promises** only (no callbacks).

## 6.2 Mini Project — Student CRUD REST API with Express 🛠️

```mermaid
flowchart TD
    Client["📱 Client / Postman"] -->|"HTTP"| Express["🚏 Express routes"]
    Express --> Mongoose["📐 Mongoose Model"]
    Mongoose --> Mongo["🍃 MongoDB"]
```

```bash
npm install express mongoose
```

**Structure**
```
student-api/
├── server.js
├── db.js
└── models/Student.js     (from Lecture 5)
```

**`server.js`**
```javascript
const express = require('express');
const connectDB = require('./db');
const Student = require('./models/Student');

const app = express();
app.use(express.json());

// ➕ CREATE
app.post('/students', async (req, res) => {
  try {
    const student = await Student.create(req.body);
    res.status(201).json(student);
  } catch (err) {
    res.status(400).json({ error: err.message });      // validation errors
  }
});

// 🔍 READ ALL
app.get('/students', async (req, res) => {
  const students = await Student.find();
  res.json(students);
});

// 🔍 READ ONE
app.get('/students/:id', async (req, res) => {
  try {
    const student = await Student.findById(req.params.id);
    if (!student) return res.status(404).json({ error: 'Student not found' });
    res.json(student);
  } catch (err) {
    res.status(400).json({ error: 'Invalid ID format' });
  }
});

// ✏️ UPDATE
app.put('/students/:id', async (req, res) => {
  try {
    const student = await Student.findByIdAndUpdate(req.params.id, req.body, {
      new: true,
      runValidators: true,
    });
    if (!student) return res.status(404).json({ error: 'Student not found' });
    res.json(student);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

// 🗑️ DELETE
app.delete('/students/:id', async (req, res) => {
  try {
    const student = await Student.findByIdAndDelete(req.params.id);
    if (!student) return res.status(404).json({ error: 'Student not found' });
    res.json({ message: 'Deleted', id: student._id });
  } catch (err) {
    res.status(400).json({ error: 'Invalid ID format' });
  }
});

connectDB().then(() => {
  app.listen(3000, () => console.log('🚀 API on http://localhost:3000'));
});
```

### 🧪 Test with curl
```bash
# Create
curl -X POST http://localhost:3000/students \
  -H "Content-Type: application/json" \
  -d '{"name":"Riya","email":"riya@lpu.in","age":21,"cgpa":8.9}'

# Read all
curl http://localhost:3000/students

# Update (replace ID)
curl -X PUT http://localhost:3000/students/<id> \
  -H "Content-Type: application/json" -d '{"cgpa":9.5}'

# Delete
curl -X DELETE http://localhost:3000/students/<id>
```

| HTTP Method | Route | CRUD | Success Code |
|---|---|---|---|
| POST | `/students` | Create | `201` |
| GET | `/students` | Read all | `200` |
| GET | `/students/:id` | Read one | `200` / `404` |
| PUT | `/students/:id` | Update | `200` / `404` |
| DELETE | `/students/:id` | Delete | `200` / `404` |

---

## ✅ CHECKPOINT — Lecture 21 (Unit IV · L6)
- [ ] Use `create`, `find`, `findById`, `findByIdAndUpdate`, `findByIdAndDelete`
- [ ] Explain why `{ new: true }` and `runValidators: true` are needed on updates
- [ ] Return correct status codes: `201`, `400`, `404`
- [ ] Run the Express + Mongoose API and test all 5 routes

---

# 🏁 Unit IV Summary Map

```mermaid
mindmap
  root((Unit IV))
    MongoDB basics
      NoSQL document DB
      mongod and mongosh
      Database Collection Document Field
    Shell
      use and show dbs
      createCollection and drop
      insert find update delete
      query and update operators
    Node driver
      MongoClient
      connect and close
      CRUD with async await
    Mongoose
      Schema
      Validation
      Model
      CRUD methods
      Express REST API
```


---

# 📚 Unit V — Introduction to PostgreSQL
### Lectures 22 – 25 (4 × 50 minutes)

---

> **Unit Roadmap**

```mermaid
flowchart LR
    L1["🐘 Lecture 1
    Intro, Install,
    psql Basics"] --> L2["🏗️ Lecture 2
    CREATE TABLE,
    Data Types, INSERT"]
    L2 --> L3["🔍 Lecture 3
    SELECT, UPDATE,
    DELETE - CRUD"]
    L3 --> L4["🔗 Lecture 4
    Joins, Aggregates,
    Using Postgres from Node.js"]
```

---

# 🐘 LECTURE 22 (Unit V · L1): Introduction to PostgreSQL, Installation & `psql`

## 🎯 What You Will Know By the End
- What PostgreSQL is and why it is widely used
- How relational databases organize data
- How to install PostgreSQL and use the `psql` shell

## 1.1 What is PostgreSQL? 🤔

**PostgreSQL** (often "Postgres") is a powerful, open-source **relational database management system (RDBMS)**. It stores data in **tables** made of **rows** and **columns** and is queried with **SQL**.

| Trait | Meaning |
|---|---|
| 🏛️ Relational | Data in related tables |
| 🔒 ACID compliant | Reliable transactions (Atomicity, Consistency, Isolation, Durability) |
| 🆓 Open source | Free to use |
| 🧩 Extensible | Supports JSON, arrays, custom types |
| 📏 Standards-friendly | Strong SQL standard support |

## 1.2 Relational Model Refresher 📊

```mermaid
flowchart TD
    DB["🗄️ Database: college"] --> T1["📋 Table: students"]
    DB --> T2["📋 Table: courses"]
    T1 --> Row["Row = one record"]
    T1 --> Col["Column = one attribute"]
```

**Table: `students`**
| id *(PK)* | name | email | cgpa |
|---|---|---|---|
| 1 | Riya | riya@lpu.in | 8.90 |
| 2 | Aman | aman@lpu.in | 8.10 |

| Term | Meaning |
|---|---|
| **Table** | Collection of rows with the same structure |
| **Row (tuple)** | One record |
| **Column (attribute)** | One field with a fixed data type |
| **Primary Key** | Column(s) that uniquely identify each row |
| **Foreign Key** | Column that references another table's primary key |

### MongoDB vs PostgreSQL (link to Unit IV)
| | MongoDB | PostgreSQL |
|---|---|---|
| Unit of data | Document | Row |
| Group | Collection | Table |
| Schema | Flexible | Strict, defined upfront |
| Query language | JSON-style methods | SQL |

## 1.3 Installing PostgreSQL 🛠️

1. Download the installer for your OS from the official PostgreSQL website (Windows/macOS), or use a package manager on Linux.
2. During installation you will be asked for:
   - 🔑 a **password for the `postgres` superuser** — remember it!
   - 🔌 a **port** — default is **5432**
3. The installer typically includes **`psql`** (command line) and **pgAdmin** (graphical tool).
4. Verify:
```bash
psql --version
```
> 💡 Installer screens and package names differ by OS and version — follow the current instructions on the download page.

## 1.4 Connecting with `psql` 💻

```bash
psql -U postgres
# enter the password when prompted
```

```mermaid
sequenceDiagram
    participant U as You
    participant P as psql client
    participant S as PostgreSQL Server port 5432

    U->>P: psql -U postgres
    P->>S: authenticate with password
    S-->>P: connected
    U->>P: SELECT version
    P->>S: run SQL
    S-->>U: version info
```

### Essential `psql` Meta-Commands (start with backslash)
| Command | Purpose |
|---|---|
| `\l` | List databases |
| `\c dbname` | Connect to a database |
| `\dt` | List tables in current database |
| `\d tablename` | Describe a table |
| `\du` | List users/roles |
| `\?` | Help for psql commands |
| `\q` | Quit |

### 🧪 Create Your First Database
```sql
CREATE DATABASE college;
\l                 -- college is listed
\c college         -- switch to it
```
> ⚠️ SQL statements end with a **semicolon `;`**. Meta-commands (`\l`) do **not**.

```sql
SELECT version();          -- shows the PostgreSQL version
SELECT 2 + 3 AS result;    -- returns 5
```

---

## ✅ CHECKPOINT — Lecture 22 (Unit V · L1)
- [ ] Define RDBMS, table, row, column, primary key, foreign key
- [ ] Install PostgreSQL and verify with `psql --version`
- [ ] Log in with `psql -U postgres`
- [ ] Create a database `college` and connect with `\c college`

---

# 🏗️ LECTURE 23 (Unit V · L2): Basic SQL — `CREATE TABLE`, Data Types, Constraints & `INSERT`

## 🎯 What You Will Know By the End
- Core PostgreSQL data types
- How to create tables with constraints
- How to insert data
- How to alter and drop tables

## 2.1 Common Data Types 🔤

| Category | Type | Example |
|---|---|---|
| Integer | `INTEGER`, `SERIAL` (auto-increment) | `21` |
| Decimal | `NUMERIC(p,s)` | `NUMERIC(4,2)` → `8.95` |
| Text | `VARCHAR(n)`, `TEXT` | `'Riya'` |
| Boolean | `BOOLEAN` | `TRUE` / `FALSE` |
| Date/time | `DATE`, `TIMESTAMP` | `'2026-07-15'` |
| JSON | `JSON`, `JSONB` | `'{"a":1}'` |

> 📌 In SQL, **text and dates use single quotes** `'...'`. Double quotes are for identifiers.

## 2.2 Creating a Table 🧱

```sql
CREATE TABLE students (
  id          SERIAL PRIMARY KEY,
  name        VARCHAR(50)  NOT NULL,
  email       VARCHAR(100) UNIQUE NOT NULL,
  age         INTEGER CHECK (age >= 16),
  cgpa        NUMERIC(4,2) DEFAULT 0,
  city        VARCHAR(50),
  enrolled_on DATE DEFAULT CURRENT_DATE
);
```

```mermaid
flowchart TD
    T["📋 students"] --> A["id - SERIAL PRIMARY KEY"]
    T --> B["name - VARCHAR NOT NULL"]
    T --> C["email - VARCHAR UNIQUE"]
    T --> D["age - INTEGER CHECK"]
    T --> E["cgpa - NUMERIC DEFAULT 0"]
    T --> F["enrolled_on - DATE DEFAULT today"]
```

### Constraints
| Constraint | Rule |
|---|---|
| `PRIMARY KEY` | Unique and not null; identifies each row |
| `NOT NULL` | Value is required |
| `UNIQUE` | No duplicates allowed |
| `DEFAULT x` | Value used when none is given |
| `CHECK (cond)` | Value must satisfy a condition |
| `REFERENCES t(col)` | Foreign key to another table |

Verify:
```sql
\dt
\d students
```

## 2.3 Inserting Data ➕

```sql
-- One row
INSERT INTO students (name, email, age, cgpa, city)
VALUES ('Riya', 'riya@lpu.in', 21, 8.90, 'Jalandhar');

-- Many rows
INSERT INTO students (name, email, age, cgpa, city) VALUES
  ('Aman',   'aman@lpu.in',   22, 8.10, 'Ludhiana'),
  ('Simran', 'simran@lpu.in', 20, 9.30, 'Jalandhar'),
  ('Karan',  'karan@lpu.in',  23, 6.80, 'Amritsar');

-- Get the generated row back
INSERT INTO students (name, email, age)
VALUES ('Neha', 'neha@lpu.in', 21)
RETURNING id, name;
```
`id` is skipped because `SERIAL` generates it automatically. `RETURNING` is a handy PostgreSQL feature.

### Constraint Violations (what students will see)
```sql
INSERT INTO students (name, email, age) VALUES ('X', 'riya@lpu.in', 21);
-- ERROR: duplicate key value violates unique constraint

INSERT INTO students (name, email, age) VALUES ('Y', 'y@lpu.in', 10);
-- ERROR: new row violates check constraint
```

## 2.4 Altering and Dropping Tables 🔧

```sql
ALTER TABLE students ADD COLUMN phone VARCHAR(15);
ALTER TABLE students DROP COLUMN phone;
ALTER TABLE students RENAME COLUMN city TO hometown;

DROP TABLE students;               -- ⚠️ deletes table and all data
DROP TABLE IF EXISTS students;     -- no error if it doesn't exist
```

---

## ✅ CHECKPOINT — Lecture 23 (Unit V · L2)
- [ ] Create a table with `PRIMARY KEY`, `NOT NULL`, `UNIQUE`, `DEFAULT`, `CHECK`
- [ ] Insert one row and then multiple rows
- [ ] Use `RETURNING` on an insert
- [ ] Trigger and explain a unique-constraint error
- [ ] Add a column using `ALTER TABLE`

---

# 🔍 LECTURE 24 (Unit V · L3): CRUD — `SELECT`, `UPDATE`, `DELETE`

## 🎯 What You Will Know By the End
- How to query data with `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`
- How to modify rows with `UPDATE` and remove them with `DELETE`
- Why `WHERE` is critical in `UPDATE` / `DELETE`

```mermaid
flowchart LR
    C["➕ Create
    INSERT"] --- R["🔍 Read
    SELECT"] --- U["✏️ Update
    UPDATE"] --- D["🗑️ Delete
    DELETE"]
```

*(Sample data from Lecture 2 is assumed: Riya, Aman, Simran, Karan, Neha.)*

## 3.1 Read — `SELECT` 🔍

```sql
SELECT * FROM students;                          -- all columns, all rows
SELECT name, cgpa FROM students;                 -- chosen columns
SELECT name AS student_name FROM students;       -- alias
SELECT DISTINCT city FROM students;              -- unique values only
```

### Filtering with `WHERE`
```sql
SELECT * FROM students WHERE city = 'Jalandhar';
SELECT * FROM students WHERE cgpa > 8;
SELECT * FROM students WHERE cgpa BETWEEN 8 AND 9;
SELECT * FROM students WHERE city IN ('Jalandhar', 'Amritsar');
SELECT * FROM students WHERE name LIKE 'S%';         -- starts with S
SELECT * FROM students WHERE city = 'Jalandhar' AND cgpa > 9;
SELECT * FROM students WHERE age < 21 OR cgpa < 7;
SELECT * FROM students WHERE cgpa IS NULL;           -- use IS NULL, not = NULL
```

| Operator | Meaning |
|---|---|
| `=` `<>` | equal, not equal |
| `>` `<` `>=` `<=` | comparisons |
| `AND` `OR` `NOT` | logical |
| `BETWEEN a AND b` | inclusive range |
| `IN (...)` | matches any in list |
| `LIKE` | pattern: `%` = any chars, `_` = one char |
| `IS NULL` | missing value check |

### Sorting and Limiting
```sql
SELECT name, cgpa FROM students ORDER BY cgpa DESC;           -- highest first
SELECT name, cgpa FROM students ORDER BY cgpa DESC LIMIT 3;   -- top 3
SELECT * FROM students ORDER BY id LIMIT 2 OFFSET 2;          -- pagination
```

### Order of writing a query
```mermaid
flowchart LR
    A["SELECT"] --> B["FROM"] --> C["WHERE"] --> D["ORDER BY"] --> E["LIMIT"]
```

## 3.2 Update ✏️

```sql
UPDATE students SET cgpa = 9.10 WHERE name = 'Riya';

UPDATE students SET city = 'Phagwara', age = age + 1 WHERE id = 2;

UPDATE students SET cgpa = cgpa + 0.2 WHERE city = 'Jalandhar' RETURNING name, cgpa;
```

## 3.3 Delete 🗑️

```sql
DELETE FROM students WHERE name = 'Karan';
DELETE FROM students WHERE cgpa < 5;
```

> 🚨 **The most dangerous mistake in SQL:**
> ```sql
> UPDATE students SET cgpa = 0;      -- no WHERE: changes EVERY row
> DELETE FROM students;              -- no WHERE: deletes EVERY row
> ```
> **Tip:** write the `WHERE` first, or run a `SELECT` with the same `WHERE` before updating or deleting.

### `DELETE` vs `TRUNCATE` vs `DROP`
| Command | What it removes | Table remains? |
|---|---|---|
| `DELETE FROM t WHERE ...` | Selected rows | ✅ |
| `TRUNCATE TABLE t` | All rows (fast) | ✅ |
| `DROP TABLE t` | Rows **and** the table | ❌ |

## 3.4 Transactions — All or Nothing 🔒 (short intro)

```sql
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;          -- or ROLLBACK; to undo both
```
```mermaid
flowchart LR
    B["BEGIN"] --> S1["Step 1"] --> S2["Step 2"] --> Ok{"All OK?"}
    Ok -->|"Yes"| C["COMMIT - save"]
    Ok -->|"No"| R["ROLLBACK - undo"]
```

---

## ✅ CHECKPOINT — Lecture 24 (Unit V · L3)
- [ ] Write `SELECT` queries with `WHERE`, `AND/OR`, `IN`, `LIKE`
- [ ] Sort results with `ORDER BY` and limit with `LIMIT`
- [ ] Update a single row safely with `WHERE`
- [ ] Delete a row and explain `DELETE` vs `TRUNCATE` vs `DROP`
- [ ] Explain what `COMMIT` and `ROLLBACK` do

---

# 🔗 LECTURE 25 (Unit V · L4): Aggregates, Joins & Using PostgreSQL from Node.js

## 🎯 What You Will Know By the End
- How to summarize data with `COUNT`, `AVG`, `GROUP BY`
- How foreign keys and `JOIN` connect tables
- How to run SQL CRUD from Node.js with the `pg` library

## 4.1 Aggregate Functions and `GROUP BY` 📈

```sql
SELECT COUNT(*)  FROM students;                -- number of rows
SELECT AVG(cgpa) FROM students;                -- average
SELECT MAX(cgpa), MIN(cgpa) FROM students;

-- Per-group summary
SELECT city, COUNT(*) AS total, ROUND(AVG(cgpa), 2) AS avg_cgpa
FROM students
GROUP BY city
ORDER BY total DESC;

-- Filter groups with HAVING (WHERE filters rows, HAVING filters groups)
SELECT city, COUNT(*) FROM students GROUP BY city HAVING COUNT(*) > 1;
```

| Function | Result |
|---|---|
| `COUNT(*)` | Number of rows |
| `SUM(col)` | Total |
| `AVG(col)` | Average |
| `MIN` / `MAX` | Smallest / largest |

## 4.2 Relationships and Joins 🤝

Create a second table linked by a **foreign key**:

```sql
CREATE TABLE courses (
  id    SERIAL PRIMARY KEY,
  title VARCHAR(100) NOT NULL
);

CREATE TABLE enrollments (
  id         SERIAL PRIMARY KEY,
  student_id INTEGER REFERENCES students(id) ON DELETE CASCADE,
  course_id  INTEGER REFERENCES courses(id)  ON DELETE CASCADE
);

INSERT INTO courses (title) VALUES ('Advanced Web Programming'), ('Compiler Design');
INSERT INTO enrollments (student_id, course_id) VALUES (1, 1), (1, 2), (2, 1);
```

```mermaid
erDiagram
    STUDENTS ||--o{ ENROLLMENTS : has
    COURSES  ||--o{ ENROLLMENTS : has
    STUDENTS {
        int id PK
        string name
        string email
    }
    COURSES {
        int id PK
        string title
    }
    ENROLLMENTS {
        int id PK
        int student_id FK
        int course_id FK
    }
```

### `INNER JOIN` — only matching rows
```sql
SELECT s.name, c.title
FROM enrollments e
JOIN students s ON s.id = e.student_id
JOIN courses  c ON c.id = e.course_id
ORDER BY s.name;
```
| name | title |
|---|---|
| Aman | Advanced Web Programming |
| Riya | Advanced Web Programming |
| Riya | Compiler Design |

### `LEFT JOIN` — keep all left rows, even without a match
```sql
SELECT s.name, COUNT(e.id) AS courses_taken
FROM students s
LEFT JOIN enrollments e ON e.student_id = s.id
GROUP BY s.name;
```
Students with **no enrollments** still appear with `0`.

```mermaid
flowchart LR
    A["INNER JOIN
    only matches"] --- B["LEFT JOIN
    all left rows
    plus matches"]
```

## 4.3 Using PostgreSQL from Node.js (`pg`) 🟩🐘

```bash
mkdir pg-demo && cd pg-demo
npm init -y
npm install pg express
```

### Connection Pool
```javascript
// db.js
const { Pool } = require('pg');

const pool = new Pool({
  host: 'localhost',
  port: 5432,
  user: 'postgres',
  password: 'your_password',      // later: move to an environment variable
  database: 'college',
});

module.exports = pool;
```

> 🔐 **Never hard-code passwords in code you push to GitHub.** Use environment variables (covered in Unit VI).

### 🧪 CRUD with `pool.query`
```javascript
const pool = require('./db');

async function main() {
  // ➕ CREATE
  const created = await pool.query(
    'INSERT INTO students (name, email, age, cgpa) VALUES ($1, $2, $3, $4) RETURNING *',
    ['Isha', 'isha@lpu.in', 20, 8.7]
  );
  console.log('Created:', created.rows[0]);

  // 🔍 READ
  const all = await pool.query('SELECT * FROM students ORDER BY id');
  console.log('All:', all.rows);

  const good = await pool.query('SELECT name, cgpa FROM students WHERE cgpa > $1', [8]);
  console.log('Above 8:', good.rows);

  // ✏️ UPDATE
  const upd = await pool.query(
    'UPDATE students SET cgpa = $1 WHERE email = $2 RETURNING *',
    [9.0, 'isha@lpu.in']
  );
  console.log('Updated:', upd.rows[0]);

  // 🗑️ DELETE
  const del = await pool.query('DELETE FROM students WHERE email = $1', ['isha@lpu.in']);
  console.log('Deleted rows:', del.rowCount);

  await pool.end();
}

main().catch(console.error);
```

### ⚠️ Parameterized Queries Prevent SQL Injection
```javascript
// ❌ DANGEROUS - string concatenation
pool.query(`SELECT * FROM students WHERE name = '${userInput}'`);

// ✅ SAFE - placeholders $1, $2 ...
pool.query('SELECT * FROM students WHERE name = $1', [userInput]);
```
```mermaid
flowchart LR
    Bad["❌ Concatenated SQL
    user input becomes code"] --> Hack["💥 SQL Injection"]
    Good["✅ Parameterized query
    input stays data"] --> Safe["🛡️ Safe"]
```

### 🧪 Mini Express Route
```javascript
const express = require('express');
const pool = require('./db');
const app = express();
app.use(express.json());

app.get('/students', async (req, res) => {
  const { rows } = await pool.query('SELECT * FROM students ORDER BY id');
  res.json(rows);
});

app.post('/students', async (req, res) => {
  try {
    const { name, email, age, cgpa } = req.body;
    const { rows } = await pool.query(
      'INSERT INTO students (name, email, age, cgpa) VALUES ($1,$2,$3,$4) RETURNING *',
      [name, email, age, cgpa]
    );
    res.status(201).json(rows[0]);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

app.listen(3000, () => console.log('Running on http://localhost:3000'));
```

### 📊 Unit IV vs Unit V — Same Task, Two Databases
| Task | MongoDB / Mongoose | PostgreSQL / pg |
|---|---|---|
| Create | `Student.create({...})` | `INSERT INTO students ... VALUES ($1..)` |
| Read | `Student.find({cgpa: {$gt: 8}})` | `SELECT * FROM students WHERE cgpa > $1` |
| Update | `Student.findByIdAndUpdate(...)` | `UPDATE students SET ... WHERE id = $1` |
| Delete | `Student.findByIdAndDelete(id)` | `DELETE FROM students WHERE id = $1` |

---

## ✅ CHECKPOINT — Lecture 25 (Unit V · L4)
- [ ] Use `COUNT`, `AVG` with `GROUP BY` (and `HAVING`)
- [ ] Create two tables linked by a foreign key
- [ ] Write an `INNER JOIN` and a `LEFT JOIN`
- [ ] Run CRUD from Node.js using `pg` with `$1, $2` placeholders
- [ ] Explain SQL injection and how parameterized queries stop it

---

# 🏁 Unit V Summary Map

```mermaid
mindmap
  root((Unit V: PostgreSQL))
    Basics
      RDBMS concepts
      Install
      psql commands
    DDL
      CREATE TABLE
      Data types
      Constraints
      ALTER and DROP
    CRUD
      INSERT
      SELECT with WHERE
      UPDATE
      DELETE
    Beyond basics
      Aggregates and GROUP BY
      Joins
      Transactions
      pg with Node.js
```


---

# 📚 Unit VI — Testing & Deployment
### Lectures 26 – 29 (4 × 50 minutes)

---

> **Unit Roadmap**

```mermaid
flowchart LR
    L1["🧪 Lecture 1
    Testing REST APIs
    Manually"] --> L2["🤖 Lecture 2
    Automated API Tests
    Jest and Supertest"]
    L2 --> L3["🐙 Lecture 3
    Deployment with
    GitHub and CI"]
    L3 --> L4["☁️ Lecture 4
    Third-Party Hosting
    and Rendering"]
```

> 📝 **Scope note for the instructor:** "Third party rendering" is interpreted here as deploying and serving the application through third-party platforms (e.g., Render, Railway, Vercel) and third-party services (e.g., MongoDB Atlas). Platform dashboards and free-tier rules change often, so the steps below stay at the concept level — verify exact button names before class.

---

# 🧪 LECTURE 26 (Unit VI · L1): Testing REST APIs (Manual Testing)

## 🎯 What You Will Know By the End
- What a REST API is and what "testing" it means
- How to test endpoints using the browser, `curl`, and Postman / Thunder Client
- What to check in every response: status, headers, body

## 1.1 Quick Recap — REST API 🔁

A **REST API** exposes resources through URLs and uses HTTP methods for actions.

| Method | Action | Example | Typical Success |
|---|---|---|---|
| `GET` | Read | `GET /api/students` | `200` |
| `POST` | Create | `POST /api/students` | `201` |
| `PUT` / `PATCH` | Update | `PUT /api/students/1` | `200` |
| `DELETE` | Delete | `DELETE /api/students/1` | `200` / `204` |

## 1.2 Why Test? 🤔

```mermaid
flowchart TD
    Code["✍️ Write API code"] --> Q{"Tested?"}
    Q -->|"No"| Bug["🐞 Bugs found by users
    in production"]
    Q -->|"Yes"| Safe["✅ Bugs found early,
    safe to change code"]
```

### What to verify for each endpoint
| Check | Example |
|---|---|
| ✅ Correct **status code** | `201` after create, `404` for missing item |
| ✅ Correct **response body** | JSON has expected fields |
| ✅ Correct **headers** | `Content-Type: application/json` |
| ✅ **Error handling** | invalid input gives `400`, not a crash |
| ✅ **Edge cases** | empty body, wrong ID, duplicate data |

## 1.3 A Small API to Test 🛠️

We use an **in-memory** API so no database is needed.

```bash
mkdir api-testing && cd api-testing
npm init -y
npm install express
```

**`app.js`**
```javascript
const express = require('express');
const app = express();
app.use(express.json());

let students = [
  { id: 1, name: 'Riya', cgpa: 8.9 },
  { id: 2, name: 'Aman', cgpa: 8.1 },
];
let nextId = 3;

// READ ALL
app.get('/api/students', (req, res) => {
  res.status(200).json(students);
});

// READ ONE
app.get('/api/students/:id', (req, res) => {
  const student = students.find((s) => s.id === Number(req.params.id));
  if (!student) return res.status(404).json({ error: 'Student not found' });
  res.json(student);
});

// CREATE
app.post('/api/students', (req, res) => {
  const { name, cgpa } = req.body;
  if (!name || typeof cgpa !== 'number') {
    return res.status(400).json({ error: 'name and numeric cgpa are required' });
  }
  const student = { id: nextId++, name, cgpa };
  students.push(student);
  res.status(201).json(student);
});

// DELETE
app.delete('/api/students/:id', (req, res) => {
  const index = students.findIndex((s) => s.id === Number(req.params.id));
  if (index === -1) return res.status(404).json({ error: 'Student not found' });
  students.splice(index, 1);
  res.status(204).send();
});

module.exports = app;     // 👈 exported so tests can use it (important for Lecture 2)
```

**`server.js`**
```javascript
const app = require('./app');
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`🚀 Server on port ${PORT}`));
```
Run: `node server.js`

> 💡 **Design tip:** keep `app` (routes) and `listen` (starting the server) in **separate files**. Tests can then import `app` without opening a real port.

## 1.4 Manual Testing Tools 🧰

```mermaid
flowchart LR
    T1["🌐 Browser
    GET only"] --- T2["⌨️ curl
    command line"] --- T3["📮 Postman /
    Thunder Client
    visual tools"]
```

### a) Browser — only `GET`
Open `http://localhost:3000/api/students`.

### b) `curl` — command line
```bash
# GET all
curl http://localhost:3000/api/students

# GET one, showing status and headers (-i)
curl -i http://localhost:3000/api/students/1

# POST (create)
curl -i -X POST http://localhost:3000/api/students \
  -H "Content-Type: application/json" \
  -d '{"name":"Simran","cgpa":9.3}'

# POST with invalid data -> expect 400
curl -i -X POST http://localhost:3000/api/students \
  -H "Content-Type: application/json" \
  -d '{"name":"NoCgpa"}'

# DELETE
curl -i -X DELETE http://localhost:3000/api/students/2
```

### c) Postman / Thunder Client (VS Code extension)
```mermaid
flowchart TD
    A["1. Pick method
    GET POST PUT DELETE"] --> B["2. Enter URL
    localhost:3000/api/students"]
    B --> C["3. For POST: Body, raw, JSON"]
    C --> D["4. Click Send"]
    D --> E["5. Inspect status,
    body and headers"]
```

### 🧪 Manual Test Table (students fill this in)
| # | Request | Expected Status | Expected Body |
|---|---|---|---|
| 1 | `GET /api/students` | 200 | array of 2 students |
| 2 | `GET /api/students/1` | 200 | Riya |
| 3 | `GET /api/students/99` | 404 | `{ error: ... }` |
| 4 | `POST` valid body | 201 | new student with `id` |
| 5 | `POST` missing `cgpa` | 400 | `{ error: ... }` |
| 6 | `DELETE /api/students/1` | 204 | empty |

> ⚠️ **Limitation of manual testing:** it is slow, repetitive and easy to forget. This motivates **automated tests** (Lecture 2).

---

## ✅ CHECKPOINT — Lecture 26 (Unit VI · L1)
- [ ] Explain what to verify in an API response (status, body, headers)
- [ ] Run the sample API and test `GET` in the browser
- [ ] Test `POST` and `DELETE` using `curl` or Postman/Thunder Client
- [ ] Complete the manual test table including the error cases

---

# 🤖 LECTURE 27 (Unit VI · L2): Automated API Testing with Jest & Supertest

## 🎯 What You Will Know By the End
- What automated testing is and why it matters
- How to write tests with **Jest** and call the API with **Supertest**
- How to run tests with `npm test` and read the results

## 2.1 The Idea 💡

Instead of typing `curl` commands by hand, **write code that tests your code**. Run it after every change in seconds.

```mermaid
flowchart LR
    T["🧪 Test file"] -->|"Supertest sends
    fake HTTP request"| App["🚏 Express app"]
    App -->|"response"| T
    T --> Assert{"expect statusCode
    equals 200 ?"}
    Assert -->|"Yes"| Pass["✅ PASS"]
    Assert -->|"No"| Fail["❌ FAIL"]
```

| Tool | Role |
|---|---|
| **Jest** | Test runner and assertion library (`describe`, `it`, `expect`) |
| **Supertest** | Sends HTTP requests directly to your Express `app` |

## 2.2 Setup 🛠️

```bash
npm install --save-dev jest supertest
```

**`package.json` — add the test script**
```json
{
  "scripts": {
    "start": "node server.js",
    "test": "jest"
  }
}
```
> Test files are auto-detected if named `*.test.js` or placed in a `__tests__` folder.

## 2.3 Anatomy of a Test 🔬

```javascript
describe('group name', () => {          // groups related tests
  it('does something', async () => {    // one test case
    // 1. Arrange - set up
    // 2. Act     - call the API
    // 3. Assert  - check the result
    expect(actual).toBe(expected);
  });
});
```

### Common Jest Matchers
| Matcher | Checks |
|---|---|
| `toBe(x)` | strict equality (numbers, strings) |
| `toEqual(obj)` | deep equality (objects, arrays) |
| `toHaveProperty('id')` | object has property |
| `toBeGreaterThan(n)` | numeric comparison |
| `toContain(x)` | array/string contains |
| `not.toBe(x)` | negation |

## 2.4 Writing the Tests 🧪

**`app.test.js`**
```javascript
const request = require('supertest');
const app = require('./app');

describe('GET /api/students', () => {
  it('returns 200 and an array of students', async () => {
    const res = await request(app).get('/api/students');

    expect(res.statusCode).toBe(200);
    expect(Array.isArray(res.body)).toBe(true);
    expect(res.body.length).toBeGreaterThan(0);
  });

  it('returns JSON content type', async () => {
    const res = await request(app).get('/api/students');
    expect(res.headers['content-type']).toMatch(/json/);
  });
});

describe('GET /api/students/:id', () => {
  it('returns the student when ID exists', async () => {
    const res = await request(app).get('/api/students/1');
    expect(res.statusCode).toBe(200);
    expect(res.body.name).toBe('Riya');
  });

  it('returns 404 when ID does not exist', async () => {
    const res = await request(app).get('/api/students/999');
    expect(res.statusCode).toBe(404);
    expect(res.body).toHaveProperty('error');
  });
});

describe('POST /api/students', () => {
  it('creates a student and returns 201', async () => {
    const res = await request(app)
      .post('/api/students')
      .send({ name: 'Simran', cgpa: 9.3 });

    expect(res.statusCode).toBe(201);
    expect(res.body).toHaveProperty('id');
    expect(res.body.name).toBe('Simran');
  });

  it('returns 400 when cgpa is missing', async () => {
    const res = await request(app)
      .post('/api/students')
      .send({ name: 'NoCgpa' });

    expect(res.statusCode).toBe(400);
  });
});

describe('DELETE /api/students/:id', () => {
  it('deletes an existing student with 204', async () => {
    const res = await request(app).delete('/api/students/2');
    expect(res.statusCode).toBe(204);
  });

  it('returns 404 for a missing student', async () => {
    const res = await request(app).delete('/api/students/999');
    expect(res.statusCode).toBe(404);
  });
});
```

## 2.5 Running the Tests ▶️

```bash
npm test
```
**Typical output:**
```
 PASS  ./app.test.js
  GET /api/students
    ✓ returns 200 and an array of students
    ✓ returns JSON content type
  GET /api/students/:id
    ✓ returns the student when ID exists
    ✓ returns 404 when ID does not exist
  POST /api/students
    ✓ creates a student and returns 201
    ✓ returns 400 when cgpa is missing
  DELETE /api/students/:id
    ✓ deletes an existing student with 204
    ✓ returns 404 for a missing student

Tests:       8 passed, 8 total
```

### 🔬 Deliberately Break It
Change `res.status(201)` to `res.status(200)` in `app.js` and re-run `npm test`:
```
✕ creates a student and returns 201
  Expected: 201
  Received: 200
```
> 🎯 **Teaching moment:** the test caught a bug in seconds — this is the safety net that makes refactoring safe.

### Testing Tips
```mermaid
mindmap
  root((Good API tests))
    Cover success paths
    Cover error paths
      400 bad input
      404 not found
    Independent tests
    Clear names
    Run on every change
```

> ⚠️ **Note:** our sample API keeps data in memory and tests share it, so test order matters (e.g., deleting ID `2`). With a real database, use a **separate test database** and reset data before each test (`beforeEach`).

---

## ✅ CHECKPOINT — Lecture 27 (Unit VI · L2)
- [ ] Install Jest and Supertest and add the `npm test` script
- [ ] Write a test for `GET` that checks status and body
- [ ] Write tests for `POST` success (`201`) and failure (`400`)
- [ ] Run `npm test`, break the code on purpose, and observe the failing test
- [ ] Explain why `app` and `listen` live in different files

---

# 🐙 LECTURE 28 (Unit VI · L3): Deployment with GitHub

## 🎯 What You Will Know By the End
- What deployment means and the general pipeline
- How to put a project on GitHub safely (`.gitignore`, no secrets)
- How to use environment variables
- How to run tests automatically with GitHub Actions (CI)

## 3.1 What is Deployment? 🌍

**Deployment** = making your application run on a server so that **anyone can reach it** via a public URL.

```mermaid
flowchart LR
    Dev["💻 Local machine
    localhost:3000"] --> Git["🐙 GitHub
    source code"] --> Host["☁️ Hosting platform
    builds and runs"] --> URL["🌐 Public URL"]
```

## 3.2 Git & GitHub Essentials 🐙

| Term | Meaning |
|---|---|
| **Git** | Version control tool on your computer |
| **GitHub** | Online hosting for Git repositories |
| **Repository (repo)** | Project folder tracked by Git |
| **Commit** | A saved snapshot of changes |
| **Branch** | Parallel line of development (`main`) |
| **Push / Pull** | Upload / download commits |

```mermaid
flowchart LR
    W["📁 Working folder"] -->|"git add"| S["📥 Staging"]
    S -->|"git commit"| L["🗃️ Local repo"]
    L -->|"git push"| R["🐙 GitHub remote"]
    R -->|"git pull"| W
```

## 3.3 Prepare the Project 🧰

### Step 1 — Use the `PORT` from the environment
Hosting platforms assign the port. Never hard-code it:
```javascript
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Server on port ${PORT}`));
```

### Step 2 — Add a `start` script
```json
"scripts": {
  "start": "node server.js",
  "test": "jest"
}
```

### Step 3 — Environment variables (never commit secrets)
```bash
npm install dotenv
```
**`.env`** *(local only — never pushed)*
```
PORT=3000
MONGO_URI=mongodb://127.0.0.1:27017/college
SESSION_SECRET=change-me
```
**Top of `server.js`**
```javascript
require('dotenv').config();
const uri = process.env.MONGO_URI;
```

### Step 4 — `.gitignore`
```
node_modules/
.env
```
```mermaid
flowchart TD
    Files["Project files"] --> Ign{"In .gitignore?"}
    Ign -->|"node_modules, .env"| Skip["🚫 Not pushed"]
    Ign -->|"source code, package.json"| Push["✅ Pushed to GitHub"]
```
> 🚨 **Never push `.env` or passwords.** Bots scan public repos for leaked keys within minutes. If a secret is ever pushed, **rotate (change) it** — deleting the file later is not enough.

## 3.4 Push to GitHub — Step by Step 🚀

1. Create a GitHub account and click **New repository** (name e.g. `student-api`; do not add README if you already have local code).
2. In your project folder:
```bash
git init
git add .
git commit -m "Initial commit: student API"
git branch -M main
git remote add origin https://github.com/<your-username>/student-api.git
git push -u origin main
```
3. Refresh the repo page — your code is online. ✅

> 🔑 GitHub **no longer accepts account passwords** for `git push`. Authenticate with a **Personal Access Token**, **SSH key**, or GitHub's browser/credential-manager login.

### Daily Workflow
```bash
git status
git add .
git commit -m "Add DELETE route"
git push
```

## 3.5 Continuous Integration with GitHub Actions ⚙️

**CI** = automatically run tests on every push. Create `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - run: npm ci
      - run: npm test
```

```mermaid
sequenceDiagram
    participant D as Developer
    participant G as GitHub
    participant A as Actions Runner

    D->>G: git push
    G->>A: Trigger CI workflow
    A->>A: checkout, install, npm test
    A-->>G: Report pass or fail
    G-->>D: Green tick or red cross
```
`npm ci` requires a committed `package-lock.json` (created automatically by `npm install`).

---

## ✅ CHECKPOINT — Lecture 28 (Unit VI · L3)
- [ ] Explain deployment in one sentence
- [ ] Use `process.env.PORT` and add a `start` script
- [ ] Create `.gitignore` excluding `node_modules` and `.env`
- [ ] Push a project to a new GitHub repository
- [ ] Add a GitHub Actions workflow and see tests run on push

---

# ☁️ LECTURE 29 (Unit VI · L4): Deploying with Third-Party Platforms & Services

## 🎯 What You Will Know By the End
- The categories of third-party platforms for hosting Node.js apps
- How to deploy an Express API from GitHub to a hosting platform
- How to use a cloud database (MongoDB Atlas) from a deployed app
- How to verify, debug and update a live deployment

## 4.1 Landscape of Third-Party Platforms 🗺️

```mermaid
flowchart TD
    P["Third-party platforms"] --> PaaS["🧱 PaaS - app hosting
    Render, Railway, Heroku, Fly.io"]
    P --> Serverless["⚡ Serverless / Frontend
    Vercel, Netlify"]
    P --> DBaaS["🗄️ Database as a Service
    MongoDB Atlas, Neon, Supabase"]
    P --> IaaS["🖥️ Raw servers - IaaS
    AWS EC2, Azure, DigitalOcean"]
```

| Type | You manage | Good for |
|---|---|---|
| **PaaS** | Only your code | Beginners, APIs, full Node servers |
| **Serverless** | Only functions | Frontends, Next.js, light APIs |
| **DBaaS** | Only your data | Cloud databases without installing anything |
| **IaaS** | OS, security, scaling | Full control, advanced users |

> 💡 Free tiers, limits and sleep-after-inactivity policies differ per provider and change often — check the provider's pricing page before choosing.

## 4.2 Why `localhost` Databases Won't Work in Production 🚫

```mermaid
flowchart LR
    App["☁️ Deployed app
    on a remote server"] -->|"mongodb://127.0.0.1"| X["❌ No MongoDB
    on that server"]
    App -->|"Atlas connection string"| OK["✅ Cloud MongoDB"]
```
The remote server has no copy of **your laptop's** database. Use a **cloud database** and give the app its connection string.

## 4.3 Step 1 — Create a Cloud Database (MongoDB Atlas) 🍃

1. Create a free Atlas account → create a **cluster**.
2. **Database Access:** create a database user (username + password).
3. **Network Access:** allow your host's IP — for learning you may allow all (`0.0.0.0/0`), but restrict this for real projects.
4. Click **Connect → Drivers** and copy the connection string:
```
mongodb+srv://<user>:<password>@cluster0.xxxxx.mongodb.net/college?retryWrites=true&w=majority
```
5. Put it in your local `.env` and test locally first:
```
MONGO_URI=mongodb+srv://myuser:mypassword@cluster0.xxxxx.mongodb.net/college
```
```javascript
await mongoose.connect(process.env.MONGO_URI);
```

## 4.4 Step 2 — Deploy the App (Render-style PaaS) 🚀

The flow is nearly identical across platforms (Render, Railway, etc.):

```mermaid
flowchart TD
    A["1. Push code to GitHub"] --> B["2. Sign in to platform
    with GitHub"]
    B --> C["3. New Web Service,
    pick your repo"]
    C --> D["4. Set Build Command
    npm install"]
    D --> E["5. Set Start Command
    npm start"]
    E --> F["6. Add Environment Variables
    MONGO_URI, SESSION_SECRET"]
    F --> G["7. Deploy"]
    G --> H["8. Public URL ready"]
```

### Settings Cheat Sheet
| Setting | Value |
|---|---|
| Runtime | Node |
| Build command | `npm install` |
| Start command | `npm start` (runs `node server.js`) |
| Environment variables | `MONGO_URI`, `SESSION_SECRET`, etc. (**not** from your `.env` file) |
| Branch | `main` |
| Port | Read `process.env.PORT` — do **not** hard-code |

> 🔑 `.env` is git-ignored, so the platform never sees it. You **must re-enter each variable** in the platform's Environment settings.

## 4.5 Step 3 — Verify the Live Deployment ✅

```bash
curl -i https://your-app-name.onrender.com/api/students
```
Add a simple **health-check route** — useful for platforms and monitoring:
```javascript
app.get('/health', (req, res) => res.status(200).json({ status: 'ok' }));
```

| Symptom | Likely cause | Fix |
|---|---|---|
| Build fails | Missing dependency in `package.json` | Run `npm install <pkg>` (saves it) and push |
| App crashes on start | Wrong start command or missing env var | Check logs; set variables |
| `EADDRINUSE` / port error | Hard-coded port | Use `process.env.PORT` |
| DB connection timeout | Atlas network access / wrong URI | Allow host IP; recheck user/password |
| Works locally, not live | Relied on `.env` or local files | Set platform env vars |
| First request is slow | Free tier app was asleep | Wait; it wakes up |

**Debugging:** open the platform's **Logs** tab — it shows the same `console.log` output you see locally.

## 4.6 Continuous Deployment — Push to Update 🔁

Most platforms **auto-redeploy** when you push to the connected branch.

```mermaid
sequenceDiagram
    participant D as Developer
    participant G as GitHub
    participant CI as GitHub Actions
    participant H as Hosting Platform

    D->>G: git push to main
    G->>CI: run tests
    CI-->>G: tests pass
    G->>H: webhook - new commit
    H->>H: build and restart
    H-->>D: new version live
```
> 🧠 **Best practice:** only deploy when tests pass — CI (Lecture 3) plus auto-deploy forms a basic **CI/CD pipeline**.

## 4.7 "Third-Party Rendering" — Serverless & Frontend Platforms ⚡

Some platforms (e.g., Vercel, Netlify) **render and serve** your web app from their global network rather than a long-running Node server. This is the typical choice for **Next.js** or static front-ends, while an Express API with sockets or sessions suits a PaaS server.

| Need | Prefer |
|---|---|
| Long-running Express API / Socket.IO | PaaS web service |
| Static site / Next.js frontend | Vercel / Netlify |
| Managed MongoDB | Atlas |
| Managed PostgreSQL | A hosted Postgres provider |

> ⚠️ Serverless functions are short-lived — in-memory sessions and persistent WebSocket connections **do not fit well** there.

---

## ✅ CHECKPOINT — Lecture 29 (Unit VI · L4)
- [ ] Name one platform each for PaaS, serverless and DBaaS
- [ ] Explain why a `localhost` database fails after deployment
- [ ] Create an Atlas database and connect to it via `MONGO_URI`
- [ ] Deploy the GitHub repo to a PaaS with correct build/start commands and env vars
- [ ] Verify the live URL with `curl` or Postman and read the logs

---

# 🏁 Unit VI Summary Map

```mermaid
mindmap
  root((Unit VI))
    Testing REST API
      Status body headers
      curl
      Postman and Thunder Client
      Jest
      Supertest
    Deployment with GitHub
      git add commit push
      gitignore
      env variables
      GitHub Actions CI
    Third-party platforms
      PaaS Render Railway
      Serverless Vercel
      Atlas cloud database
      Logs and health check
      Auto redeploy
```

### 🎓 Course Wrap-Up: The Full-Stack Journey

```mermaid
flowchart LR
    U1["Unit I
    Node core"] --> U2["Unit II
    HTTP and Express"] --> U3["Unit III
    Sockets and Middleware"] --> U4["Unit IV
    MongoDB and Mongoose"] --> U5["Unit V
    PostgreSQL"] --> U6["Unit VI
    Test and Deploy"]
```


---

# 📚 References

- **Text Book:** *Node JS Guidebook* — Dhruti Shah, BPB Publications
- **Reference:** *Modern Full-Stack React Projects: Build, Maintain, and Deploy Modern Web Apps Using MongoDB, Express, React, and Node.js* — Daniel Bugl, Packt Publishing
