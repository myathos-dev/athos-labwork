# Epic 2: Lab UI

Turn the Athos CRM base into the lab-work interface, with a patient view and a clinician view, on top of the database from [Epic 1](01-database.md).

## Clinician view
- [ ] Patient list and search
- [ ] Create lab orders (ServiceRequests)
- [ ] Track order status
- [ ] Review lab results per patient

## Patient view
- [ ] See own lab orders and their status
- [ ] See own lab results

## Convert the CRM base
- [ ] Rework Sales Hub → clinician home
- [ ] Rework Lead Queue → clinician work queue for lab orders
- [ ] Rework Leads Dashboard → patients and orders table
- [ ] Replace the local JSON record store (`server/`, `src/lib/datasource.js`) with the Epic 1 database
- [ ] Remove sales-only content (DM and email templates, people-search links, lead types)

## Open decisions
- [ ] How users sign in and how the patient or clinician role is set
