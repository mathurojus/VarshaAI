# Varsha AI design brief

## Direction
**Monsoon Signal / Editorial Operations** — a dark, high-contrast weather intelligence interface that feels like a mission-control surface rather than a generic analytics dashboard.

## Design movement
Calm operational clarity: dense information is organized into generous cards, hairline rules, and restrained amber highlights. The interface should feel premium through hierarchy, not decoration.

## Core principles
1. Make the current weather regime the first thing an operator sees.
2. Use warm amber only for active signals, thresholds, and key numbers.
3. Pair technical data treatments with editorial labels so the product is legible to both scientists and decision-makers.
4. Motion should explain state: reveal, count, pulse, hover, and refresh — never distract.

## Color philosophy
Midnight navy canvas (#06111f) with layered slate panels (#0c1a2b, #102338), pale blue-white type, muted steel labels, and a signature rain amber (#f7b955). Risk uses coral; positive skill uses mint.

## Layout paradigm
Responsive command center: slim top bar, a 12-column desktop grid, large map / forecast canvas, and a compact right rail for regime mix and verification. On mobile, the rail stacks below the main forecast and the table becomes horizontally scrollable.

## Signature elements
- Amber vertical regime marker and active pulse.
- India rainfall heatmap drawn in CSS/SVG with plotted district points.
- Donut regime mix ring and horizontal skill bars.
- Fine animated grid and rain haze in the shell background.
- Micro status chips that read like operational telemetry.

## Interaction philosophy
Every clickable control has an immediate, low-friction response: horizon tabs update forecast figures, district filters change the table emphasis, refresh briefly changes the model-run state, and map/table rows lift on hover. Keyboard focus remains visible.

## Animation
Page load uses staggered fade-and-rise. Metric values count up. The live marker pulses gently. The regime ring draws in. Refresh uses a 700ms loading state and updates the timestamp. Respect prefers-reduced-motion.

## Typography system
Use an editorial sans stack: Inter / ui-sans-serif for interface copy and IBM Plex Mono / ui-monospace for telemetry, numeric values, and model metadata. Headings are tight, medium-weight, and tracked slightly negative.

## Brand essence
Varsha means rain. The brand is precise, grounded, and quietly confident: a layer of intelligence between raw NWP output and useful action.

## Brand voice
Concise, evidence-led, operational. Prefer “Regime confidence 86%” over “The model is very sure.”

## Wordmark / logo
A simplified filled rain-cloud silhouette with a single amber diagonal monsoon front line and three negative-space raindrops. The header uses the mark beside “VARsha AI”; the favicon/project icon uses the same silhouette on a full-bleed navy square.

## Signature brand color
Monsoon amber #f7b955 — reserved for current regime, active controls, heavy-rain thresholds, and primary metric emphasis.

## Delivery architecture
Static single-page frontend with no backend or database. Serve `index.html`, `styles.css`, and `app.js` from the project root on port 3000. Use the route manifest at `/manus-routes.json`. Future forecast data can be attached behind the existing filter/refresh interactions without changing the UI contract.
