# WAF “Bypass” — a defender-minded checklist

A WAF is not a magic shield. It’s a filter sitting in front of your app, and attackers mostly “bypass” it by:
- finding unprotected routes or alternate parsers, or
- exploiting differences between what the WAF sees and what the app actually processes.

This note is written in a **defensive mindset**: how to test coverage and reduce parser gaps.

## What to verify about your WAF setup

1. **Coverage**
   - Are *all* routes behind the WAF? (APIs, uploads, admin, legacy paths)
   - Any alternate domains, ports, or direct origin access?
2. **Normalization**
   - Does the WAF normalize encodings the same way the app/framework does?
   - How does it handle unusual content types and multipart bodies?
3. **Rate limits**
   - Are suspicious bursts throttled?
   - Are limits enforced per account + per IP + per token where relevant?
4. **Logging & response**
   - Are blocks visible in logs with enough detail to investigate?
   - Is there alerting on repeated probes?

## Common “gap” patterns (what to look for)

- Different parsers: WAF parses one way, backend parses another (especially for JSON, multipart, and uncommon HTTP features).
- Alternate entry points: GraphQL, file upload endpoints, webhooks.
- Business logic paths that don’t look “attack-like” but are still exploitable (IDOR, races).

## Practical hardening

- Block direct access to origins (force all traffic through the WAF/CDN).
- Keep rulesets updated and add app-specific allowlists for high-risk endpoints.
- Add server-side validation anyway — WAF should be an extra layer, not the only layer.
