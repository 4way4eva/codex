# A.F.G. EV0LVERSE integration contract

The authoritative A.F.G. simulation package is maintained in `4way4eva/EV0LVERSE` under `afg/` (introduced by EV0LVERSE PR #4). This document defines how Codex-side tooling should consume that package without duplicating its source assets.

## Consumer contract

A consumer should:

1. Read `afg/data/afg-defense-grid.json`.
2. Require `schemaVersion == "1.0.0"`.
3. Require `framing == "fictional-simulation"` as an invariant.
4. Validate the document against `afg/schemas/afg-defense-grid.schema.json`.
5. Optionally load normalized Scout/Sentry scene coordinates from `afg/data/afg-nodes.csv`.
6. Treat the SVGs in `afg/assets/` as visual references and the JSON/CSV as the machine-readable contract.
7. Use `afg/manifest.json` and `afg/docs/SOURCE_RASTER_HASHES.json` for provenance/integrity checks.

## Topology assumptions

The current contract declares:

- one Core Colony;
- 12 Sentry Ring nodes;
- 12 Scout Ring nodes;
- 12 radial simulation lanes;
- four abstract response states: `detect`, `intercept`, `swarm_response`, and `seal_breach`.

Coordinates are normalized rather than physical. Renderers may scale or transform them for Unity, Unreal, web, or other visualization environments.

## Safety and scope invariant

Do not infer, generate, or add physical construction dimensions, weapon parameters, chemical recipes, biological deployment parameters, or real-world tactical optimization from the source diagrams. The A.F.G. package is an in-universe/game-simulation topology; response states remain abstract gameplay or graph-state events.

## Versioning

Consumers should fail closed on an unsupported `schemaVersion`. A future schema revision should be introduced in EV0LVERSE first, along with its schema and manifest changes, before Codex-side consumers adopt it.

## Example

See `docs/afg/afg-integration.example.json` for a minimal locator/contract descriptor.
