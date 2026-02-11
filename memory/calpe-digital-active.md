# Active Tasks — Calpe

> This file is the source of truth for what's in-flight, what needs checking, and what's coming up.
> Claude reads this at the start of every session and surfaces anything due or overdue.
> Update this file at the end of every Claude session.

---

## In Progress

- **[TBD] Phase 1 — Event automation core** — Build the monthly event lifecycle: event copy generation (Gemini Pro), Facebook event creation/posting (Graph API), Stripe product/payment link creation, member management. See CLAUDE.md for full architecture.

## Pending Review

- **[TBD] Stripe API key** — Get restricted API key from Level 11 Digital Stripe account, store in GSM as `stripe-api-key`.

## Scheduled Checks

(none yet)

## Completed (Recent)

- ~~[2026-02-08] Facebook Graph API access~~ — Facebook App "Calpe Digital" created (ID: `1670527017455271`). Never-expiring page token with 16 permissions including `pages_manage_posts`. Full read+write capability verified (draft post created/deleted). All tokens in GSM (`facebook-page-token`, `facebook-user-token`, `facebook-app-secret`). Historical posts archived in `docs/reference/facebook-posts.md`. Event 2 copy saved in `docs/reference/event-2-cowork-feb12.md`.
- ~~[2026-02-07] Project scaffold~~ — GCP project created (`calpe-digital`, Moriarty.co billing), GitHub repo (`Peter-Moriarty/calpe-digital`), Vertex AI + Firestore + Cloud Run + Secret Manager + Sheets APIs enabled. CLAUDE.md, docs, reference materials imported from Google Shared Drive. Parent orchestrator updated (routing, registry, cross-project).

---

## How This File Works

**Sections:**
- **In Progress** — actively being worked on across sessions
- **Pending Review** — done but needs verification after a time delay (date = when to check)
- **Scheduled Checks** — recurring or future reviews (date = when due)
- **Completed (Recent)** — finished items, kept for ~30 days then removed

**Rules:**
- Dates in brackets are due dates, not start dates
- Move items down as they progress: In Progress → Pending Review → Completed
- Remove completed items older than 30 days (they're in git history and decisions.md)
- If an item spawns new work, add the new item and complete the original
