# Calpe Digital — Community Event Automation

## Purpose

Event automation engine for Calp Digital, a curated community for conscious founders, remote professionals, and digital nomads in Calpe/Costa Blanca, Spain. Automates the monthly event cycle: plan event, generate copy, create Facebook event, blast WhatsApp, manage Stripe payments, post-event follow-up.

## Tech Stack

- **Language**: Python 3.12+
- **Framework**: FastAPI with uvicorn
- **LLM (primary)**: Gemini Pro via Vertex AI
- **LLM (complex)**: Claude Sonnet (finishing tasks, strategy, QA)
- **Database**: Firestore (serverless, GCP)
- **Deployment**: Cloud Run (europe-southwest1)
- **Config**: Pydantic Settings

## Commands

```bash
# Development
uv run main.py              # Start the application
uv run pytest               # Run tests
uv run pytest --cov         # Run tests with coverage
uv run ruff check .         # Lint code
uv run ruff format .        # Format code

# Dependency management
uv sync                     # Install dependencies
uv sync --dev               # Install with dev dependencies
uv add <package>            # Add a dependency
```

## Project Structure

```
src/
  calpe_digital/
    api/                # FastAPI routes
    integrations/       # Facebook, WhatsApp, Stripe, Vertex AI clients
    models/             # Pydantic models (events, members, messages)
    templates/          # Event copy templates, WhatsApp message templates
    services/           # Business logic (event lifecycle, member management)
config/                 # Configuration files
docs/                   # Documentation and reference materials
  reference/            # Imported docs from Google Shared Drive
scripts/                # Utility scripts
tests/                  # Test suite
```

## GCP Project

- **Project ID**: `calpe-digital`
- **Billing**: Moriarty.co (`010B3B-E87C77-45ED6B`)
- **Region**: `europe-southwest1` (Madrid)
- **gcloud account**: `peter@moriarty.co`
- **APIs enabled**: Vertex AI, Firestore, Cloud Run, Secret Manager, Sheets

## Environment Variables

```env
# GCP
GCP_PROJECT=calpe-digital
GCP_REGION=europe-southwest1

# Stripe (Level 11 Digital account — EUR)
STRIPE_API_KEY=               # Restricted key from Level 11 Digital Stripe

# Facebook Graph API
FACEBOOK_PAGE_ID=             # calpe.digital page
FACEBOOK_GROUP_ID=            # calpe.digital group
FACEBOOK_ACCESS_TOKEN=        # Page access token with events_manage, groups_manage

# WhatsApp Cloud API (future — requires business number)
WHATSAPP_PHONE_NUMBER_ID=
WHATSAPP_ACCESS_TOKEN=

# Optional
ANTHROPIC_API_KEY=            # For Claude fallback/QA tasks
```

## Key Integrations

### Facebook
- **Page**: https://www.facebook.com/calpe.digital
- **Group**: https://www.facebook.com/groups/calpe.digital
- **API**: Graph API v21.0 — event creation, group posting, page posting

### Stripe
- **Account**: Level 11 Digital (EUR)
- **Use**: Event ticket products/payment links, customer data, revenue reporting
- **Secret**: `stripe-api-key` in GSM (`calpe-digital` project)

### WhatsApp (Phase 2 — requires business number)
- **Current**: Community linked to Peter's personal number (manual sends)
- **Future**: WhatsApp Cloud API with business number for automated event blasts

### Vertex AI (Gemini Pro)
- **Use**: Event copy generation, connection prompt generation, post-event recaps
- **Region**: `europe-southwest1`

## Google Workspace

- **Domain**: `calpe.digital` (secondary domain on moriarty.co Workspace)
- **Accounts**: `admin@calpe.digital`, `event@calpe.digital`
- **Shared Drive**: "Calpe Digital" (brand strategy, transcripts, event materials)
- **DWD**: `pa-agent@agent-484513.iam.gserviceaccount.com` can impersonate calpe.digital users (drive.readonly scope)

## Brand Context

- **Tagline**: "Where ambition meets balance"
- **Voice**: Sophisticated, Warm, Intelligent
- **Audience**: Conscious entrepreneurs, founders, high-skilled remote professionals, established nomads
- **Excluded**: Aggressive sales agents, crypto/forex promoters, restaurant menu spammers
- **Venue partner**: Calp Partners Coworking (Brianda Sosa)
- **Event cadence**: Monthly (Real Talk mixer), Bi-monthly (Walk & Talk), Quarterly (Guest speaker)
- Full brand strategy: `docs/reference/brand-strategy.md`

## Event 1 Results (Dec 5, 2025)

- "Pre-Holiday Connect & Mixer" at Partners Coworking
- 16 registrations, ~€264 Stripe revenue, €11/ticket
- Facilitated connection prompts, DJ, coworking pass raffle
- Hosts: Peter Moriarty, Zyl Go, Brianda Sosa

## Gotchas

- **Facebook Graph API**: Event creation via API requires app review and specific permissions (`pages_manage_events`). May need manual event creation initially with API for posting/promotion only.
- **WhatsApp Cloud API**: Requires verified Meta Business account + dedicated phone number. Message templates need Meta approval (24-48hr). Not available until business number is set up.
- **Stripe account**: This is Level 11 Digital (EUR), NOT the itGenius US account. Different API key.
- **Gemini region**: Use `europe-southwest1` for Vertex AI to match Cloud Run region.
- **Brand voice**: All generated content must pass brand voice check — "Sophisticated, Warm, Intelligent." No grindset language, no pretentious exclusion.

## Reference Docs

- `docs/active.md` — current tasks and status
- `docs/decisions.md` — append-only decision log
- `docs/reference/brand-strategy.md` — full brand strategy document
- `docs/reference/event1-copy.md` — Event 1 promotional copy
- `docs/reference/event1-results.md` — Event 1 registrations and Stripe data
- `docs/reference/transcript-brand-planning.md` — Brand planning conversation
- `docs/reference/transcript-event1-planning.md` — Event 1 planning with Brianda
- `docs/reference/transcript-community-structure.md` — Community structure discussion
- `docs/reference/members.csv` — Member email list (45 contacts)
