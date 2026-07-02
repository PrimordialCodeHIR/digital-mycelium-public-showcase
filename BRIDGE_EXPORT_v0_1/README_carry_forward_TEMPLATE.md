# README Carry-Forward Template

> **AI helps people generate. Digital Mycelium helps the artifact carry forward.**

This README travels with a Bridge Export v0.1 packet. It gives human reviewers enough context to inspect the route without relying on memory, hidden chat context, or private local state.

## 1. Packet identity

**Packet ID:** `REPLACE_WITH_PACKET_ID`  
**Packet kind:** `artifact_carry_forward_packet`  
**Created at UTC:** `YYYY-MM-DDTHH:MM:SSZ`  
**Prepared by / steward:** `REPLACE_WITH_NAME_OR_HANDLE`  

## 2. What this packet carries

Describe the carried artifact in plain language.

```text
Example:
This packet carries an AI-assisted code artifact produced during a local build session. It preserves the source file, prompt/seed reference, boundary declaration, receipt stub, and target intake route so the artifact can be reviewed without becoming orphaned output.
```

## 3. Source route

Where did this artifact come from?

```text
Tool / surface:
Route kind:
Public route or safe path hint:
Private details intentionally omitted:
```

Do not include secrets, private absolute paths, wallet keys, API tokens, personal account data, or other sensitive material.

## 4. Prompt, seed, or origin instruction

How is the origin instruction preserved?

```text
Mode:
- embedded
- local_ref
- hash_only
- redacted
- unavailable

Reference:
SHA-256 if available:
Disclosure note:
```

## 5. Carried files

List the main carried files and their roles.

```text
source/example.ext
- role:
- source-return role:
- SHA-256:
- size_bytes:
```

The formal file list belongs in `dm_bridge_export.json`.

## 6. What should carry forward

List the important anchors that must not be lost.

```text
Preserved anchors:
- source artifact identity
- boundary declaration
- source-return note
- receipt state
- target intake route
```

## 7. What changed

Describe any transformation, patch, translation, remix, compression, or derivative step.

```text
Transformed elements:
- REPLACE_WITH_DESCRIPTION
```

If no transformation occurred, write:

```text
No transformation declared. This packet only preserves carry-forward context.
```

## 8. Boundary summary

This packet does not claim final settlement.

It does not claim:

- consciousness;
- biological life;
- AGI;
- institutional endorsement;
- legal conclusion;
- medical conclusion;
- clinical validity;
- forensic conclusion;
- security guarantee;
- safety guarantee;
- semantic correctness;
- content settlement.

Hashes verify file continuity only. They do not prove semantic correctness.

## 9. Authority model

```text
Deterministic receipts govern.
AI witness commentary is optional and non-authoritative.
Final HELD settlement must be earned through the receiving intake route.
```

## 10. Suggested next action

```text
Run this packet through Digital Mycelium intake or a compatible receiver.
Verify listed hashes.
Recompute cohort hash.
Review boundaries.
Compare returned receipts against this bridge export packet.
```

## 11. Steward note

```text
This packet was emitted with carry-forward structure so the next builder does not start from zero.
```
