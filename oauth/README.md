# OAuth 2.0 / OIDC — security testing notes

OAuth is authorization (“can this app access this resource?”).  
OIDC adds identity (“who is the user?”) on top of OAuth.

Most real bugs are **misbindings**: the wrong session/user/client gets associated with the right token.

## Flows you’ll see in practice

- Authorization Code (recommended)
- Authorization Code + PKCE (recommended for public clients)
- Client Credentials (service-to-service)

## Things to review first

- Registered redirect URIs (must be strict and exact)
- Use of `state` (CSRF protection) and `nonce` (OIDC replay protection)
- Token audience/issuer validation in resource servers
- Scope enforcement (server must enforce, not the client)

## Testing checklist (authorized)

- Redirect URI validation: no wildcards, no path tricks, strict matching
- `state` present, unpredictable, and bound to the user session
- OIDC `nonce` validated for ID Tokens
- Resource server rejects ID Tokens where Access Tokens are required
- Refresh token rotation and reuse detection (if refresh tokens exist)

## Defensive guidance

- PKCE by default, even when you “think” you don’t need it.
- Enforce exact redirect URI match against a stored allowlist.
- Strict token validation (iss/aud/azp), short lifetimes, rotation policies.
- Use modern extensions where available (PAR/JAR/JARM, DPoP/mTLS).
