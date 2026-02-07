# Decision Log

> Append-only record of architectural and strategic decisions.
> Captures the "why" behind choices for future reference.

---

## 2026-02-07 — Project creation and tech stack

**Context**: New sub-project for Calp Digital community event automation. Similar in nature to Gary (agent-attract) but focused on Facebook events and WhatsApp group promotion, not video/blog content.

**Decisions**:
- **LLM**: Gemini Pro via Vertex AI as primary (GCP-native, cost-effective for copy generation). Claude Sonnet as secondary for complex/QA tasks.
- **GCP project**: `calpe-digital` under moriarty.co org, `peter@moriarty.co` account. Moriarty.co billing.
- **Region**: `europe-southwest1` (Madrid) — consistent with Overlord, closest to Valencia.
- **Stripe**: Separate account under "Level 11 Digital" (EUR). Not the itGenius US account.
- **WhatsApp**: Business number deferred. Current community uses Peter's personal number. Will set up WhatsApp Cloud API when business number is obtained.
- **Facebook**: Page and group already exist. Will use Graph API for event creation and posting.
- **Build approach**: Phase 0 (scaffold) done manually. Phase 1+ will use Ralph for autonomous implementation from PRD.

## 2026-02-07 — Reference document import

**Context**: admin@calpe.digital Google Shared Drive contains comprehensive brand strategy, 3 strategic conversation transcripts, event 1 materials, member list, and Stripe customer data.

**Decision**: Import all text content as markdown into `docs/reference/`. This gives the codebase (and Ralph) full context without needing Drive API access at runtime. DWD impersonation via `pa-agent` SA works for read access but only has `drive.readonly` scope.
