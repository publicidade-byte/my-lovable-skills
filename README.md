# Lovable Skills — A Production-Ready Skill Library for Lovable.dev

> **Learn to vibe code better by saving costs** — [VibeMastery](https://vibemastery.io/)

> **57 open-source [Lovable](https://lovable.dev) skills** — TanStack Query, TanStack Start server routes, Supabase RLS, Stripe webhooks, pg_cron deep dives, technical SEO, programmatic SEO, multi-tenant SaaS, dark mode, i18n, charts, and the full launch checklist. Import in one click; no Settings credit cost.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE) [![Skills: 57](https://img.shields.io/badge/skills-57-success.svg)](skills/) [![Lovable](https://img.shields.io/badge/built%20for-Lovable.dev-7c3aed.svg)](https://lovable.dev) [![Compatible: Claude, Cursor](https://img.shields.io/badge/compatible-Claude%20%7C%20Cursor-orange.svg)](https://docs.lovable.dev/features/skills)

If you searched **lovable skills**, **lovable workspace skills**, **lovable.dev skills**, **lovable agent skills**, **lovable tanstack query**, **lovable tanstack start**, **lovable pg_cron**, **lovable SEO**, or **how to add skills in Lovable**, this is the most complete catalog on GitHub.

---

## What this is

A curated collection of **[Lovable skills](https://docs.lovable.dev/features/skills)** — short markdown playbooks Lovable loads on demand to handle recurring work the same way every time. Each skill is opinionated, tested against real Supabase + Stripe + TanStack Query + shadcn projects, and small enough to live happily next to your knowledge base.

| Use **knowledge** for | Use **Lovable skills** for |
|----------------------|----------------------------|
| Brand, tone, global folder layout — always on | Auth, RLS, webhooks, ship checklist — loaded only when relevant |
| Rules that apply to every message | Task-specific playbooks |

You can keep dozens of skills in one workspace without bloating context — Lovable only loads the ones that match your prompt.

---

## Starter packs

### Every Lovable + Supabase project (6)

1. [`tanstack-query-alternative`](skills/tanstack-query-alternative/) — Lovable's default data layer
2. [`supabase-rls-and-auth`](skills/supabase-rls-and-auth/) — row level security from day one
3. [`error-states-and-empty-ui`](skills/error-states-and-empty-ui/) — loading, empty, error every list
4. [`shadcn-patterns`](skills/shadcn-patterns/) — dialogs, sheets, tables, toasts
5. [`typed-api-hooks-forms`](skills/typed-api-hooks-forms/) — Zod + react-hook-form (forms half)
6. [`lovable-ship-checklist`](skills/lovable-ship-checklist/) — pre-launch gate

### Backend / SaaS (8)

`supabase-database-design` → `supabase-auth-flows` → `supabase-rls-and-auth` → `multi-tenant-backend` → `server-input-validation` → `api-error-handling` → `edge-functions-and-webhooks` → `rate-limiting-edge`

### Payments (6)

`pricing-and-billing` → `stripe-payment-webhooks` → `payment-webhook-idempotency` → `payment-webhook-testing` → `payment-failed-and-recovery` → `stripe-one-time-payment-webhooks` *(only for one-time products)*

### Marketing site / SEO (6)

`seo-landing-page` → `seo-meta-tags-spa` → `seo-ssr-and-prerendering` → `seo-structured-data` → `seo-sitemap-generation` → `seo-core-web-vitals`

### Programmatic SEO (4)

`programmatic-seo-pages` → `programmatic-seo-content-quality` → `seo-sitemap-generation` → `seo-ssr-and-prerendering`

### TanStack Query mastery (4)

`tanstack-query-alternative` → `tanstack-mutations-and-invalidation` → `tanstack-infinite-queries` → `tanstack-prefetch-and-hydration`

### TanStack Router / Start (2)

`tanstack-router-data-loaders` → `tanstack-start-server-routes`

### Scheduled jobs with pg_cron (4)

`background-jobs-and-cron` → `pg-cron-scheduled-jobs` → `pg-cron-with-pg-net-edge` → `pg-cron-recipes`

---

## All 57 Lovable skills

### Client data layer — TanStack Query (Lovable default)

| Skill | Description |
|-------|-------------|
| [`tanstack-query-alternative`](skills/tanstack-query-alternative/) | Primary TanStack patterns — keys, defaults, fetchers, hooks |
| [`tanstack-mutations-and-invalidation`](skills/tanstack-mutations-and-invalidation/) | useMutation, invalidation strategies, optimistic + rollback |
| [`tanstack-infinite-queries`](skills/tanstack-infinite-queries/) | Cursor pagination, infinite scroll, virtualization |
| [`tanstack-prefetch-and-hydration`](skills/tanstack-prefetch-and-hydration/) | Hover prefetch, route loaders, SSR hydration |

### TanStack Router and Start — server routes and loaders

| Skill | Description |
|-------|-------------|
| [`tanstack-start-server-routes`](skills/tanstack-start-server-routes/) | File-based API routes + `createServerFn` for full-stack TanStack apps |
| [`tanstack-router-data-loaders`](skills/tanstack-router-data-loaders/) | Typed routes, `ensureQueryData`, search-param schemas, suspense queries |

### Backend — Supabase and Postgres

| Skill | Description |
|-------|-------------|
| [`supabase-database-design`](skills/supabase-database-design/) | Tables, FKs, indexes, enums, money/time conventions |
| [`supabase-auth-flows`](skills/supabase-auth-flows/) | Sign up, sign in, OAuth, magic link, sessions |
| [`supabase-rls-and-auth`](skills/supabase-rls-and-auth/) | Row level security policies and patterns |
| [`postgres-triggers-and-functions`](skills/postgres-triggers-and-functions/) | Triggers, `updated_at`, RPC, signup hook |
| [`multi-tenant-backend`](skills/multi-tenant-backend/) | Organizations, memberships, recursion-safe RLS |
| [`edge-functions-and-webhooks`](skills/edge-functions-and-webhooks/) | Supabase edge functions, secrets, structure |
| [`server-input-validation`](skills/server-input-validation/) | Zod on every server endpoint |
| [`api-error-handling`](skills/api-error-handling/) | HTTP codes, JSON error shape, Supabase mapping |
| [`rate-limiting-edge`](skills/rate-limiting-edge/) | Fixed-window rate limits for login/signup/API |
| [`background-jobs-and-cron`](skills/background-jobs-and-cron/) | Overview: `jobs` table, pg_cron, scheduled functions (decision guide) |
| [`audit-logging-backend`](skills/audit-logging-backend/) | Append-only audit trail with proper actor tracking |
| [`soft-delete-and-archiving`](skills/soft-delete-and-archiving/) | `deleted_at`, partial unique indexes, restore |
| [`postgres-full-text-search`](skills/postgres-full-text-search/) | `tsvector`, GIN, search RPC, trigram fallback |

### Postgres scheduling — pg_cron

| Skill | Description |
|-------|-------------|
| [`pg-cron-scheduled-jobs`](skills/pg-cron-scheduled-jobs/) | Cron syntax, scheduling functions, monitoring, advisory locks, idempotency |
| [`pg-cron-with-pg-net-edge`](skills/pg-cron-with-pg-net-edge/) | Call Supabase Edge Functions from cron via `pg_net` + shared-secret auth |
| [`pg-cron-recipes`](skills/pg-cron-recipes/) | Cookbook: cleanups, retries, MV refresh, digests, anonymization |

### Payments — Stripe

| Skill | Description |
|-------|-------------|
| [`pricing-and-billing`](skills/pricing-and-billing/) | Entry point: Checkout, portal, plan gating |
| [`stripe-payment-webhooks`](skills/stripe-payment-webhooks/) | Full handler with Deno-correct signature verification |
| [`payment-webhook-idempotency`](skills/payment-webhook-idempotency/) | Duplicate events, unique IDs, ordering |
| [`payment-webhook-testing`](skills/payment-webhook-testing/) | Stripe CLI, local Supabase, dashboard replay |
| [`payment-failed-and-recovery`](skills/payment-failed-and-recovery/) | `past_due`, grace period, dunning UX |
| [`stripe-one-time-payment-webhooks`](skills/stripe-one-time-payment-webhooks/) | Orders table, credits, refunds |

### SEO — technical

| Skill | Description |
|-------|-------------|
| [`seo-landing-page`](skills/seo-landing-page/) | Entry point: metadata, headings, OG, SPA pitfalls |
| [`seo-ssr-and-prerendering`](skills/seo-ssr-and-prerendering/) | Populated HTML for crawlers via vite-ssg/prerender |
| [`seo-meta-tags-spa`](skills/seo-meta-tags-spa/) | Per-route title/meta with React 19 or helmet-async |
| [`seo-structured-data`](skills/seo-structured-data/) | Organization, Article, FAQ, BreadcrumbList JSON-LD |
| [`seo-sitemap-generation`](skills/seo-sitemap-generation/) | Dynamic `sitemap.xml` from Supabase, robots.txt |
| [`seo-core-web-vitals`](skills/seo-core-web-vitals/) | LCP, INP, CLS optimization for SPAs |

### SEO — programmatic

| Skill | Description |
|-------|-------------|
| [`programmatic-seo-pages`](skills/programmatic-seo-pages/) | Location, comparison, alternatives, integration templates |
| [`programmatic-seo-content-quality`](skills/programmatic-seo-content-quality/) | Thin content gates, dedup, E-E-A-T, AI guardrails |

### UI and UX

| Skill | Description |
|-------|-------------|
| [`shadcn-patterns`](skills/shadcn-patterns/) | Dialog, Sheet, DataTable, Sonner, navigation |
| [`error-states-and-empty-ui`](skills/error-states-and-empty-ui/) | Loading, empty, error on every list |
| [`optimistic-updates`](skills/optimistic-updates/) | Instant likes/toggles, delete-with-undo |
| [`dashboard-charts-recharts`](skills/dashboard-charts-recharts/) | KPI cards, theme-aware charts, server aggregation |
| [`dark-mode-and-theming`](skills/dark-mode-and-theming/) | CSS variables, Tailwind, theme toggle, audit |
| [`onboarding-copy`](skills/onboarding-copy/) | First-run flows, tooltips, empty-state copy |
| [`accessibility-pass`](skills/accessibility-pass/) | Keyboard, focus, labels, contrast, ARIA |

### Realtime, migrations, forms

| Skill | Description |
|-------|-------------|
| [`realtime-and-subscriptions`](skills/realtime-and-subscriptions/) | Supabase Realtime with reconnect + cache merge |
| [`migration-playbook`](skills/migration-playbook/) | Backward-compatible schema changes |
| [`typed-api-hooks-forms`](skills/typed-api-hooks-forms/) | SWR (alt) + Zod + react-hook-form patterns |

### Files, comms, i18n

| Skill | Description |
|-------|-------------|
| [`file-upload-storage`](skills/file-upload-storage/) | Supabase Storage buckets, signed URLs, validation |
| [`email-and-notifications`](skills/email-and-notifications/) | Resend, react-email, deliverability, in-app bell |
| [`i18n-multi-language`](skills/i18n-multi-language/) | i18next, Intl APIs, RTL, locale switching |

### Ship, quality, performance

| Skill | Description |
|-------|-------------|
| [`lovable-ship-checklist`](skills/lovable-ship-checklist/) | Pre-launch gate with billing, a11y, secrets |
| [`refactor-safe-diff`](skills/refactor-safe-diff/) | Surgical changes, no behavior drift |
| [`performance-budget`](skills/performance-budget/) | LCP, INP, CLS, bundle, React profiling |
| [`feature-flags-and-toggles`](skills/feature-flags-and-toggles/) | DB-backed flags, rollouts, kill switches |

### Growth and ops

| Skill | Description |
|-------|-------------|
| [`analytics-events`](skills/analytics-events/) | PostHog/GA4, naming, StrictMode guard |
| [`release-notes`](skills/release-notes/) | Customer-facing changelog format |
| [`support-reply`](skills/support-reply/) | Empathetic, structured customer responses |
| [`lovable-prompting-playbook`](skills/lovable-prompting-playbook/) | How to phrase work for Lovable so it ships |

Full table with slash invocations: [`skills/README.md`](skills/README.md).

---

## How to import Lovable skills

### Option 1 — Import from GitHub (recommended)

In Lovable: **Settings → Skills → Add → Import from GitHub** and paste a subdirectory URL.

```text
https://github.com/YOUR_ORG/lovable-skills/tree/main/skills/tanstack-query-alternative
```

Repeat per skill you want, or import only a [starter pack](#starter-packs).

### Option 2 — Upload ZIP

Download a skill folder, then **Settings → Skills → Add → Upload ZIP**.

### Option 3 — Write manually

Open `skills/<skill>/SKILL.md`, copy the `description` and body into Lovable's **Write manually** form. Folder name = skill name.

### Use in a chat

```text
/tanstack-query-alternative Add useProjects and useCreateProject with proper invalidation.

/stripe-payment-webhooks Implement the webhook handler and sync to Supabase.

/programmatic-seo-pages Generate location pages for these 50 US cities.

/seo-core-web-vitals My homepage scores 42 on PageSpeed mobile — fix the top three issues.

/lovable-ship-checklist Review the app before Friday's release.
```

Or describe the task; Lovable auto-matches the right skill via its "Use when…" description.

---

## Why use this repo

- **Tested against real production traps** — RLS recursion, Stripe Deno crypto, idempotent webhooks, SPA crawl issues, TanStack cache invalidation, programmatic thin content.
- **TanStack Query first** — matches Lovable's current default; SWR available as an alternative path.
- **Six layers of SEO** — meta tags, SSR, structured data, sitemap, Core Web Vitals, programmatic — not just a "SEO checklist".
- **Concise on purpose** — each skill is small enough to load without burning context.
- **Cross-referenced** — skills point at companion skills so Lovable composes them well.
- **Portable** — same `SKILL.md` shape as [Agent Skills](https://docs.lovable.dev/features/skills) (Claude, Cursor, others).
- **MIT-licensed** — fork, adapt, ship.

---

## Contributing

PRs welcome. See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the skill template, naming rules, and review checklist. Skill changes are recorded in [`CHANGELOG.md`](CHANGELOG.md).

Want a skill that's not here? Open an issue with the "Use when…" trigger and at least one example prompt that should load it.

---

## FAQ

### How many Lovable skills can I import?

As many as you want. Lovable only loads skills whose descriptions match the current request, so a large library does not slow individual chats.

### Do these replace Lovable's built-in skills?

No. Built-in skills stay read-only and managed by Lovable. These are **custom workspace skills** you own — edit, extend, or remove.

### Is TanStack Query really Lovable's default?

Yes, Lovable currently scaffolds projects with TanStack Query. The skills in this repo treat TanStack as the default; if your project already uses SWR, use [`typed-api-hooks-forms`](skills/typed-api-hooks-forms/). Never mix the two.

### Will these work in Cursor or Claude?

Yes. The `SKILL.md` shape is shared across Agent Skills implementations. Drop the folder into the appropriate skills directory (or import the ZIP).

### Do skills cost credits in Lovable?

No additional skill-specific cost. Standard chat credits apply to messages; importing or writing skills in Settings is free.

### How do I keep skills up to date?

Star and watch this repo, or fork it into your org and pull updates periodically. Skill changes ship in [`CHANGELOG.md`](CHANGELOG.md).

### How do I write my own Lovable skill?

Read [`CONTRIBUTING.md`](CONTRIBUTING.md) and [`lovable-prompting-playbook`](skills/lovable-prompting-playbook/) for skill design tips. The official guide is in [Lovable's docs](https://docs.lovable.dev/features/skills).

---

## Keywords

**Lovable skills** · **lovable workspace skills** · **lovable.dev skills** · **lovable agent skills** · **custom lovable skills** · **import lovable skills from GitHub** · **lovable tanstack query** · **lovable tanstack start** · **lovable tanstack router** · **lovable react query** · **Lovable Supabase skills** · **Lovable Stripe webhook skill** · **Lovable RLS playbook** · **Lovable pg_cron skill** · **Lovable scheduled jobs** · **Lovable SEO skills** · **lovable programmatic SEO** · **Lovable SSR prerender** · **Lovable structured data** · **Lovable Core Web Vitals** · **Lovable launch checklist** · **Lovable multi-tenant** · **Lovable dark mode** · **Lovable i18n** · **Lovable feature flags** · **Lovable accessibility** · **Lovable shadcn patterns**

---

**License:** [MIT](LICENSE). Free for personal and commercial use; attribution appreciated but not required.
