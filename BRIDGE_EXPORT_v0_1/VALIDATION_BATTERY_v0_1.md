# VALIDATION_BATTERY_v0_1

**Schema:** `DIGITAL_MYCELIUM_STANDARD_BRIDGE_EXPORT v0.1`  
**Purpose:** manual validation battery for bridge export packets

## Lockline

> **AI helps people generate. Digital Mycelium helps the artifact carry forward.**

Bridge Export v0.1 gives that carry-forward route a packet shape.

## Validation target

A v0.1 bridge packet should validate as one of:

```text
BRIDGE_EXPORT_PACKET_STUB_HELD
STRAINED
REPAIRING
CONFLICT
QUARANTINED
MUST_STOP
```

`BRIDGE_EXPORT_PACKET_STUB_HELD` means the packet is structurally intact and intake-ready. It does not mean final content settlement.

## Required directory checks

A packet should contain:

```text
PACKET_ROOT/
  dm_bridge_export.json
  README_carry_forward.md
  source/
  receipts/
  boundaries/
```

Optional:

```text
optional/
  screenshots/
  witness_commentary/
  notes/
```

### Directory validation

| Check | Pass condition | Fail state |
|---|---|---|
| `dm_bridge_export.json` exists | file exists and parses as JSON | `MUST_STOP` if absent |
| `README_carry_forward.md` exists | file exists | `STRAINED` |
| `source/` exists | directory exists | `CONFLICT` if manifest lists source files |
| `receipts/` exists | directory exists | `STRAINED` |
| `boundaries/` exists | directory exists | `STRAINED` |

## JSON required-field checks

`dm_bridge_export.json` must include:

```text
schema_name
schema_version
packet_id
packet_kind
created_at_utc
product_line
source_tool_tag
source_route_ref
prompt_or_seed_ref
artifact_manifest
cohort_hash
lineage
authority
boundary_declaration
receipt_stub
target_intake
```

### Required values

```text
schema_name == DIGITAL_MYCELIUM_STANDARD_BRIDGE_EXPORT
schema_version == 0.1
product_line == AI helps people generate. Digital Mycelium helps the artifact carry forward.
```

If `schema_name` or `schema_version` is wrong, state is `CONFLICT`.

## Artifact manifest checks

For each `artifact_manifest` entry:

| Field | Required |
|---|---:|
| `artifact_id` | yes |
| `path` | yes |
| `role` | yes |
| `source_return_role` | yes |
| `kind` | yes |
| `size_bytes` | yes |
| `sha256` | yes |
| `included_in_cohort_hash` | yes |

For each listed file:

```text
1. Path must be relative.
2. Path must not escape the packet root.
3. File must exist.
4. File size must match size_bytes.
5. SHA-256 must match sha256.
```

Failure mapping:

```text
Missing listed file: CONFLICT
Hash mismatch: CONFLICT
Size mismatch: CONFLICT
Unsafe path traversal: MUST_STOP
Private key / token / secret detected: QUARANTINED
```

## Cohort hash recomputation

Canonical v0.1 rule:

```text
1. Select artifact_manifest entries where included_in_cohort_hash is true.
2. Sort selected entries by path using bytewise lexicographic order over UTF-8 path strings.
3. For each selected entry, create one line:
   path|sha256|size_bytes
4. Join lines with LF and no trailing newline.
5. Compute SHA-256 over UTF-8 bytes of that canonical text.
```

Validation:

```text
computed_cohort_hash == cohort_hash.value
```

Failure:

```text
Mismatch: CONFLICT
```

## Authority checks

The `authority` object must preserve the separation between receipts and AI commentary.

Required:

```text
authority.ai_role == optional_witness_commentary_only
authority.hashes_verify_file_continuity_only == true
authority.semantic_correctness_not_proven_by_hash == true
```

Recommended:

```text
authority.held_decider == deterministic_receipts_and_digital_mycelium_intake
authority.external_llm_required == false
authority.gpu_required == false
authority.network_required_during_deterministic_route == false
```

Failure mapping:

```text
AI output claims to decide HELD: MUST_STOP
Hashes claimed to prove semantic correctness: MUST_STOP
External LLM required but not disclosed: STRAINED or CONFLICT
```

## Boundary checks

`boundary_declaration.denied_claims` should include at least:

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

Required:

```text
boundary_declaration.content_settlement_denied == true
boundary_declaration.human_review_required == true
```

Failure mapping:

```text
Missing boundary declaration: STRAINED
Missing high-stakes denied claims: STRAINED
Packet claims final content settlement: MUST_STOP
Packet claims endorsement without evidence: MUST_STOP
```

## Receipt stub checks

Required:

```text
receipt_stub.state exists
receipt_stub.intake_ready is boolean
receipt_stub.generated_at_utc exists
receipt_stub.notes include final settlement boundary
```

Recommended state:

```text
BRIDGE_EXPORT_PACKET_STUB_HELD
```

Failure mapping:

```text
Receipt stub absent: STRAINED
Receipt claims final HELD without intake: CONFLICT or MUST_STOP
```

## Target intake checks

Required:

```text
target_intake.intended_receiver exists
target_intake.compatible_route exists
target_intake.can_reenter_digital_mycelium == true
target_intake.suggested_next_action exists
```

Failure mapping:

```text
No target intake: STRAINED
Cannot re-enter Digital Mycelium: STRAINED unless intentional
False target intake claim: CONFLICT
```

## State definitions

### BRIDGE_EXPORT_PACKET_STUB_HELD

Use when:

```text
All required files exist.
All hashes match.
Cohort hash recomputes.
Boundaries are present.
Authority is separated.
No false settlement is introduced.
Packet is intake-ready.
```

### STRAINED

Use when:

```text
The artifact remains inspectable, but context is incomplete.
A recommended file is missing.
Boundary wording is incomplete but not misleading.
Prompt/seed reference is unavailable but disclosed.
```

### REPAIRING

Use when:

```text
Packet can be repaired by adding missing context, boundaries, receipts, or safe redactions.
```

### CONFLICT

Use when:

```text
Hashes disagree.
Manifest and files disagree.
Route claims conflict.
Lineage claims conflict.
Cohort hash fails.
```

### QUARANTINED

Use when:

```text
Packet contains private paths, secrets, account data, tokens, private keys, unsafe sensitive material, or material that should not be publicly carried.
```

### MUST_STOP

Use when:

```text
Packet attempts endorsement laundering.
Packet attempts false settlement.
Packet claims AI output is authoritative.
Packet claims hashes prove truth/safety/semantic correctness.
Packet attempts malicious carry-forward.
Packet makes unsupported high-stakes claims.
```

## Manual validation checklist

```text
[ ] dm_bridge_export.json exists and parses.
[ ] schema_name matches.
[ ] schema_version matches.
[ ] packet_id exists.
[ ] created_at_utc exists.
[ ] product_line lockline exists.
[ ] source_tool_tag exists.
[ ] source_route_ref avoids private secrets.
[ ] prompt_or_seed_ref exists or unavailable is disclosed.
[ ] artifact_manifest is non-empty.
[ ] every listed path is relative and safe.
[ ] every listed file exists.
[ ] every listed size_bytes matches.
[ ] every listed SHA-256 matches.
[ ] cohort_hash recomputes.
[ ] lineage object exists.
[ ] authority object exists.
[ ] AI role is witness commentary only.
[ ] hashes verify file continuity only.
[ ] semantic correctness is not claimed by hash.
[ ] boundary_declaration exists.
[ ] denied_claims include high-stakes boundaries.
[ ] content_settlement_denied is true.
[ ] human_review_required is true.
[ ] receipt_stub exists.
[ ] final HELD settlement is not claimed prematurely.
[ ] target_intake exists.
[ ] can_reenter_digital_mycelium is true.
[ ] no false endorsement, no false settlement, no hidden authority transfer.
```

## Final validation statement template

```text
VALIDATION_STATE:
BRIDGE_EXPORT_PACKET_STUB_HELD

REASON:
The packet preserved minimum source-return structure, file continuity, boundary declaration, authority separation, and target intake route. This is intake-ready only. Final HELD settlement must be earned through the receiving intake route.
```
