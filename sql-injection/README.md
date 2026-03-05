# SQL Injection (SQLi) — testing notes

SQL injection happens when an application **builds SQL using untrusted input** without safe parameterization.  
In practice, SQLi is rarely about “fancy payloads” — it’s about **data flow**: *user input → query builder → database*.

> ✅ Use this only in **authorized** environments. Prefer non-destructive verification.

## What you’re looking for

- A request parameter (querystring, JSON body, header, cookie, GraphQL variable, filter/sort fields) that changes the SQL query structure.
- Different server behavior when the input is slightly altered (errors, timing, result count, permission bypass).

## Fast triage checklist

1. **Map the query surface**
   - Search / filter / sort parameters
   - Login / password reset / “check availability”
   - Export endpoints (CSV/PDF), admin dashboards
2. **Look for query construction hints**
   - Stack traces, verbose DB errors
   - Inconsistent escaping, odd quoting
   - “Advanced search” syntax features
3. **Verify safely**
   - Aim for **read-only** confirmation first (e.g., result set changes, predictable error changes).
   - If blind, verify with **timing** differences *within a safe threshold* and *rate-limit yourself*.

## Common variants you should remember

- **In-band**: error-based, union-style result merging (often noisy).
- **Blind**: boolean-based (true/false branches), time-based (response delays).
- **Out-of-band**: the DB makes a network callback (rare, environment-dependent).
- **Second-order**: input is stored, then later used in SQL somewhere else.
- **API-shaped SQLi**: JSON filters/sorts that translate to SQL, WebSocket messages, or “search DSLs”.

## What to capture for a solid report

- A single **repro request** (sanitized) + exact endpoint and parameter.
- Proof of impact (data exposure, auth bypass, write capability).
- DB tech hints (MySQL/Postgres/MSSQL/Oracle) if available.
- Logs / screenshots showing the behavior change.

## Defensive fixes (what you’d recommend)

- Use **parameterized queries** / prepared statements.
- Apply **allowlists** for sortable columns, operators, and filter fields.
- Use least-privilege DB accounts (separate read/write roles).
- Centralize input validation and add monitoring for anomaly patterns.
