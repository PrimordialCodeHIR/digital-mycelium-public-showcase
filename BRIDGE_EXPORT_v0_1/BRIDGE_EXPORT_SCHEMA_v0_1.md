# DIGITAL_MYCELIUM_STANDARD_BRIDGE_EXPORT v0.1

**Status:** repo-ready draft  
**Packet type:** source-return / carry-forward bridge packet  
**Primary audience:** AI-assisted builders, researchers, artifact stewards, and Digital Mycelium-compatible receivers

## Lockline

> **AI helps people generate. Digital Mycelium helps the artifact carry forward.**

Bridge Export v0.1 gives that carry-forward route a packet shape.

## Purpose

Bridge Export v0.1 is a small, survivable source-return envelope.

Its purpose is to let generated artifacts leave code assistants, local folders, GitHub handoffs, Hugging Face packages, or other tool surfaces without becoming orphaned outputs.

It does not settle the truth of the content. It preserves the route so later review can happen honestly.

## Core problem

AI-assisted work often fails during carry-forward:

- prior work gets dropped;
- files silently disappear;
- context gets overwritten;
- patches rupture the app body;
- generated outputs become detached from source;
- another builder cannot inspect the route;
- the original human has to reconstruct the trail by hand.

Bridge Export v0.1 is the first minimal road for preventing that rupture.

## Recommended packet layout

```text
PACKET_ROOT/
  dm_bridge_export.json
  README_carry_forward.md
  source/
  receipts/
  boundaries/
  optional/
    screenshots/
    witness_commentary/
    notes/
```

For repo templates, use:

```text
BRIDGE_EXPORT_v0_1/
  BRIDGE_EXPORT_SCHEMA_v0_1.md
  dm_bridge_export.example.json
  README_carry_forward_TEMPLATE.md
  BOUNDARY_DECLARATION_TEMPLATE.md
  VALIDATION_BATTERY_v0_1.md
  SAMPLE_PACKET_README.md
```

## Canonical JSON object

A v0.1 bridge packet is centered on `dm_bridge_export.json`.

Required top-level fields:

| Field | Required | Purpose |
|---|---:|---|
| `schema_name` | yes | Must equal `DIGITAL_MYCELIUM_STANDARD_BRIDGE_EXPORT` |
| `schema_version` | yes | Must equal `0.1` |
| `packet_id` | yes | Human-readable packet identifier |
| `packet_kind` | yes | Type of bridge packet |
| `created_at_utc` | yes | ISO-8601 UTC timestamp |
| `product_line` | yes | Public wedge / lockline |
| `source_tool_tag` | yes | Tool/source context without endorsement claim |
| `source_route_ref` | yes | Safe route reference |
| `prompt_or_seed_ref` | yes | Origin instruction, seed, prompt, or hash reference |
| `artifact_manifest` | yes | List of carried artifacts with hashes |
| `cohort_hash` | yes | Manifest-level portable anchor |
| `lineage` | yes | Parent packets, source refs, route events |
| `authority` | yes | Authority separation: deterministic receipts vs AI witness |
| `boundary_declaration` | yes | What the packet does and does not claim |
| `receipt_stub` | yes | Intake-ready closure receipt, not final settlement |
| `target_intake` | yes | Intended receiving route |

## `schema_name`

Must be:

```text
DIGITAL_MYCELIUM_STANDARD_BRIDGE_EXPORT
```

## `schema_version`

Must be:

```text
0.1
```

## `packet_kind`

Recommended values:

```text
artifact_carry_forward_packet
code_assistant_output
local_folder_drop
github_handoff
huggingface_package_handoff
manual_wrapper
source_return_addendum
translation_route_addendum
```

Additional values may be introduced later, but v0.1 receivers should treat unknown kinds as `artifact_carry_forward_packet` unless they conflict with boundaries.

## `source_tool_tag`

Identifies the tool or context that produced or carried the artifact.

Example:

```json
{
  "tool_name": "example-code-assistant",
  "tool_type": "code_assistant",
  "tool_version": "unknown_or_optional",
  "operator_note": "Human-directed AI-assisted build output"
}
```

This field does not claim endorsement by the tool, platform, model provider, or host.

## `source_route_ref`

Preserves the route without exposing private material.

Example:

```json
{
  "route_kind": "local_workspace",
  "route_label": "Example code assistant output folder",
  "uri_or_path_hint": "public-example/no-private-path",
  "privacy_note": "Public packets should not expose private local paths, tokens, account data, secrets, or private user identifiers."
}
```

## `prompt_or_seed_ref`

Preserves origin context.

Allowed modes:

```text
embedded
local_ref
hash_only
redacted
unavailable
```

Recommended example:

```json
{
  "mode": "hash_only",
  "sha256": "0000000000000000000000000000000000000000000000000000000000000000",
  "local_ref": "receipts/prompt_or_seed_ref.txt",
  "disclosure_note": "Prompt, seed, or origin instruction may be embedded, referenced, or hash-only depending on privacy and review needs."
}
```

## `artifact_manifest`

Every carried file should appear as one manifest entry.

Required manifest entry fields:

| Field | Required | Purpose |
|---|---:|---|
| `artifact_id` | yes | Stable ID inside the packet |
| `path` | yes | Relative path from packet root |
| `role` | yes | How the file participates |
| `source_return_role` | yes | Role in source-return |
| `kind` | yes | General file kind |
| `media_type` | recommended | MIME/media type |
| `size_bytes` | yes | File size in bytes |
| `sha256` | yes | SHA-256 of file bytes |
| `included_in_cohort_hash` | yes | Whether included in cohort hash |

Recommended `role` values:

```text
carried_artifact
primary_source
supporting_source
generated_output
receipt
boundary
screenshot
witness_commentary
manifest
```

Recommended `source_return_role` values:

```text
primary_payload
parent_source
child_derivative
receipt_anchor
boundary_anchor
witness_material
context_material
```

Recommended `kind` values:

```text
code
text
markdown
json
csv
html
pdf
image
audio
video
zip
dataset
other
```

## Cohort hash canonicalization

The `cohort_hash` creates one portable digest for the packet’s included manifest cohort.

Canonical rule for v0.1:

```text
1. Select artifact_manifest entries where included_in_cohort_hash is true.
2. Sort selected entries by path using bytewise lexicographic order over UTF-8 path strings.
3. For each selected entry, create one line:
   path|sha256|size_bytes
4. Join lines with LF (`\n`) and no trailing newline.
5. Compute SHA-256 over UTF-8 bytes of that canonical text.
```

The `cohort_hash.value` must equal the resulting digest.

Hashes verify file continuity. They do not prove semantic correctness, safety, legality, clinical validity, or truth.

## `lineage`

Preserves where the packet came from and what it carries forward.

Example:

```json
{
  "parent_packet_ids": [],
  "source_artifact_refs": [],
  "known_route_events": [],
  "source_return_note": "This bridge packet preserves route context so the carried artifact does not become an orphaned output."
}
```

## `authority`

This object is mandatory.

Required lock:

```text
Deterministic receipts govern.
AI witness is optional commentary only.
Hashes verify file continuity only.
Hashes do not prove semantic correctness.
```

Example:

```json
{
  "held_decider": "deterministic_receipts_and_digital_mycelium_intake",
  "ai_role": "optional_witness_commentary_only",
  "external_llm_required": false,
  "gpu_required": false,
  "network_required_during_deterministic_route": false,
  "hashes_verify_file_continuity_only": true,
  "semantic_correctness_not_proven_by_hash": true
}
```

## `boundary_declaration`

The boundary must travel with the artifact.

Required denied claim classes:

```text
consciousness claim
biological life claim
AGI claim
institutional endorsement claim
external validation claim
legal conclusion
medical conclusion
clinical validity claim
forensic conclusion
security guarantee
safety guarantee
semantic correctness claim
content settlement claim
```

A packet may add stricter boundaries.

## `receipt_stub`

A bridge export packet may be `stub-held` or intake-ready. That is not final settlement.

Recommended state:

```text
BRIDGE_EXPORT_PACKET_STUB_HELD
```

Required note:

```text
Final HELD settlement must be earned through the receiving intake route.
```

## `target_intake`

Must indicate whether the packet can re-enter Digital Mycelium or a compatible receiver.

Required:

```json
"can_reenter_digital_mycelium": true
```

## v0.1 validation states

```text
BRIDGE_EXPORT_PACKET_STUB_HELD
STRAINED
REPAIRING
CONFLICT
QUARANTINED
MUST_STOP
```

### `BRIDGE_EXPORT_PACKET_STUB_HELD`

The packet is structurally intact, hashes verify, boundaries are present, authority is separated, and it is intake-ready.

### `STRAINED`

The payload may remain inspectable, but recommended context is missing or weak.

### `REPAIRING`

The packet needs bounded repair before it can be treated as intake-ready.

### `CONFLICT`

Hashes, file paths, manifest claims, or route claims disagree.

### `QUARANTINED`

The packet includes private data, secrets, unsafe material, or an unclear route that should not be carried forward publicly.

### `MUST_STOP`

The packet attempts false settlement, endorsement laundering, hidden authority transfer, malicious carry-forward, or high-stakes overclaiming.

## What Bridge Export v0.1 does not do

Bridge Export v0.1 does not:

- determine copyright ownership;
- replace legal review;
- replace medical review;
- validate scientific claims;
- prove safety;
- prove semantic correctness;
- prove institutional endorsement;
- certify production readiness;
- replace deterministic Digital Mycelium intake;
- turn AI output into authority.

It preserves a route.

## Public explanation

> Bridge Export v0.1 is not a giant standard.  
> It is a survivable source-return envelope.  
> Its purpose is to let generated artifacts leave code assistants, local folders, GitHub handoffs, or Hugging Face packages without becoming orphaned outputs.  
> It does not settle content. It preserves the route so later review can happen honestly.

## Final lockline

> **AI helps people generate. Digital Mycelium helps the artifact carry forward.**  
> **Bridge Export v0.1 gives that carry-forward route a packet shape.**
