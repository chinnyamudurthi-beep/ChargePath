# ChargePath implementation plan

## Product scope
ChargePath is a responsive electric-vehicle charging station planner that recommends the best station and route using trip distance, current battery level, expected charging time, and station availability. The interface makes Dijkstra, greedy selection, and shortest-path ideas understandable while comparing charging options.

## Approved design direction
- **Design movement:** futuristic transit-control UI with editorial dashboard restraint; dark graphite canvas, electric cyan routing, and lime energy accents.
- **Core principles:** high signal over decoration; route logic stays legible; live operational cues feel tactile; mobile remains a first-class planning surface.
- **Color philosophy:** near-black graphite supports map-like focus; cyan communicates navigation and certainty; acid lime marks charge/availability; warm amber flags trade-offs.
- **Layout paradigm:** asymmetric split cockpit: a command rail on the left, route visualization as the visual anchor, and a bottom/side comparison shelf rather than a centered card grid.
- **Signature elements:** route-node constellation, pill-shaped algorithm chips, and scanline/contour textures used sparingly.
- **Interaction philosophy:** direct manipulation and immediate feedback; input changes re-rank stations without leaving the main view; selected cards expose reasoning, not just a score.
- **Animation:** subtle route pulse, node glow on selection, count-up metrics, and short ease-out panel transitions. Respect reduced motion.
- **Typography:** Space Grotesk for display/headings and Inter for utility copy, with tabular numeric treatment for metrics.
- **Brand essence:** a calm co-pilot for smarter charging decisions; precise, transparent, energetic.
- **Brand voice:** concise and confident. Example lines: “Plot the next clean stop.” “Every recommendation shows its work.”
- **Wordmark/logo:** a compact “CP” monogram formed by a route curve entering a charging bolt, paired with the ChargePath wordmark.
- **Signature brand color:** electric cyan `#65E6D8` used only for the brand route and primary action.

## Implementation
- Use the existing React/Vite starter and keep the experience static/local because the user asked for a planner UI, not login or persistence.
- Build a single-page responsive planner in `client/src/App.tsx`, with reusable presentational UI in `client/src/components/` only where useful; keep data and route-ranking helpers in `client/src/lib/`.
- Use an inline SVG map-style visualization so no external image or map key is required. Include route segments, charging nodes, and an active vehicle marker.
- Implement deterministic local ranking: a Dijkstra-like path cost for overall recommendation plus a greedy comparator. Rank by reachability, arrival battery, availability, distance, charger speed, charging time, and route impact.
- Add controls for origin, destination, battery, and vehicle profile; clicking a station updates the recommendation panel. Include a mobile-friendly horizontal station rail and accessible button labels.
- Serve `/manus-routes.json` from `public/` with the root route declaration.
- Configure a static build using the existing Vite/pnpm toolchain and keep `app.config.ts` with a durable inline SVG data URL logo.

## Project structure
- `client/src/App.tsx`: page composition, local planner state, controls, algorithm explainer, station cards.
- `client/src/index.css`: theme tokens, layout, map, responsive behavior, motion/accessibility.
- `client/src/lib/planner.ts`: sample stations and ranking logic for Dijkstra/greedy comparison.
- `public/manus-routes.json`: route manifest for the home page.
- `app.config.ts`: project logo metadata.
