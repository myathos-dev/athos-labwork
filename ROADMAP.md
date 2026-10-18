# Roadmap

The work ahead is split into two epics, done in order:

1. [Epic 1: Database](epics/01-database.md): new classifier tables, plus Synthea lab data loaded into Medplum
2. [Epic 2: Lab UI](epics/02-lab-ui.md): patient view and clinician view, built from the Athos CRM base

All data is synthetic sample data. No real patient information.

## Later: multi-layer architecture with Claude

Whether this gets built depends on how the rules-based classifier performs. The entries log shows how often each domain hits the fallback.

Layers, in order:

1. **Clinical overrides**: hard-coded safety responses. Always run first; never sent to an AI model.
2. **Rules-based classifier** (Epic 1): handles every entry it can match.
3. **Claude API**: only for low-confidence entries that fall back.

Rules for layer 3:

- Claude is used through its API as a feature of the app. The project does not build, train, fine-tune or evaluate AI models, and does not collect entries or ratings as training data.
- The app uses its own API key, stored in `.env` with a placeholder in `.env.example`. It is never the key used for work sessions.
- Sample data only: no real people's personal data is sent.

- [ ] Decide whether to add layer 3, based on the classifier's fallback rate
