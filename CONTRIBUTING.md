# Contributing to Lovable Skills

Thanks for considering a contribution. This repo curates **production-quality Lovable skills** — playbooks that Lovable can load on demand. Every skill should make a real project ship faster or safer.

## What makes a good Lovable skill

A skill belongs here if it:

1. **Solves a recurring task** Lovable users hit on most projects (not one-offs).
2. **Has a clear trigger** — the description starts with "Use when…" and names what scenarios load it.
3. **Saves more tokens than it spends** — concise, opinionated, no rambling.
4. **Is portable** — works in any Lovable workspace (no project-specific names hardcoded).
5. **States what it does NOT cover** — clear boundaries reduce conflicts with other skills.

If your idea fits, open a PR. If unsure, open an issue first.

## Skill structure

```
skills/your-skill-name/
├── SKILL.md           # required
└── examples.md        # optional bundled file
```

### `SKILL.md` template

```markdown
---
name: your-skill-name
description: >-
  Use when <trigger>. Not for <out-of-scope>.
---

# Title

One-paragraph "what and why".

## Section 1
...

## Section 2
...

## Avoid

- Anti-pattern 1
- Anti-pattern 2

## Checklist

- [ ] Item
- [ ] Item
```

### Rules

- `name`: lowercase, hyphens only, ≤ 64 chars, must equal the folder name.
- `description`: starts with **"Use when"**, ≤ 1024 chars, mentions both scope and non-goals.
- Body: under **500 lines**; use [progressive disclosure](https://docs.lovable.dev/features/skills) (`examples.md`) for longer content.
- Cross-reference other skills by name in backticks: `` `supabase-rls-and-auth` ``.
- ASCII only — no smart quotes or em-dashes that break copy-paste.
- Code blocks must specify the language.

## Workflow

1. Fork and clone.
2. Create `skills/your-skill-name/SKILL.md`.
3. Add the skill to:
   - The category table in [`skills/README.md`](skills/README.md).
   - The category table in [`README.md`](README.md).
   - [`CHANGELOG.md`](CHANGELOG.md) under "Unreleased".
4. Open a PR with a short rationale and at least one Lovable prompt example that should trigger your skill.

## Editing existing skills

- Fix bugs and out-of-date snippets freely; reference the source (Stripe docs, Supabase docs) in the PR.
- Substantial changes that alter the skill's contract (renames, removed sections) should add a CHANGELOG entry.

## Reviews

A maintainer will check:

- Description triggers cleanly without conflicting with neighbors.
- Code samples compile in current Lovable defaults (Vite + React + TS + Supabase).
- Skill stays focused (one job, not three).

## Code of conduct

Be kind, be specific, assume good intent. Off-topic, harassing, or marketing-only PRs will be closed.
