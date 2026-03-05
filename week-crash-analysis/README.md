# Week 4 — Crash analysis & exploitability (study notes)

Once you have a crash, your job is to answer:

1) **What happened?** (root cause)  
2) **Can an attacker control it?** (inputs, reachability)  
3) **What does it buy them?** (impact)

## Crash triage basics

- Reproduce reliably
- Get a high-signal report (symbols, sanitizer output if possible)
- Classify the bug (overflow, UAF, OOB read/write, etc.)
- Minimize and deduplicate

## Exploitability thinking (high level)

- Control: can you influence instruction pointer / function pointers / writes?
- Constraints: mitigations, sandboxing, privilege boundaries
- Reliability: can it be triggered consistently?

## Output

A strong crash report includes:
- steps to reproduce,
- the minimized crashing input,
- stack trace / debugger notes,
- and a severity rationale.
