# Sorter V2 wiring

Wiring documentation for the Sorter V2 machine, as a small SvelteKit site so it's
easy to extend and share.

Pages:

- **Wire harness** (`/`) — 24V power distribution, the single system interconnect
  diagram, wire schedule, parts, and connector types.
- **Stepper connectors** (`/steppers`) — basically board v1.3 stepper pinout,
  board-to-motor connector mapping, and a connector photo reference.
- **Order spec** (`/order`) — order-ready cable build list for a custom harness
  vendor: gauges, connector part numbers, pin maps, and which ends stay bare
  for on-machine splicing. TBDs filled in with stated guesses.
- **WireViz** (`/wireviz`) — rendered harness drawings with downloads
  (PDF/PNG/SVG/HTML/BOM/YAML) and a ready-to-send supplier RFQ zip. Not
  validated; guesses are marked GUESS in the drawings.

## Develop

```
npm install
npm run dev
```

## Structure

- `src/routes/+page.svelte` — wire harness page
- `src/routes/steppers/+page.svelte` — stepper connectors page
- `src/routes/order/+page.svelte` — harness order spec page
- `wireviz/` — WireViz YAML sources for the harness drawings; render with
  `wireviz wireviz/*.yml -f sp -o static/harness` (needs `pip install wireviz`
  and graphviz)
- `static/harness/` — rendered WireViz drawings (png + svg)
- `src/lib/components/` — diagram components (`SystemDiagram`, `StepperPinout`, `PinSwap`)
- `static/` — connector photos
- `src/app.css` — global document styling

Deployed on Vercel.
