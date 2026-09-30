---
name: security-pack
description: Master security orchestration skill for Lovable projects. Use this skill to coordinate the security-core, Supabase RLS, input validation, edge functions, rate limiting, audit logging, and launch checklist skills according to the needs of each project.
---

# Security Pack

## Purpose

Use this skill as the main security orchestration layer for Lovable projects.

This skill does not replace specialized security modules.

Its job is to decide which security modules should be applied, in which order, and how their findings should be combined.

---

# Available Security Modules

Use the following installed skills when relevant:

- security-core
- supabase-rls-and-auth
- server-input-validation
- edge-functions-and-webhooks
- rate-limiting-edge
- audit-logging-backend
- lovable-ship-checklist

---

# Default Workflow

When reviewing or building a project, apply the modules in this order when relevant:

1. security-core
2. supabase-rls-and-auth
3. server-input-validation
4. edge-functions-and-webhooks
5. rate-limiting-edge
6. audit-logging-backend
7. lovable-ship-checklist

Do not force a module when the project does not use the related technology or feature.

---

# Project Detection

Before applying the modules, identify:

- whether Supabase is used
- whether authentication exists
- whether the app has server functions or APIs
- whether webhooks exist
- whether rate limiting is necessary
- whether sensitive admin actions exist
- whether audit logs are needed
- whether the project is approaching production

Use only the modules that are relevant.

---

# Security Core Role

Use security-core as the main framework for:

- severity classification
- false-positive avoidance
- verified vs unverified findings
- production-readiness language
- prioritization
- secure-by-default principles

Specialized skills should provide technical depth.

Security Core should organize and classify their findings.

---

# Supabase Security

If Supabase is used, apply:

supabase-rls-and-auth

Review:

- RLS
- auth.uid()
- SELECT
- INSERT
- UPDATE
- DELETE
- anon
- authenticated
- service_role
- storage
- SECURITY DEFINER
- privilege escalation
- IDOR

---

# Input Validation

When the application accepts user-controlled data, apply:

server-input-validation

Review:

- server-side validation
- database constraints
- Zod or equivalent validation
- type validation
- IDs
- enums
- quantities
- uploaded files
- manipulated frontend values

---

# Edge Functions and Webhooks

When the project uses:

- server functions
- edge functions
- API endpoints
- webhooks
- external integrations

apply:

edge-functions-and-webhooks

Review:

- authentication
- authorization
- secrets
- error handling
- webhook verification
- idempotency
- replay protection
- sensitive operations

---

# Rate Limiting

When endpoints may be abused or repeatedly called, apply:

rate-limiting-edge

Especially review:

- authentication endpoints
- payment endpoints
- coupon endpoints
- AI endpoints
- expensive queries
- email sending
- public APIs
- server functions with meaningful resource cost

Do not invent arbitrary limits without product context.

---

# Audit Logging

When the project contains sensitive actions, apply:

audit-logging-backend

Consider logging:

- admin actions
- account changes
- authorization failures
- payment events
- important configuration changes

Never log secrets, passwords, tokens, or payment card data.

---

# Pre-Launch Review

Before production, apply:

lovable-ship-checklist

Use it together with security-core.

Do not declare the application safe for production based only on repository review.

Clearly list:

- code-level blockers
- external settings still requiring verification
- hardening recommendations
- operational risks

---

# Building New Features

When implementing a new feature:

1. identify which security modules apply
2. explain the security plan before major architectural changes
3. preserve existing security controls
4. apply validation and authorization server-side
5. test realistic bypass attempts
6. distinguish executed tests from code inspection
7. report any remaining unknowns

---

# Audit Mode

When asked to audit a project:

Use the specialized modules for technical analysis.

Then use security-core to produce the final report.

The report should separate:

- Critical
- High
- Medium
- Low
- Hardening
- Verified secure controls
- NOT VERIFIED
- Recommended next actions

---
# Dependency Vulnerabilities

When a dependency scanner reports a vulnerability, do not classify the application risk only from the upstream CVE severity.

Separate:

- dependency advisory severity
- actual exploitability in this application
- reachable attack path
- production exposure
- recommended remediation priority

Example:

A dependency may have a HIGH severity advisory, but if the vulnerable code path is not used or is only present during build time, classify the application risk separately.

Use labels such as:

- Dependency Advisory: High
- Application Exploitability: Low
- Action Priority: Update when practical

Do not present a dependency advisory severity as equivalent to confirmed application exploitability.

---

# Do Not

Do not:

- assume every module is relevant
- invent vulnerabilities
- invent arbitrary product limits
- weaken RLS for convenience
- expose service_role keys
- trust frontend authorization
- make destructive changes without approval
- declare production readiness without acknowledging unverified controls
