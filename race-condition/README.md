# Race Conditions (web/app) — testing notes

A race condition happens when correctness depends on timing.  
In security, this becomes a bug when concurrent requests let you bypass a rule that should only allow an action once.

## The classic patterns

- **TOCTOU**: “check” happens, then state changes before “use”.
- **Read–Modify–Write**: two threads read the same value, both write back, one update gets lost.
- **Duplicate execution**: “only once” actions (coupon, transfer, claim) run multiple times.

## Where to look

- Payments, refunds, wallet transfers
- Coupon redemption / inventory reservations
- Password reset / email change workflows
- Rate-limited actions (“send OTP”, “claim reward”)
- File uploads and object creation with uniqueness constraints

## Safe testing approach

- Use a controlled test account and small amounts (or test environment).
- Send concurrent requests (same payload) and compare outcomes.
- Look for:
  - duplicate records
  - balance mismatch
  - inconsistent status transitions

## What helps defenders

- Atomic DB operations (transactions, row locks, unique constraints).
- Idempotency keys for retries.
- Queueing/serialization for critical sections.
- Correct cache invalidation (avoid “check cache then write DB” races).
