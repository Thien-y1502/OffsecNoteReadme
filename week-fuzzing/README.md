# Week 2 — Finding bugs with fuzzing (study notes)

This week is about understanding **how fuzzers discover real bugs**, and how to turn crashes into actionable findings.

## Topics

- Coverage-guided fuzzing concepts (edges, corpus, mutations)
- Harness design (what makes a target “fuzzable”)
- Sanitizers and crash signal quality
- Corpus minimization and deduplication

## Practical outcomes

- You can set up a simple fuzz target in a lab
- You can interpret crash reports and prioritize them
- You can produce a minimal input that reproduces the crash

## Mindset

Fuzzing feels slow until it doesn’t. The “win” is repeatable infrastructure: harness + seeds + triage.
