# JWT Security — testing notes

JWTs are designed for **integrity**, not secrecy. A JWT can be read by anyone who has it, unless you add separate encryption.

## How JWT works (quick mental model)

- Header: token type + algorithm
- Payload: claims (who, what, when)
- Signature: proves the token wasn’t modified

## What commonly goes wrong

- Weak or leaked signing secrets (HMAC)
- Confusing algorithms (treating a public key flow like a shared-secret flow)
- Accepting unsigned tokens or unexpected algorithms
- Trusting client-controlled headers for key selection (key confusion / key injection)
- Over-trusting claims without server-side validation (roles, scopes, user IDs)

## Testing checklist (authorized)

1. Confirm the service validates:
   - issuer (`iss`), audience (`aud`), expiration (`exp`), not-before (`nbf`)
2. Confirm algorithm handling:
   - server should enforce an allowlist of expected algorithms
3. Review key management:
   - proper rotation, unique key IDs, pinned key sources
4. Look for sensitive data inside the payload:
   - if it’s sensitive, JWT isn’t the right container

## Defensive guidance

- Strict validation (iss/aud/exp) and small clock skew.
- Don’t accept key material locations from untrusted headers unless pinned.
- Use strong secrets for HMAC; prefer asymmetric keys when appropriate.
- Consider token binding / sender-constrained tokens in high-risk apps.
