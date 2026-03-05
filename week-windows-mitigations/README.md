# Week 6 — Windows mitigations (study notes)

Windows mitigations are layers that make exploitation harder or prevent it entirely.

## Key mitigations to understand

- DEP/NX
- ASLR (including high entropy ASLR)
- Stack cookies (/GS)
- CFG/XFG
- CET shadow stack (on supported systems)
- Heap integrity checks and allocator hardening

## What to be able to do

- Recognize which mitigation stopped an exploit attempt from crash evidence.
- Check which protections a binary opted into.
- Explain how defense-in-depth changes attacker requirements.

## Outcome

You can build a small matrix:
- bug class → required primitive → mitigations that block it → what an attacker would need next
