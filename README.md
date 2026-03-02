# Security Analysis — Claude Code Skill

A comprehensive security audit skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that performs full application security assessments on any SaaS web application, regardless of framework or ORM.

## What It Does

This skill turns Claude Code into a **Senior Application Security Consultant** that analyzes your codebase and identifies real, exploitable vulnerabilities — not generic theory.

It's designed to be run **before production deployment** or **after MVP completion** as a final security gate.

## Audit Coverage

The skill performs a structured audit across **13 security domains**:

| # | Domain | What It Checks |
|---|--------|----------------|
| 1 | **Attack Surface Mapping** | Public endpoints, API routes, webhooks, exposed env vars, internal tools |
| 2 | **Authentication Security** | Token/session handling, JWT config, brute force protection, MFA, logout |
| 3 | **Authorization & Access Control** | RBAC, BOLA, tenant isolation, privilege escalation, ID enumeration |
| 4 | **Database & ORM Layer** | SQL injection, mass assignment, race conditions, row-level isolation |
| 5 | **Injection & Input Handling** | XSS, CSRF, SSRF, command injection, path traversal, template injection |
| 6 | **Secrets & Cryptography** | Hardcoded creds, weak hashing, secret rotation, insecure randomness |
| 7 | **API Hardening** | Rate limiting, DDoS resilience, bot mitigation, request size limits |
| 8 | **Payments & Integrations** | Webhook validation, replay protection, API key exposure, fraud vectors |
| 9 | **Cache & Queue Systems** | Cache poisoning, replay risks, queue abuse, tenant namespace isolation |
| 10 | **Logging & Monitoring** | Sensitive data in logs, audit trails, incident detection capability |
| 11 | **DevOps & Infrastructure** | CI/CD secrets, Docker config, TLS, cloud IAM, git history leaks |
| 12 | **Supply Chain Security** | Outdated deps, known CVEs, lockfile integrity, SBOM availability |
| 13 | **Privacy & Compliance** | Data minimization, right to erasure, consent tracking, retention policy |

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
git clone https://github.com/danielbom/claude-skill-security-analysis.git \
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

## Example Use Cases

- Pre-launch security review for a SaaS MVP
- Audit a new feature branch before merging
- Periodic security health checks on an existing codebase
- Onboarding onto a new project to understand its security posture

## Requirements

- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) installed and configured

## License

MIT
