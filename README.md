# AgriCycle Rajasthan

**Waste to Wealth — Turning Agricultural Waste into Opportunity.**

A responsive prototype for the MBM Amrit Mahotsav Innovation Contest (MAMIC), MBM University. It connects fictional Rajasthan farmers, industrial buyers and transporters around agricultural residue listings, matching, recommendations and pickup tracking.

## Run locally

Requires Node.js 20 or newer and npm.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite. To create and preview a production build:

```bash
npm run build
npm run preview
```

No paid service or API key is required. The landing page uses a remote Unsplash image; app functionality itself is local. If offline, all app workflows still operate.

## Demo accounts

Open the app, then use the account selector in the top bar to switch roles. The preloaded demo users are:

| Role | Name | Email |
|---|---|---|
| Farmer | Ramesh Choudhary | ramesh@demo.ag |
| Buyer | Thar BioEnergy | procurement1@demo.ag |
| Transporter | Marwar Logistics | dispatch1@demo.ag |

This is a demo role switcher, not real authentication. The app also seeds 10 farmer profiles, 6 buyers, 5 transporters, 15 residue listings, and one in-transit order.

## Architecture

- `src/data.ts` defines the shared typed domain model and fictional Rajasthan seed data.
- `src/App.tsx` contains the landing page, responsive role-aware application shell, route pages, forms and workflow operations.
- `src/styles.css` defines the responsive visual system.
- React Router handles app navigation; Recharts renders illustrative activity charts; Lucide React supplies interface icons.
- The `agricycle-v1` localStorage key stores the shared users, listings and orders. `agricycle-user` stores the selected demo account. Clear these keys in browser storage to restore the original seed state.

## Prototype logic

The recommendation engine is transparent rule-based logic. Each residue type maps to possible applications and reasons; stated condition can remove unsuitable uses (for example, mixed material is not recommended for biomass fuel). It is not a trained machine-learning model, and recommendations are indicative pending material inspection.

Matching scores combine a simulated district-order proximity score, basic buyer industry compatibility and listing quantity. District indices stand in for distance; displayed matches are not geospatial or routing results. Pickup cost is a configurable demo formula: **₹900 base + ₹42 per simulated kilometre + ₹250 per tonne**. Impact analytics clearly mark all values illustrative; potential diversion is estimated as delivered quantity plus 18% of listed stock, not a measured environmental outcome.

## Main journey

1. Switch to a Farmer account, add/edit/delete a residue listing.
2. Switch to a Buyer account, search/filter listings and request a quantity.
3. Switch back to the Farmer, review the request and assign a transporter or accept it.
4. Switch to the assigned Transporter, accept pickup (if unassigned), start transit and mark delivery.
5. Review the order status and illustrative impact totals in the dashboards.
