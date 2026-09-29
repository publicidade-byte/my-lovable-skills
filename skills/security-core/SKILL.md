# Security Core

## Purpose

Use this skill as the default security standard for Lovable applications.

Always assume that frontend code and client input can be manipulated.

## Core Principles

- Never trust the client.
- Never expose private secrets.
- Authorization must be enforced server-side.
- Validate sensitive input server-side.
- Use least privilege.
- Protect sensitive endpoints against abuse.
- Review security before production.

## Supabase

When Supabase is used:

- Enable appropriate RLS policies.
- Review SELECT, INSERT, UPDATE and DELETE permissions.
- Never expose service_role keys in frontend code.
- Review Storage policies.
- Review SECURITY DEFINER functions.

## Authorization

Never rely only on frontend roles or hidden UI elements.

Administrative and sensitive permissions must be verified server-side.

## Security Review

Before completing a feature, check:

- Can User A access User B's data?
- Can IDs be changed manually?
- Can APIs be called directly?
- Can frontend values be manipulated?
- Are any secrets exposed?
- Are database permissions too broad?
