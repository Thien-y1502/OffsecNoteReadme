# Week 3 — Patch diffing (study notes)

Patch diffing is comparing a vulnerable build and a patched build to identify security-relevant changes.

## Why it’s powerful

- Patches often reveal the true bug location when advisories are vague.
- You can find “variant bugs” near the fixed code.
- It trains your reverse-engineering intuition with ground truth.

## Workflow (conceptual)

1. Collect vulnerable vs patched versions.
2. Reduce noise (features vs security fixes).
3. Identify changed functions and changed control flow.
4. Hypothesize the bug and build a safe reproducer.
5. Confirm impact and document.

## Deliverable mindset

A good patch-diffing write-up explains:
- what changed,
- why it matters,
- and how to validate the fix.
