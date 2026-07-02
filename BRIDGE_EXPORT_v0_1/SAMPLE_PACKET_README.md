# SAMPLE_PACKET_README

This file explains how to build and inspect the first Bridge Export v0.1 sample packet.

## Recommended first sample

Use an existing Digital Mycelium artifact that already has a held receipt.

Recommended candidate:

```text
Digital_Mycelium_v0_3_OPTIONAL_OLLAMA_WITNESS_MANIFEST_PHASE_SEAL.zip
```

Known SHA-256 from prior project state:

```text
67631359D0BA30EB3BC0F4D436F1B984CEA5B794136F9F7BB3934CCF4CF1D2AB
```

Known state:

```text
DIGITAL_MYCELIUM_v0_3_OPTIONAL_OLLAMA_WITNESS_MANIFEST_PHASE_SEAL_HELD
```

## Sample packet layout

```text
sample_packet/
  dm_bridge_export.json
  README_carry_forward.md
  source/
    Digital_Mycelium_v0_3_OPTIONAL_OLLAMA_WITNESS_MANIFEST_PHASE_SEAL.zip
  receipts/
    prior_receipt_or_manifest.md
  boundaries/
    BOUNDARY_DECLARATION.md
  optional/
    screenshots/
    witness_commentary/
    notes/
```

## What the sample demonstrates

The sample should demonstrate:

```text
artifact leaves prior route
artifact is wrapped with source-return context
artifact hash is preserved
artifact boundaries travel with it
artifact can be handed to another builder or receiver
artifact can re-enter Digital Mycelium intake
```

## What the sample does not demonstrate

The sample does not prove:

```text
commercial production readiness
legal compliance
medical validity
scientific settlement
security certification
platform endorsement
AI authority
```

It demonstrates a carry-forward route.

## Sample source-return statement

```text
This sample packet wraps a prior Digital Mycelium held artifact as a Bridge Export v0.1 packet. The purpose is to preserve source-return, boundary declaration, receipt context, and target intake so the artifact can be inspected by another builder without becoming orphaned output.
```

## Sample authority statement

```text
Deterministic receipts govern.
AI witness commentary is optional and non-authoritative.
Hashes verify file continuity only.
Final HELD settlement must be earned through the receiving intake route.
```

## Sample validation target

Expected result if all checks pass:

```text
BRIDGE_EXPORT_PACKET_STUB_HELD
```

Reason:

```text
The packet preserved minimum source-return structure, file continuity, boundary declaration, authority separation, and target intake route.
```

## Future sample candidates

Additional samples can later include:

```text
proof_of_pressure_gemini_grok_source_return
hir_spu_quantum_music_architecture_translation
willow_hir_cross_language_source_return
audible_lineage_layer_examples
```

These should remain samples or parking-lot items until they are converted into canonical Bridge Export packet structure.
