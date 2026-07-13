# Sorter V2 wiring

Wiring documentation for the Sorter V2 machine, as a small SvelteKit site so it's
easy to extend and share.

Pages:

- **Wire harness** (`/`) — 24V power distribution, the single system interconnect
  diagram, wire schedule, parts, and connector types.
- **Stepper connectors** (`/steppers`) — basically board v1.3 stepper pinout,
  board-to-motor connector mapping, and a connector photo reference.

## Develop

```
npm install
npm run dev
```

## Structure

- `src/routes/+page.svelte` — wire harness page
- `src/routes/steppers/+page.svelte` — stepper connectors page
- `src/lib/components/` — diagram components (`SystemDiagram`, `StepperPinout`, `PinSwap`)
- `static/` — connector photos
- `src/app.css` — global document styling

Deployed on Vercel.
