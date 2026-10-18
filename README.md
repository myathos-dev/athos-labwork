# Athos Labs

A web app for lab work (in progress): clinicians order lab tests and review results, and patients see their own orders and results. It runs on [Medplum](https://github.com/medplum/medplum), and all sample data is synthetic, generated with [Synthea](https://github.com/synthetichealth/synthea).

> **Sample data only.** This project uses made-up patients from Synthea. It does not store or process real patient or health information.

## Status

The app starts from my Athos CRM: three sales pages (Sales Hub, Lead Queue, Leads Dashboard) moved off Softr into a standalone Node.js web app. The work ahead is in [ROADMAP.md](ROADMAP.md), split into two epics in `epics/`: building the database, then building the lab UI with a patient view and a clinician view.

## Who it's for

- **Clinicians**: order lab work and review results.
- **Patients**: see their lab orders and results.

## Built with

- **Node.js + Express**: web server and API (`server/`)
- **React + Vite**: web interface (`src/`)
- **TanStack Query** and **sonner**: data loading and notifications
- **Medplum** (`external/medplum`, git submodule): the backend where patients, lab orders and results will live
- **Synthea** (`external/synthea`, git submodule): generates the synthetic patients and lab data

## Project layout

```
server/            Express server: API routes, serves the web app
src/
  App.jsx          Page routing
  blocks/          The app's pages (SalesHub, WorkQueue, LeadsDashboard)
  lib/             Data and user hooks the pages use
external/
  medplum/         Medplum (git submodule)
  synthea/         Synthea (git submodule)
```

## Run it

Requirements: Node.js 20 or newer. You also need Java 17 or newer if you generate data with Synthea.

```bash
git clone --recurse-submodules https://github.com/<your-username>/athos-labs.git
cd athos-labs
cp .env.example .env
npm install
npm run dev
```

Open http://localhost:3000.

For a production build:

```bash
npm run build
npm start
```

### Configuration

Settings go in `.env` (copied from `.env.example`). Never commit `.env`.

| Variable | What it does |
|---|---|
| `PORT` | Port the app runs on (default 3000) |
| `DEV_USER_ID`, `DEV_USER_NAME`, `DEV_USER_EMAIL` | Local development user |
| `DEV_USER_ROLE` | `Admin` sees all records; any other value sees only records assigned to that user |

## Sample data (Synthea)

All patient data comes from Synthea, which generates realistic but fake patient records. To generate some:

```bash
cd external/synthea
./run_synthea -p 10
```

Synthea writes the records to `external/synthea/output/fhir/`. Loading them into Medplum is on the [roadmap](ROADMAP.md).

## License

[GNU Affero General Public License v3.0](LICENSE).

Synthea and Medplum are separate projects included as git submodules, each under its own license (Apache 2.0).
