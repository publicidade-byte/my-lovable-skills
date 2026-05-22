# Changelog

All notable changes to this collection of **Lovable skills** are documented here.

The project follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) loosely; semantic versioning applies to the catalog as a whole, not to individual skills.

## [0.4.0] — 2026-05-22

### Added — TanStack Router and Start

- `tanstack-start-server-routes` — file-based API routes + `createServerFn` for full-stack TanStack apps; webhooks, auth, runtime targets, error shape.
- `tanstack-router-data-loaders` — typed loaders with `ensureQueryData`, search-param Zod schemas, `pendingComponent`/`errorComponent`, auth `beforeLoad`, parallel sibling loaders.

### Added — pg_cron deep dives

- `pg-cron-scheduled-jobs` — extension setup, cron syntax, function wrappers, monitoring, advisory locks, idempotency, migration discipline.
- `pg-cron-with-pg-net-edge` — call Supabase Edge Functions from cron via `pg_net` with shared-secret auth and optional HMAC signing.
- `pg-cron-recipes` — copy-pasteable cookbook: soft-delete cleanup, trial expiration, materialized view refresh, queue dispatch, retry backoff, log trimming, weekly digests, heartbeat, PII anonymization.

### Changed

- `background-jobs-and-cron`: now serves as the entry-point overview; deep dives moved to the three pg_cron skills above.

## [0.3.0] — 2026-05-22

### Added — TanStack Query deep dives (Lovable's default data layer)

- `tanstack-mutations-and-invalidation`
- `tanstack-infinite-queries`
- `tanstack-prefetch-and-hydration`

### Added — Technical SEO

- `seo-ssr-and-prerendering`
- `seo-meta-tags-spa`
- `seo-structured-data`
- `seo-sitemap-generation`
- `seo-core-web-vitals`

### Added — Programmatic SEO

- `programmatic-seo-pages`
- `programmatic-seo-content-quality`

### Changed

- `tanstack-query-alternative`: rewritten as the **primary** TanStack playbook (was "alternative" framing). Now covers QueryClient defaults, key factories, joined Supabase fetchers, and links to the new deep-dive skills.
- `typed-api-hooks-forms`: reframed to acknowledge TanStack Query as Lovable's default; this skill now focuses on Zod + react-hook-form plus the SWR alternative.
- `seo-landing-page`: now serves as an entry-point hub linking to the six new SEO skills.

## [0.2.0] — 2026-05-22

### Added — backend skills

- `supabase-database-design`
- `postgres-triggers-and-functions`
- `supabase-auth-flows`
- `multi-tenant-backend`
- `server-input-validation`
- `api-error-handling`
- `background-jobs-and-cron`
- `audit-logging-backend`
- `soft-delete-and-archiving`
- `postgres-full-text-search`
- `rate-limiting-edge`

### Added — payment webhooks

- `stripe-payment-webhooks` (+ `examples.md`)
- `payment-webhook-idempotency`
- `payment-webhook-testing`
- `payment-failed-and-recovery`
- `stripe-one-time-payment-webhooks`

### Added — product, UI, ops

- `optimistic-updates`
- `dark-mode-and-theming`
- `i18n-multi-language`
- `feature-flags-and-toggles`
- `dashboard-charts-recharts`
- `lovable-prompting-playbook`

### Changed

- `multi-tenant-backend`: switched RLS to `security definer` helper to prevent recursion.
- `stripe-payment-webhooks` examples: use `constructEventAsync` and `createFetchHttpClient` (correct for Deno).
- `audit-logging-backend`: clarified that `auth.uid()` only resolves for PostgREST-initiated changes; explicit actor pattern for service-role writes.
- `postgres-triggers-and-functions`: added `on conflict do nothing` and Supabase dashboard note for `auth.users` trigger.
- `server-input-validation`: updated Zod import to `npm:zod@3` (modern Deno).
- `supabase-rls-and-auth`: added performance/recursion guidance referencing helper functions.
- `supabase-database-design`: added money (`bigint cents`) and time (`timestamptz`) conventions.
- `file-upload-storage`: added explicit size/MIME validation before upload.
- `email-and-notifications`: added react-email templating and SPF/DKIM/DMARC deliverability section.
- `realtime-and-subscriptions`: added reconnect/refetch pattern.
- `shadcn-patterns`: added Sonner toast pattern, navigation, theming pointer.
- `lovable-ship-checklist`: added billing, accessibility, observability, secrets sections.
- `seo-landing-page`: added SPA metadata note (React 19 title / Helmet / pre-render).
- `analytics-events`: added StrictMode double-fire guard.
- `edge-functions-and-webhooks`: explicit pairing with input validation and error handling.

## [0.1.0] — Initial drop

- `typed-api-hooks-forms` (+ `examples.md`)
- `tanstack-query-alternative`
- `supabase-rls-and-auth`
- `edge-functions-and-webhooks`
- `realtime-and-subscriptions`
- `file-upload-storage`
- `email-and-notifications`
- `migration-playbook`
- `shadcn-patterns`
- `error-states-and-empty-ui`
- `onboarding-copy`
- `accessibility-pass`
- `lovable-ship-checklist`
- `refactor-safe-diff`
- `performance-budget`
- `seo-landing-page`
- `analytics-events`
- `pricing-and-billing`
- `release-notes`
- `support-reply`
