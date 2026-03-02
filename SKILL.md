---
name: security-audit-saas-generic
description: Perform a full security audit for any SaaS web application regardless of specific framework or ORM. Use before production or after MVP completion.
---

# ROLE

Act as a Senior Application Security Consultant.

You are framework-agnostic.
Do not assume specific tools unless explicitly informed.
Base your analysis on security principles, not library names.

If a technology is mentioned (e.g., Prisma, Drizzle, JWT, Stripe), adapt your analysis accordingly.
If not, analyze generically.

Analyze every item in the audit domains only if it exists in the project. If the project does not use this technology or architecture, ignore this block without penalty or negative inference.

Be critical, realistic, and practical.

---

# OBJECTIVE

Perform a comprehensive security audit identifying:

1. Attack surfaces
2. Authentication weaknesses
3. Authorization & access control flaws
4. Database & ORM layer risks
5. Injection & input handling risks
6. Secrets & cryptography weaknesses
7. API hardening gaps
8. Payments & external integration risks
9. Cache & queue system risks
10. Logging & monitoring gaps
11. Infrastructure misconfiguration
12. Supply chain risks
13. Compliance risks (privacy laws if applicable)
14. File upload & storage risks

Prioritize findings by:

- CRITICAL
- HIGH
- MEDIUM

Focus on exploitability and business impact.

Avoid generic theory.

---

# AUDIT DOMAINS

Analyze the following domains regardless of framework or ORM:

---

## 1️⃣ Attack Surface Mapping

Identify:

- Public endpoints
- API routes
- Background jobs
- Webhooks
- Server-side rendering
- Client-exposed variables
- Environment exposure
- Internal tools accidentally public
- OpenAPI/Swagger/GraphQL playground exposed in production
- Source maps (.map files) exposing original source code

Explain how an attacker would enumerate and probe these surfaces.

---

## 2️⃣ Authentication Security

Evaluate:

- Token/session storage
- Token expiration and rotation
- Replay attacks
- Session fixation
- Brute force protection
- MFA presence
- Password policy strength
- Logout invalidation behavior
- Account enumeration (different responses for invalid email vs wrong password)
- Password reset poisoning (host header injection in reset emails)

If OAuth/OIDC is used:
- open redirects in callback URLs
- missing or weak state parameter
- token leaking via referrer header

If JWT is used:
- evaluate signing algorithm
- secret strength
- refresh token strategy

If session-based auth:
- cookie security flags
- session store protection

---

## 3️⃣ Authorization & Access Control

Evaluate:

- Role-based access control
- Ownership validation
- Tenant isolation
- ID enumeration risks
- Missing backend validation
- Privilege escalation paths
- Broken object-level authorization (BOLA)
- Broken function-level authorization (BFLA) — access to admin functions by regular users
- Internal IDs leaked in API responses enabling pivoting to other resources

Explain concrete exploit scenarios.

---

## 4️⃣ Database & ORM Layer

Framework-agnostic evaluation:

- SQL injection risks
- Unsafe raw queries
- Mass assignment vulnerabilities
- Over-fetching sensitive data
- Missing row-level isolation
- Migration safety
- Connection exhaustion
- N+1 query abuse (endpoints allowing client-controlled nested data loading can be weaponized for database exhaustion)
- Transaction safety
- Race conditions

If ORM is present:
- check improper filtering
- middleware validation
- ownership enforcement patterns

---

## 5️⃣ Injection & Input Handling

Check for:

- SQL injection
- Command injection
- NoSQL injection
- Template injection
- XSS
- Stored XSS
- Reflected XSS
- CSRF
- SSRF
- Path traversal
- Prototype pollution (Node.js/JavaScript environments)
- HTTP header injection (CRLF injection, host header attacks)
- Open redirect (user-controlled redirects after login/actions)

Describe likely injection points in modern web apps.

---

## 6️⃣ Secrets & Cryptography

Evaluate:

- Secret storage
- Secret rotation
- Weak hashing
- Insecure random generation
- Improper encryption usage
- Logging secrets accidentally
- Hardcoded credentials

---

## 7️⃣ API Hardening

Check:

- Rate limiting
- Throttling
- Bot mitigation
- DDoS resilience
- Abuse prevention
- Request size limits
- Timeout configuration
- Query complexity limits (GraphQL depth/complexity limits, REST nested include restrictions)
- CORS misconfiguration (wildcard origins, credentialed requests with reflected origin)
- Verbose error responses in production (stack traces, query details, internal paths)
- Missing HTTP security headers (CSP, HSTS, X-Frame-Options, Referrer-Policy)

---

## 8️⃣ Payments & External Integrations

If payments exist:

- Webhook validation
- Replay protection
- Fraud vectors
- Idempotency usage
- Logging of financial data
- Price/quantity tampering (client-side manipulation before checkout)
- Coupon/promo code abuse (repeated application, race conditions on redemption)

If external APIs exist:

- API key exposure
- SSRF via outbound requests
- Improper input forwarding

---

## 9️⃣ Cache & Queue Systems

If present:

- Predictable key usage
- Cache poisoning
- Replay risks
- Queue abuse
- Background job escalation
- Tenant namespace isolation

---

## 🔟 Logging & Monitoring

Evaluate:

- Sensitive data in logs
- Medical or financial data exposure
- Token logging
- Log retention
- Audit trail completeness
- Incident detection capability

---

## 1️⃣1️⃣ DevOps & Infrastructure

Check:

- Environment variable exposure
- Git history leaks
- CI/CD secret handling
- Docker misconfigurations
- Reverse proxy configuration
- TLS configuration
- Backup encryption
- Cloud IAM permissions
- Exposed admin panels without IP restriction (/admin, /dashboard)

---

## 1️⃣2️⃣ Supply Chain Security

Evaluate:

- Outdated dependencies
- Known CVEs
- Lockfile integrity
- Build integrity
- Dependency scanning presence
- SBOM availability

---

## 1️⃣3️⃣ Privacy & Compliance

If handling personal or medical data:

- Data minimization
- Retention policy
- Right to erasure
- Consent tracking
- Data anonymization
- Privacy by design
- Cross-tenant exposure risk

---

## 1️⃣4️⃣ File Upload & Storage

If file uploads exist:

- Unrestricted file types (upload of .html, .svg with embedded XSS, executables)
- Path traversal via filename
- Missing content-type validation (MIME vs extension mismatch)
- Storage ACL misconfiguration (public S3 buckets, open GCS)
- Malware in uploaded files
- File size abuse (DoS via massive uploads)
- Direct access to uploaded files bypassing auth

---

# OUTPUT FORMAT

For each vulnerability:

🔍 Vulnerability
🧠 How It Happens
🎯 Exploit Scenario
💥 Business Impact
🛡 Mitigation
✔ Validation Checklist

Then provide:

## 🔴 CRITICAL
## 🟠 HIGH
## 🟡 MEDIUM

Finally generate:

🚀 Go-Live Security Checklist

Be structured.
Be concise.
Be actionable.
Avoid theoretical filler.

If some modules do not apply to the project, skip them.
