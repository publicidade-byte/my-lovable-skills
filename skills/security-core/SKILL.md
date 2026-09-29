---
name: security-core
description: Universal security standard and audit framework for Lovable applications. Use when creating, modifying, reviewing, or preparing an app for production, especially for authentication, authorization, Supabase, APIs, secrets, payments, admin features, webhooks, and abuse prevention.
---

# Security Core

## Purpose

Use this skill as the default security standard for Lovable applications.

The goal is to help build and review applications using a secure-by-default approach without treating every hardening opportunity as a critical vulnerability.

Always assume that frontend code and client input can be inspected and manipulated.

Do not make destructive or architectural changes automatically during an audit unless explicitly asked.

---

# Core Principles

Always follow these principles:

1. Never trust the client for security decisions.
2. Never expose private secrets to the frontend.
3. Authorization must be enforced using trusted server-side or database-side controls.
4. Authentication and authorization are different concerns.
5. Validate untrusted input appropriately.
6. Apply least privilege.
7. Protect sensitive operations against abuse.
8. Prefer secure defaults.
9. Avoid inventing arbitrary security requirements without product context.
10. Clearly distinguish vulnerabilities from hardening recommendations.

---

# Security Severity Classification

Every security finding must be classified using one of these levels.

## CRITICAL

Use only when exploitation could realistically cause severe impact such as:

- service role key or private secret exposed publicly
- missing access control that exposes sensitive data broadly
- unauthenticated access to highly sensitive operations
- payment manipulation that can directly create fraudulent successful payments
- unrestricted admin access
- remote code execution
- arbitrary database access

Critical findings should normally be fixed immediately.

---

## HIGH

Use when exploitation could lead to:

- one user accessing or modifying another user's data
- privilege escalation
- broken authorization
- insecure admin operations
- webhook forgery with meaningful impact
- trusting client-controlled price, permissions or payment state
- exposed sensitive personal information
- bypass of server-side validation in sensitive workflows

High findings should normally be resolved before production.

---

## MEDIUM

Use for meaningful weaknesses that increase attack surface or abuse risk, such as:

- missing rate limiting on abuse-prone operations
- incomplete server-side input validation
- insufficient upload restrictions
- excessive permissions
- weak security logging
- unsafe session handling patterns
- missing idempotency in operations where duplicate execution matters

Medium findings should be evaluated before production.

---

## LOW

Use for minor security improvements with limited direct exploitation impact.

Examples:

- additional defensive validation
- security headers with limited impact in the current architecture
- improved error handling
- additional logging
- minor hardening improvements

---

## HARDENING

Use when the recommendation is not a vulnerability but would improve resilience.

Examples:

- introducing stricter length limits
- additional monitoring
- optional rate limits
- stronger password UX
- additional audit logs
- stricter operational quotas

Do not present hardening recommendations as security vulnerabilities.

---

# Required Audit Output

When performing a security review, present findings in this order:

1. Executive Summary
2. Critical Findings
3. High Findings
4. Medium Findings
5. Low Findings
6. Hardening Recommendations
7. What Is Already Secure
8. Recommended Next Actions
9. Assumptions and Unknowns
Explicitly list anything that could not be verified, such as:

- Supabase dashboard settings
- authentication provider settings
- environment secrets not visible in the repository
- production infrastructure
- external payment provider configuration
- firewall or platform-level rate limits
- third-party service settings

Do not mark these areas as secure unless they were actually verified.

For each finding explain:

- What was found
- Where it was found
- Why it matters
- Realistic attack scenario
- Recommended fix
- Whether the fix is required before production

Use clear language suitable for a non-security specialist.

---

# Action Priority

Every finding must also receive one action category:

## FIX NOW

Use for Critical findings and urgent High findings.

## FIX BEFORE PRODUCTION

Use for High and important Medium findings.

## REVIEW BEFORE PRODUCTION

Use for Medium findings requiring product or architectural decisions.

## OPTIONAL HARDENING

Use for Low or Hardening recommendations.

Do not recommend unnecessary work simply because it is technically possible.

---

# Frontend Security

Assume that the user can:

- inspect JavaScript
- inspect network requests
- modify API requests
- change localStorage
- change URL parameters
- modify hidden fields
- call APIs directly
- automate requests

Therefore:

- hiding a button is not authorization
- disabling an input is not authorization
- protecting a route visually is not authorization
- frontend validation alone is not security validation

Frontend validation is useful for user experience but should not be the only protection for sensitive operations.

---

# Secrets

Never expose private secrets in frontend code.

Never expose:

- Supabase service role keys
- database passwords
- payment provider secrets
- webhook secrets
- private API keys
- private tokens
- backend credentials

Public client keys may be exposed only when they are explicitly designed to be public.

When reviewing secrets, distinguish between:

- public client configuration
- private secrets

Do not incorrectly classify public Supabase client keys as leaked secrets.

---

# Authentication

When authentication exists:

- verify that authentication is handled by a trusted identity provider
- review session handling
- review password recovery
- review email verification when appropriate
- review account recovery flows
- review authentication abuse protections

Do not assume frontend password rules are the authoritative security control.

When Supabase Auth is used, also consider the authentication settings configured in Supabase itself.

Do not invent password complexity requirements without checking the application's authentication provider and risk profile.

---

# Authorization

Every sensitive operation must answer:

WHO is requesting this?

WHAT resource are they trying to access?

ARE they allowed to perform this action?

Never rely only on frontend state such as:

role === "admin"

Administrative permissions must be verified using trusted data.

Always test horizontal privilege escalation:

User A attempts to access User B's resource.

Always test vertical privilege escalation:

Normal user attempts to perform administrator actions.

---

# Supabase Security

When Supabase is used:

Review:

- Row Level Security
- SELECT policies
- INSERT policies
- UPDATE policies
- DELETE policies
- Storage policies
- Edge Functions
- privileged database functions
- service role usage

RLS should normally be enabled for application tables exposed through the Supabase Data API.

For user-owned resources, ownership should usually be enforced using the authenticated user identity.

Do not assume that direct access to Supabase APIs is itself a vulnerability.

Direct client access is expected in many Supabase architectures.

The real security boundary is:

- authentication
- RLS
- database policies
- secure backend logic

---

# Supabase Service Role

The Supabase service role key is highly privileged.

Never expose it in:

- React code
- Vite public variables
- browser bundles
- localStorage
- public repositories

Service role operations must run in trusted server-side environments.

---

# IDOR

Always test for Insecure Direct Object Reference.

Example:

User A owns:

order_id = 123

Attempt to access:

order_id = 124

If order 124 belongs to User B, User A must not gain access.

Test this for:

- profiles
- orders
- tickets
- notes
- bookings
- invoices
- files
- messages
- subscriptions
- admin resources

If RLS or trusted server-side authorization correctly blocks access, classify IDOR as mitigated.

---

# Input Validation

Treat external input as untrusted.

Validate where appropriate:

- IDs
- UUIDs
- strings
- numbers
- quantities
- emails
- URLs
- dates
- enum values
- uploaded files
- payment-related values

Use server-side or database-side validation for security-sensitive constraints.

Frontend validation is primarily for user experience.

Do not classify missing string length limits as a vulnerability by default.

First determine whether unrestricted input creates a realistic security, availability, cost, or resource-exhaustion risk in the specific application.

If the impact is primarily operational or related to product limits, classify it as Hardening or Needs Review rather than Medium or High.

Only classify it as a security vulnerability when a realistic abuse scenario and meaningful impact are demonstrated.
---

# API and Edge Function Security

For every sensitive endpoint or Edge Function ask:

1. Does it require authentication?
2. Does it verify authorization?
3. Is input validated?
4. Can another user's resource ID be supplied?
5. Can the operation be repeated?
6. Does duplicate execution matter?
7. Should rate limiting exist?
8. Are secrets handled safely?
9. Does it expose unnecessary information?

---

# Rate Limiting and Abuse Prevention

Consider rate limiting or quotas for operations such as:

- authentication attempts
- password recovery
- account creation
- coupon validation
- payments
- AI requests
- expensive queries
- email sending
- file processing
- public APIs

Do not invent arbitrary limits such as:

"maximum 500 records per user"

unless product context supports that limit.

Instead recommend:

"Define an appropriate quota based on expected product usage."

---

# File Upload Security

When file uploads exist, review:

- MIME type
- extension
- file size
- access permissions
- storage visibility
- executable content
- ownership
- public versus private buckets

Do not trust the extension alone.

Private files must not accidentally become public.

---

# Payment Security

When payments exist:

Never trust client-controlled:

- price
- discount
- total
- payment status
- order ownership

Prefer:

Client sends:
product_id

Trusted backend determines:
price

Payment success must be verified through trusted payment provider mechanisms.

Do not mark an order as paid only because the frontend reports success.

---

# Webhook Security

When webhooks exist:

Review:

- provider signature verification
- webhook secret storage
- replay protection
- idempotency
- event validation
- duplicate processing
- trusted source verification

Not every webhook implementation uses the same verification mechanism.

Do not invent provider-specific requirements without knowing the provider.

---

# Admin Security

Admin interfaces require special protection.

Review:

- server-side authorization
- role validation
- sensitive operations
- audit logging
- privilege boundaries

A hidden admin route is not protected simply because users do not know the URL.

---

# Logging

Security logging should help identify important actions without leaking sensitive information.

Consider logging:

- admin actions
- authorization failures
- authentication failures
- payment events
- security-sensitive account changes

Never log:

- passwords
- card numbers
- authentication secrets
- private API keys
- private tokens

---

# Avoid False Positives

Do not label something a vulnerability only because:

- a public API key exists
- the frontend calls Supabase directly
- frontend validation exists
- getSession() is used for harmless UI behavior
- a string has no arbitrary maximum length
- an endpoint does not have rate limiting even though abuse impact is negligible

Evaluate realistic exploitability and impact.

If context is insufficient, say:

"Needs review"

instead of claiming a vulnerability.

---

# Security Review Questions

Before considering a feature secure, ask:

Can User A access User B's data?

Can a normal user become an admin?

Can IDs be modified to access another resource?

Can sensitive frontend values be manipulated?

Can APIs be called directly?

If called directly, are permissions still enforced?

Can sensitive operations be repeated?

Can payment state be forged?

Are private secrets exposed?

Are database permissions too broad?

Can files be accessed by unauthorized users?

Can webhook events be forged or replayed?

---

# Audit Safety

When auditing an existing project:

Do not automatically rewrite working authentication.

Do not automatically change RLS policies.

Do not automatically alter database schemas.

Do not automatically introduce quotas.

Do not automatically change payment logic.

Do not make destructive changes unless explicitly asked.

First report:

- findings
- severity
- recommended fix
- risk of the fix

Then wait for approval before applying major security changes.

---

# Rule When Security Is Uncertain

When uncertain:

Do not invent certainty.

State:

- what is known
- what is assumed
- what should be verified

Prefer a safer architecture when reasonable, but explain tradeoffs.
