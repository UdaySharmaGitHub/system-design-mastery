# Security Policy

## Supported Versions

Because `system-design-mastery` is a documentation and learning repository (no deployed service, no user data), security concerns are primarily about content integrity and contributor safety.

| Version / Branch | Supported |
|---|---|
| `main` | Yes — all fixes applied here |
| Archived branches | No |

---

## Reporting a Vulnerability

**Please do NOT open a public GitHub issue for security reports.**

If you discover a security concern — including but not limited to:

- Malicious or misleading content that could harm learners
- Exposed secrets or credentials accidentally committed to the repo
- A dependency in a CI workflow with a known CVE
- A phishing or typosquatting attempt targeting contributors

Please report it privately using one of these channels:

1. **GitHub Private Advisory** (preferred): [https://github.com/UdaySharmaGitHub/system-design-mastery/security/advisories/new](https://github.com/UdaySharmaGitHub/system-design-mastery/security/advisories/new)
2. **GitHub DM**: [@UdaySharmaGitHub](https://github.com/UdaySharmaGitHub)

---

## What to Include in a Report

To help us triage quickly, please include:

- **Description** — what the issue is and why it is a security concern
- **Affected content or file(s)** — path(s) or URL(s) in the repo
- **Reproduction steps** — how to verify the issue
- **Suggested fix** — if you have one

---

## Response SLA

| Stage | Target |
|---|---|
| Acknowledgement | Within **3 business days** |
| Initial triage | Within **7 days** |
| Fix or mitigation | Within **14 days** for high severity; **30 days** for moderate |

We will credit reporters by name (or handle) in the fix commit unless they request anonymity.

---

## Security Guidance for Contributors

When contributing to this repository:

- **Never commit secrets.** No API keys, tokens, passwords, or credentials — not even fake-looking ones used as examples. Use `<YOUR_API_KEY>` placeholders in documentation.
- **Treat CI workflows as security boundaries.** Any `uses:` action or `run:` command in `.github/workflows/` is executed code. Avoid pinning actions by mutable tags (e.g. `@main`); prefer commit SHAs.
- **No executable code with external network calls** in contributed examples unless clearly sandboxed and scoped.
- **No links to third-party sites that require authentication or harvest personal data.**
