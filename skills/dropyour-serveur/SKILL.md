---
name: dropyour-serveur
description: Write server-side code (server.js) for a graduated Dropyour app: queryable store, clock, secrets, signed-in visitors, files, realtime. Use when the app needs data shared between visitors, a scheduled job, or an outgoing API call.
---

# Le code serveur d'une app Dropyour

Disponible sur une app **graduée** (palier 4). Si l'app ne l'est pas encore, `dropyour_graduate`.

Before generating what I'll ask you, STRICTLY apply these rules (this is SERVER code for a GRADUATED Dropyour app, tier 4):

1. Write `server.js` at the ROOT of the .zip (or several files under `server/`, with `server/index.js` as the entry). Plain ES modules, no build step, no npm install, no bundler.

2. THE CONTRACT — this is the whole surface, and there is nothing else:

Your server code runs as `server.js` at the root of the .zip (or under `server/` for several files).
It exports a default object with two optional handlers:

  export default {
    async fetch(app) { /* return a Response, or null to serve the static page */ },
    async scheduled(app) { /* runs when the clock rings */ },
  };

`app` is the capability. It is the ONLY thing your code receives — there is no ambient access to
the network, the platform, or another app. What is not listed below does not exist.

- **app.request** — the incoming `Request`, untouched. In `scheduled` it is synthetic.
- **app.dropId** — your app's id — use it to build your own URLs instead of guessing them.
- **app.state** — a single JSON blob with optimistic versioning. Good for settings and small shared state.
    - `app.state.get` — read `{ data, version }`.
    - `app.state.put` — write; pass the version you read to detect a conflict instead of overwriting silently.
- **app.records** — the queryable store: many documents in named collections. This is where real app data lives.
    - `app.records.list` — list a collection, with an optional `where` on ONE top-level field (`eq`/`lt`/`gt`), and a cursor.
    - `app.records.get` — read one document by id.
    - `app.records.stats` — counts per collection, without downloading the documents.
    - `app.records.put` — create or replace one document.
    - `app.records.remove` — delete one document. Deleting an absent one is not an error.
- **app.schedule** — your app's clock. Your `scheduled` handler re-arms it itself — there is no cron syntax.
    - `app.schedule.next` — ask to be woken once, between 5 minutes and 30 days from now. Replaces any pending wake-up.
    - `app.schedule.cancel` — drop the pending wake-up.
- **app.log** — write a line your agent can read back later with `dropyour_logs`. Levels: info, warn, error.
- **app.visitor** — who is signed in, or `null`. `id` is stable for this app only; `email` only if they agreed to share it.
- **app.files** — your app's file space. Serve files from YOUR routes — there is no public bucket URL.
    - `app.files.put` — write or replace a file.
    - `app.files.get` — read a file back, with its content type.
    - `app.files.list` — list files under an optional prefix, with the total size used.
    - `app.files.delete` — remove a file. Removing an absent one is not an error.
- **app.realtime** — push a message to every browser currently connected to your app, and count them.

3. `fetch(app)` returns a `Response`, or `null` to let the static page be served as usual. Route by reading `new URL(app.request.url).pathname`. Never assume a path prefix you did not create.

4. Outgoing calls are CLOSED BY DEFAULT and opened by DECLARATION: the hosts you may reach are derived from the code you publish, so write each URL literally instead of assembling it from pieces. A secret never lives in your code — it is injected at the network boundary, so call the API with no key and the platform adds it.

5. Data belongs server-side. Use `app.records` for anything shared between visitors or queried; `app.state` for a small settings blob. Do NOT reimplement storage in localStorage and then try to sync it.

6. Failures are named, never silent: every write returns a result you must read — a version conflict is a normal answer, not a crash. Call `app.log` on the paths you will want to debug; an agent reads those lines back.

7. At the end, give me each file separately with its path, and remind me to publish with the MCP tool dropyour_replace. Same stable URL, data preserved.

## Ce que le contrat garantit, et qu'il faut savoir avant d'écrire

Your server code runs as `server.js` at the root of the .zip (or under `server/` for several files).
It exports a default object with two optional handlers:

  export default {
    async fetch(app) { /* return a Response, or null to serve the static page */ },
    async scheduled(app) { /* runs when the clock rings */ },
  };

`app` is the capability. It is the ONLY thing your code receives — there is no ambient access to
the network, the platform, or another app. What is not listed below does not exist.

- **app.request** — the incoming `Request`, untouched. In `scheduled` it is synthetic.
- **app.dropId** — your app's id — use it to build your own URLs instead of guessing them.
- **app.state** — a single JSON blob with optimistic versioning. Good for settings and small shared state.
    - `app.state.get` — read `{ data, version }`.
    - `app.state.put` — write; pass the version you read to detect a conflict instead of overwriting silently.
- **app.records** — the queryable store: many documents in named collections. This is where real app data lives.
    - `app.records.list` — list a collection, with an optional `where` on ONE top-level field (`eq`/`lt`/`gt`), and a cursor.
    - `app.records.get` — read one document by id.
    - `app.records.stats` — counts per collection, without downloading the documents.
    - `app.records.put` — create or replace one document.
    - `app.records.remove` — delete one document. Deleting an absent one is not an error.
- **app.schedule** — your app's clock. Your `scheduled` handler re-arms it itself — there is no cron syntax.
    - `app.schedule.next` — ask to be woken once, between 5 minutes and 30 days from now. Replaces any pending wake-up.
    - `app.schedule.cancel` — drop the pending wake-up.
- **app.log** — write a line your agent can read back later with `dropyour_logs`. Levels: info, warn, error.
- **app.visitor** — who is signed in, or `null`. `id` is stable for this app only; `email` only if they agreed to share it.
- **app.files** — your app's file space. Serve files from YOUR routes — there is no public bucket URL.
    - `app.files.put` — write or replace a file.
    - `app.files.get` — read a file back, with its content type.
    - `app.files.list` — list files under an optional prefix, with the total size used.
    - `app.files.delete` — remove a file. Removing an absent one is not an error.
- **app.realtime** — push a message to every browser currently connected to your app, and count them.
