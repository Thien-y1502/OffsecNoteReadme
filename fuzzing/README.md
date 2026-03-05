# Fuzzing — an overview (for vulnerability research)

Fuzzing is automated testing where you feed a program many inputs to discover crashes, hangs, or logic bugs.

## Three “levels” of fuzzing

- **Black-box**: no visibility into internals; fastest to start, weaker coverage.
- **Grey-box**: lightweight instrumentation gives feedback (coverage, edges).
- **White-box / symbolic**: heavier analysis; can explore deeper paths but costs more.

## A simple workflow that scales

1. Pick a target and define the **input format** (file, network message, API).
2. Build a **harness** (a small wrapper that makes the target easy to run).
3. Start a fuzz campaign with a small **seed corpus**.
4. Triage crashes: minimize inputs, deduplicate, identify root cause.
5. Turn the best crashes into reports or patches.

## What “good” looks like

- Reproducible crashes
- Short, minimized PoC inputs
- A clear stack trace / sanitizer report
- A path to fix (root cause and patch idea)

## Tools you’ll see often

- Coverage-guided fuzzers (e.g., AFL-style, libFuzzer-style)
- Sanitizers (ASAN/UBSAN/TSAN)
- Crash triage and dedup tooling

*(This repo keeps things conceptual. For hands-on commands, use a lab VM and official docs.)*
