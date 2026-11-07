# Release Hype Radar

An entertainment social-listening and incident-triage application for release launches, trailers, cast moments, announcements, and emerging audience concerns.

## What it demonstrates

- Bounded, explainable anomaly detection using a rolling z-score baseline.
- Topic, market, sentiment, platform, and creator context for every alert.
- Response ownership and SLA thinking: alerting without a response workflow is not operationally useful.
- Evidence-aware triage for reputation and accessibility concerns.

## Run locally

```bash
npm install
npm run dev
```

Navigate to `http://127.0.0.1:3000`. The app is deliberately seeded for portfolio review; it does not collect or scrape social data.

## Decision flow

1. Ingest authorized mentions with provider/source IDs and timestamps.
2. Deduplicate and classify by topic, locale, sentiment, and safety category.
3. Compare observed mention volume to a rolling baseline.
4. Attach representative evidence and assign a named owner before escalating.
5. Measure alert decay and whether the recommended response resolved the concern.

## Key APIs

| Route | Purpose |
| --- | --- |
| `GET /api/v1/projects/release-hype-radar/workspace` | Detection parameters and triage target |
| `GET /api/v1/projects/release-hype-radar/quality` | Ingestion quality checks |
| `POST /api/v1/actions` | Acknowledge and audit an alert |
| `GET /api/v1/projects/release-hype-radar/audit-events` | Review response history |

## Production safeguards

- Use only approved listening/API providers and comply with data terms, consent, geography, and retention policies.
- Store raw evidence separately from aggregate metrics and restrict it with tenant RBAC.
- Calibrate sentiment and topic models by market; do not make high-stakes decisions from an unreviewed model label.
- Define escalation paths for misinformation, harassment, safety, accessibility, and legal issues.

## Validation

```bash
npm run check
npm test
docker compose up --build
```
