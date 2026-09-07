# Notes

## CLAUDE.md

I kept it to a one-line project description, the three commands I actually run (`dev`, `test`, `lint`), two conventions (CommonJS, and routes only touching data through `db/store.js`), and a short architecture note on how `server.js`, `routes/`, and `db/store.js` fit together.

I left out anything the code already makes obvious (e.g. exact route paths, the shape of the user object), one-off details like the sample data in `db/store.js`, and anything from `.env.example` — no secrets or config values belong in a file every session loads.

## Permission rules

- **Allow:** `Bash(npm test:*)` and `Bash(npm run lint:*)` — safe, read-only-ish commands I run constantly and don't want to approve every time.
- **Ask:** `Bash(git push:*)` — pushing is fine to do often, but I want a chance to glance at what's being pushed first.
- **Deny:** `Read(./.env)` and `Bash(git push --force:*)` — without the `.env` deny rule, Claude could read real secrets into context and potentially leak them in output or logs. Without the force-push deny rule, Claude could overwrite remote history and destroy other people's commits with no way to undo it.

## Verification

- `/memory` shows `CLAUDE.md` loaded from the project root.
- `/permissions` shows the allow/ask/deny rules from `.claude/settings.json`.
- Asking "How do I run the tests here?" answers with `npm test` straight from the file, with no extra explanation needed.
