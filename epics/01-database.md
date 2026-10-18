# Epic 1: Database

Create the database for the app: new tables for the rules-based classifier, plus the lab data from Synthea. Sample data only, no real patient information.

## Classifier tables

| Table | What it holds |
|---|---|
| `overrides` | Clinical contraindication keywords and the safety response for each (no call to action). Checked first, before anything else. |
| `stacks` | Stack name and `trigger_keywords`. A stack match skips normal domain routing. |
| `domains` | Domain name and its comma-separated `keywords` list. |
| `intensity_modifiers` | High and low modifier words. Medium is the default when none match. |
| `protocols` | Response templates grouped by `domain` + `intensity` + `variant_group`, with `{{slot_key}}` placeholders. |
| `slots` | `slot_key` and pipe-separated interchangeable phrases. |
| `entries_log` | One row per entry: matched domain, intensity, confidence, and whether the fallback, stack or override fired. |

### Lexicon rules
- [ ] At least 5 keywords per domain
- [ ] All keywords stored lowercase
- [ ] No keyword shared between domains, so scores can't tie

### Tasks
- [ ] Create the tables
- [ ] Fill them with starting content
- [ ] Build the classifier pipeline in order: override check → stack detection → domain scoring (keyword hits = `confidence_score`) → intensity → random variant group per session → slot rendering → log the entry

## Lab data

- [ ] Run Medplum locally from `external/medplum`
- [ ] Generate patients and lab data with Synthea (`external/synthea`)
- [ ] Load the Synthea output into Medplum

## Open decisions
- [ ] Where the classifier tables live (Medplum or a separate database)
- [ ] Whether the classifier pipeline belongs in this epic or in Epic 2
