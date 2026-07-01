# Visual Walkthrough

This page gives a quick visual route through the current Digital Mycelium v0.3 public showcase.

## 1. Demo-ready state

Show:

`HELD_DEMO_READY_STATE_v0_3\HELD_STATE.txt`

Meaning:

The public demo route is currently held, top-of-chain indexed, and live-rehearsed.

## 2. Top-of-chain packet

Current packet:

`Digital_Mycelium_v0_3_OPTIONAL_OLLAMA_WITNESS_MANIFEST_PHASE_SEAL.zip`

SHA-256:

`67631359D0BA30EB3BC0F4D436F1B984CEA5B794136F9F7BB3934CCF4CF1D2AB`

## 3. Hardened cockpit

Run:

`python3 -u .\local_review_cockpit_v0_2_2.py`

Then use the current top-of-chain packet as input.

## 4. Expected result

State:

`CROSS_PLATFORM_GENERALIZED_INTAKE_HELD`

Verified:

`True`

## 5. Rehearsal proof

Live rehearsal seal SHA-256:

`D3DD078BCDB7900DA07F447B27A5DC0F359497BF6383E98D1496C83AB025B98A`

## 6. Authority boundary

The deterministic kernel and receipts remain authority.

Ollama is optional witness commentary only.

Ollama does not decide HELD.

## Screenshot slots

Add screenshots here later:

- `SCREENSHOTS/01-demo-ready-state.png`
- `SCREENSHOTS/02-top-of-chain-state.png`
- `SCREENSHOTS/03-cockpit-input.png`
- `SCREENSHOTS/04-cross-platform-held.png`
- `SCREENSHOTS/05-technical-receipts.png`
- `SCREENSHOTS/06-public-boundary.png`
