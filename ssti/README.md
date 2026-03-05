# SSTI — Server-Side Template Injection (testing notes)

SSTI occurs when user-controlled input is interpreted as **template code** on the server.  
If the template engine offers powerful objects/APIs, SSTI can sometimes lead to **server-side data access** or even **code execution**.

> ✅ In real assessments, keep PoCs non-destructive and stop once you can demonstrate server-side evaluation.

## What usually causes SSTI

- Rendering raw user input as a template
- “Convenience” helpers that compile template strings at runtime
- Misconfigured sandboxing or overly powerful template globals

## Detection workflow

1. Find reflection points where your input is used in server-side views:
   - email templates, PDF/HTML reports, previews, admin pages
2. Trigger **template evaluation** (not just reflection):
   - look for math evaluation, engine-specific error patterns, or unexpected output changes
3. Identify the engine (Jinja2 / Twig / Freemarker / Velocity / etc.)
4. Assess impact:
   - can you access server-side variables?
   - can you read configuration or environment?
   - is execution blocked by a sandbox?

## Reporting tips

- Show a minimal request + response diff proving server-side evaluation.
- Identify engine and where the render happens (controller/view).
- Document any sandbox boundaries that prevent escalation (still a finding).

## Defensive fixes

- Never compile templates from untrusted strings.
- Keep templates static; treat user input as **data only**.
- Use strict sandboxes and minimal template globals.
- Add security tests for template endpoints and render helpers.
