# Modern Initial Access — defensive overview

This page summarizes common initial access vectors used in real intrusions, **from a defender’s perspective**.

> This is for awareness, detection, and hardening — not for running attacks.

## Common initial access vectors (high level)

- Phishing leading to credential theft
- Business email compromise and account takeover
- OAuth consent abuse (malicious apps gaining token scopes)
- Exposed remote services with weak auth (RDP/VPN gateways)
- Malicious browser extensions or compromised SaaS sessions
- Supply-chain style compromises (trusted software abused)

## What to monitor

- Identity events: impossible travel, suspicious consent grants, MFA fatigue patterns
- Email security: attachment/link detonation results, unusual sender domains
- Endpoint telemetry: new persistence, suspicious child processes, script execution
- Cloud logs: new app registrations, token anomalies, unusual API patterns

## Hardening checklist

- Strong MFA with phishing-resistant methods where possible
- Conditional access policies and risk-based auth
- Disable legacy auth, enforce least privilege for OAuth apps
- Reduce exposed services; VPN hardening; rate limit and alert
- Secure browsing and extension allowlists
- Regular patching + asset inventory + EDR coverage
