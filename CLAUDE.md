# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A small Express API for managing users, backed by an in-memory store (no real database).

## Commands

- `npm run dev` — start the API with auto-reload on http://localhost:3000
- `npm test` — run the test suite (Node's built-in test runner + supertest)
- `npm run lint` — check code style with ESLint
- `node --test tests/users.test.js` — run a single test file

## Conventions

- Use `require`/`module.exports` (CommonJS), not ES module `import`/`export`.
- Each resource gets its own file under `routes/`, mounted in `server.js`.
- Route handlers talk to data only through `db/store.js`, never manipulate the `users` array directly.

## Architecture

- `server.js` is the entry point: builds the Express app, mounts route modules, and only calls `app.listen` when run directly (so tests can `require` the app without opening a port).
- `routes/` holds one file per resource (`users.js`, `health.js`); each exports an `express.Router()`.
- `db/store.js` is a tiny in-memory data layer (array + helper functions); state resets on every restart.
