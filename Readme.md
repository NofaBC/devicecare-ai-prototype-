# DeviceCare AI™ — Judy-style L1/L2/L3 support prototype

**NOFA AI Factory · Proof of Concept · October 2026**

A Next.js demonstration of card-led medical-device support, a Judy-style chat interface, simulated L1/L2 guidance, and Level 3 technical escalation through Slack.

## Quick start

```bash
npm install
npm run dev
```

Open http://localhost:3000. Select **Use synthetic sample ID card** to enable case simulations and Slack test messages.

## Deploy to Vercel

1. Create a private GitHub repository and upload these files.
2. Import the repository into Vercel as a Next.js project.
3. Optionally set `SLACK_DEMO_WEBHOOK_URL` in Vercel environment variables. Keep it secret.
4. Deploy. Test escalation using the **synthetic sample card only**.

Incoming webhooks: https://api.slack.com/messaging/webhooks

## Implemented

- Card-first intake: no patient registration or manually typed identifying fields.
- Local-only photograph selection and preview; **uploaded card pictures are never sent to the server, OCR service, or Slack**.
- Synthetic device card for the full functional demonstration.
- Judy-style deterministic text interaction; four safe, scripted scenarios.
- Level 1 general information, Level 2 constrained support workflow, Level 3 escalation path.
- Server-side Slack webhook posting **synthetic scenario data only**.
- Case summary UI, error/availability states, fallback when Slack webhook isn't configured.
- No database, identifiers, real records, secrets in frontend, external AI call, or actual medical-device connectivity.

## Important prototype limitations

This is a **scripted conversational demonstration**, **not an LLM-backed Judy service**, manufacturer-authorized diagnostic product, certified on-call service, or validated medical software. Support replies are conservative example content and not substitutes for official device-specific instructions. An optional voice/avatar integration and approved-document retrieval would be the next authorized build phase, after knowledge review.

A real patient's ID card commonly contains identifiable health information. The future production system will need explicit consent, secure ingestion, role-based access, model/device identification extraction, applicable HIPAA arrangements, retention/deletion rules, threat modeling, manufacturer review, clinical safety validation, and a regulatory assessment before ingesting such cards. The current prototype intentionally does not transmit, extract, or persist real card images. **Do not use a real patient ID card when demonstrating or testing this app.**

Slack webhook success means **message delivered**, not **technician acknowledged**, and no escalation response timer/fallback is implemented. Real-world L3 support requires an on-call agreement and monitored acknowledgment workflow.

Do not use this app for patient care or to determine the safety of waiting for charging assistance. No resets, reprogramming, treatment decisions, battery estimates, or implant telemetry are supported.

## Proposed production pathway

- Manufacturer document permission + versioned, cited RAG knowledge store.
- OCR of a device ID card in a compliant processing environment, with data minimization.
- Deterministic safety/triage rules and validated procedure flowcharts.
- Judy LLM/voice/avatar only for the bounded conversational interface; refusal/escalation policy enforced separately.
- Case store, authentication, audit events, durable queues, monitored SLAs, and escalation acknowledgment by authorized technicians.
- Clinical, device-manufacturer, privacy and regulatory reviews before clinical use.

## Technical details

Built with Next.js App Router, TypeScript, React, Lucide. No account creation or API keys needed for core demonstration. `POST /api/escalate` accepts only `{ "demo": true, "scenario": "A27"|"CHARGER_POWER"|"ROUTINE"|"UNKNOWN" }` and posts a generic synthetic case to Slack when configured.
