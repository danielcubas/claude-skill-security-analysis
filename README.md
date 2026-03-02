# Security Analysis — Claude Code Skill

A comprehensive security audit skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that performs full application security assessments on any SaaS web application, regardless of framework or ORM.

## What It Does

This skill turns Claude Code into a **Senior Application Security Consultant** that analyzes your codebase and identifies real, exploitable vulnerabilities — not generic theory.

It's designed to be run **before production deployment** or **after MVP completion** as a final security gate.

## Audit Coverage

The skill performs a structured audit across **14 security domains**:

| # | Domain | What It Checks |
|---|--------|----------------|
| 1 | **Attack Surface Mapping** | Public endpoints, API routes, webhooks, exposed env vars, internal tools, OpenAPI/Swagger/GraphQL playground exposure, source maps |
| 2 | **Authentication Security** | Token/session handling, JWT config, brute force protection, MFA, logout, account enumeration, password reset poisoning, OAuth/OIDC misconfigs |
| 3 | **Authorization & Access Control** | RBAC, BOLA, BFLA, tenant isolation, privilege escalation, ID enumeration, leaked internal IDs |
| 4 | **Database & ORM Layer** | SQL injection, mass assignment, race conditions, row-level isolation, N+1 query abuse, connection exhaustion |
| 5 | **Injection & Input Handling** | XSS, CSRF, SSRF, command injection, path traversal, template injection, prototype pollution, HTTP header injection, open redirects |
| 6 | **Secrets & Cryptography** | Hardcoded creds, weak hashing, secret rotation, insecure randomness |
| 7 | **API Hardening** | Rate limiting, DDoS resilience, bot mitigation, request size limits, CORS misconfiguration, query complexity limits, HTTP security headers, verbose errors |
| 8 | **Payments & Integrations** | Webhook validation, replay protection, API key exposure, fraud vectors, price/quantity tampering, coupon abuse |
| 9 | **Cache & Queue Systems** | Cache poisoning, replay risks, queue abuse, tenant namespace isolation |
| 10 | **Logging & Monitoring** | Sensitive data in logs, audit trails, incident detection capability |
| 11 | **DevOps & Infrastructure** | CI/CD secrets, Docker config, TLS, cloud IAM, git history leaks, exposed admin panels |
| 12 | **Supply Chain Security** | Outdated deps, known CVEs, lockfile integrity, SBOM availability |
| 13 | **Privacy & Compliance** | Data minimization, right to erasure, consent tracking, retention policy |
| 14 | **File Upload & Storage** | Unrestricted file types, path traversal via filename, MIME validation, storage ACL misconfiguration, malware, file size abuse |

## Key Design Principles

- **Framework-agnostic** — Works with any stack (Next.js, Django, Rails, Express, Laravel, etc.)
- **Adaptive** — If you use specific tools (Prisma, Stripe, JWT), it adapts its analysis accordingly
- **Practical** — Focuses on exploitability and business impact, not theoretical risks
- **Selective** — Only audits domains that exist in your project; skips irrelevant ones

## Output Format

Each finding includes:

- **Vulnerability** — What the issue is
- **How It Happens** — Root cause explanation
- **Exploit Scenario** — Concrete attack path
- **Business Impact** — What's at stake
- **Mitigation** — How to fix it
- **Validation Checklist** — How to verify the fix

Findings are prioritized as **CRITICAL**, **HIGH**, or **MEDIUM**, and the audit concludes with a **Go-Live Security Checklist**.

## Installation

### Option 1: Clone into Claude Code skills directory

```bash
git clone https://github.com/danielcubas/claude-skill-security-analysis.git \
  ~/.claude/skills/security-analysis
```

### Option 2: Manual setup

1. Create the skill directory:
   ```bash
   mkdir -p ~/.claude/skills/security-analysis
   ```
2. Copy `SKILL.md` into that directory.

## Usage

Inside any project directory with Claude Code running:

```
/security-analysis
```

Claude will scan your codebase and produce a structured security audit report.

## How It Works

1. You run `/security-analysis` inside your project directory
2. Claude reads your codebase — routes, models, configs, environment files, dependencies, etc.
3. Each of the 14 audit domains is evaluated against what actually exists in your project
4. Domains that don't apply (e.g., no payments, no queue system) are automatically skipped
5. A structured report is generated with prioritized findings and a go-live checklist

## Limitations

- **Static analysis only** — This skill analyzes source code and configuration. It does not perform dynamic testing (DAST), runtime fuzzing, or network-level scanning.
- **Not a replacement for professional pentesting** — Use this as a complement to, not a substitute for, dedicated SAST/DAST tools and manual penetration testing.
- **Scope depends on file access** — The quality of the audit depends on which files Claude can read in your project. Ensure relevant source files are accessible.

## Language Support

This skill is framework-agnostic and works with any language or stack, including but not limited to:

TypeScript/JavaScript, Python, Go, Ruby, PHP, Java, Kotlin, Swift, Rust, C#

It adapts to whatever frameworks, ORMs, and libraries your project uses.

## Example Use Cases

- Pre-launch security review for a SaaS MVP
- Audit a new feature branch before merging
- Periodic security health checks on an existing codebase
- Onboarding onto a new project to understand its security posture

## Requirements

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed and configured

## Contributing

Contributions are welcome! Feel free to:

- Open an [issue](https://github.com/danielcubas/claude-skill-security-analysis/issues) to report bugs or suggest new audit domains
- Submit a pull request with improvements to `SKILL.md` or `README.md`
- Share feedback on false positives or missing coverage areas

## License

MIT
