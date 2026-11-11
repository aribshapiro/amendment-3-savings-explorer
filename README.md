# Miami-Dade Amendment 3 Savings Explorer

An interactive map of every Miami-Dade County parcel and what Florida's
Amendment 3 is estimated to save it on property taxes in 2027 and 2028.

**Live map:** https://aribshapiro.github.io/amendment-3-savings-explorer/

## What it does

- Search any address, folio, city, or ZIP to see a parcel's estimated
  savings — 2027 and 2028, plus the two-year total.
- Zoom out to see a dot for every Amendment 3-eligible parcel in the
  county, coloured by two-year savings (pale = small, deep red = large).
  Zoom in and the dots become the actual parcel polygons.
- Click any parcel (or pick a condo unit from the dropdown) for the full
  breakdown: assessed and market value, current exemption, the Save Our
  Homes cap reduction, and the Amendment 3 exemption for 2027 and 2028.
- Countywide totals: **$434,546,387** estimated in 2027 and
  **$745,605,053** in 2028, across **451,610 eligible parcels**.

## Data and method

- Parcel records and savings: a precomputed table of 939,447 Miami-Dade
  folios (Supabase, `public.savings`), built from the Miami-Dade Property
  Appraiser's 2026 assessment roll with 2026 adopted non-school millage
  as the proxy. The current non-school homestead exemption is the
  CPI-indexed **$51,411**; Amendment 3 raises it to **$150,000** in 2027
  and **$250,000** in 2028. Savings = the taxable-value reduction times
  the parcel's non-school millage / 1000.
- Parcel geometry: Miami-Dade County's Parcelpoly service, joined by folio.
- The numbers are **projections, not tax bills** — they use 2026
  assessments and millage. The school-tax exemption ($25,000) is unchanged
  by Amendment 3 and is not part of the savings.

## Running it

This is a single self-contained `index.html`. No build step, no server.

- **Use it:** open the live map link above, or double-click `index.html`
  in a regular desktop browser.
- **Develop:** edit `index.html` directly. It loads Leaflet and the Esri
  World Topographic basemap from CDNs, and reads the savings table and
  parcel geometry live from Supabase and the county's ArcGIS services.

The Supabase publishable key in the file is public by design (the table
is read-only through Row Level Security). No secret or service-role key
is in this repo.
