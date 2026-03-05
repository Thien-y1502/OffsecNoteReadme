# AI / LLM Pentest — practical notes (authorized only)

AI systems fail in different ways than classic web apps because they combine:
- instruction-following behavior,
- untrusted inputs (prompts, docs, web pages),
- and often “agency” (tools/plugins/actions).

## What to map first (threat model)

- Model + providers (LLM, embeddings, reranker)
- Data sources (RAG docs, web browsing, internal KB)
- Tools / actions (plugins, function calling, ticket creation, email, file access)
- Secrets in scope (API keys, tokens), and where they could leak
- Business impact: fraud, data leakage, policy violations, brand risk

## Common classes of issues

- **Prompt injection** (direct or indirect via documents/web content)
- **Data leakage** (sensitive context in outputs, logs, or traces)
- **Insecure tool use** (LLM can trigger actions it shouldn’t)
- **Output handling bugs** (LLM output flows into HTML, SQL, shell, etc.)
- **Denial of service** (resource-heavy prompts, tool loops)
- **Supply chain** (unsafe models, poisoned data, insecure pipelines)

## Testing approach (safe)

1. Start with “read-only” probes: can you make it reveal system prompts, hidden instructions, or sensitive context?
2. Try indirect injection via a document/web page the model will ingest.
3. Validate tool permissions: can it do actions outside the user’s intent?
4. Verify that downstream consumers treat LLM output as untrusted.

## Defenses that actually help

- Clear separation: instructions vs data (robust prompt templates)
- Allowlisted tools + least privilege + human approval for risky actions
- Output escaping/validation before passing to interpreters or browsers
- Monitoring for jailbreak patterns and anomalous tool usage
- Secure RAG: source allowlists, sandboxed retrieval, content filtering
