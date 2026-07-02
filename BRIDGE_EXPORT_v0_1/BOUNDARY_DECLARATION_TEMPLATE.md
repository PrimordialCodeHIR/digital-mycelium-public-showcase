# Boundary Declaration Template

**Packet ID:** `REPLACE_WITH_PACKET_ID`  
**Schema:** `DIGITAL_MYCELIUM_STANDARD_BRIDGE_EXPORT v0.1`  
**Boundary state:** `DRAFT / HELD / STRAINED / CONFLICT / QUARANTINED / MUST_STOP`

## Purpose

This boundary declaration travels with a Bridge Export v0.1 packet.

Its role is to prevent false settlement, endorsement laundering, hidden authority transfer, and overclaiming.

## Positive claim

This packet may claim:

```text
This packet preserves minimum source-return structure for later Digital Mycelium intake.
```

This packet may also claim, if verified:

```text
The listed files were present at packet creation time.
The listed file hashes matched at packet creation time.
The cohort hash was computed from the declared manifest canonicalization rule.
The artifact remains inspectable in source/.
```

## Denied claims

This packet does **not** claim:

- consciousness;
- biological life;
- AGI;
- institutional endorsement;
- external validation;
- legal conclusion;
- medical conclusion;
- clinical validity;
- forensic conclusion;
- security guarantee;
- safety guarantee;
- semantic correctness;
- content settlement;
- production readiness;
- platform endorsement;
- model-provider endorsement;
- copyright ownership determination;
- fair-use determination;
- investment, token, coin, or financial settlement.

## Authority model

```text
Deterministic receipts govern.
AI witness commentary is optional and non-authoritative.
Human review remains required.
```

## Hash boundary

SHA-256 hashes can verify file continuity.

SHA-256 hashes do not prove:

- truth;
- safety;
- legality;
- correctness;
- originality;
- authorship;
- clinical validity;
- scientific validity;
- semantic interpretation.

## AI witness boundary

AI outputs may be included as witness material, derivative material, or commentary.

AI outputs do not decide HELD settlement.

A model-generated explanation, song, image, review, or pressure read is not platform validation or institutional endorsement.

## Source-return boundary

The packet should preserve source-return.

The packet should not hide, erase, launder, or falsely claim parentage.

If source lineage is uncertain, mark it as uncertain.

If source lineage conflicts, mark the packet as `CONFLICT`.

If the packet contains private data or secrets, mark it as `QUARANTINED`.

If the packet attempts false settlement or endorsement laundering, mark it as `MUST_STOP`.

## High-stakes boundary

For medical, legal, forensic, security, financial, safety-critical, child-facing, or other high-stakes uses:

```text
Bridge Export v0.1 is a carry-forward envelope only.
It does not replace domain expert review.
It does not certify deployment, diagnosis, advice, legality, safety, or compliance.
```

## Final statement

This packet preserves the route so later review can happen honestly.

It does not settle the content.
