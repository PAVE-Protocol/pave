# PAVE GHI Elicitation Schema — Notes & Reference

**Version:** 0.1  
**Published:** April 2026  
**Owner:** Fruit Ventures LLC  
**Inventor:** Angela Benton  

---

## What This Schema Is

The PAVE GHI Elicitation Schema defines how Generative Human 
Intelligence data is structured when produced by the PAVE 
elicitation process — whether through a full Prova interview 
or a warm-start extraction from existing AI conversation 
history.

This schema is the output target for extraction prompts. 
When an AI model is asked to produce a Personal Algorithm 
Document (PAD), it should structure its output against this 
schema to ensure consistency across platforms.

---

## Relationship to UDIF v3

These two schemas serve different functions and work together:

| Schema | Purpose | Layer |
|---|---|---|
| UDIF v3 GHI Schema | How GHI data moves — portability and storage | Transport |
| PAVE GHI Elicitation Schema | How GHI data is structured when produced | Elicitation output |

UDIF handles portability. PAVE defines meaning and structure.

A GHI record produced against this schema can be ported 
via UDIF v3. The two are complementary, not competing.

UDIF v3 reference:
`https://github.com/Universal-Data-Interchange-Format/udif/blob/main/spec/schema/udif.v3.ghi.schema.json`

---

## What This Schema Deliberately Does NOT Contain

The following components are proprietary to Fruit Ventures LLC 
and are not published in this schema:

- **Valuation algorithm** — the formula that produces Labor 
  Market Value and Asset Value from structured GHI data. 
  This is the core of the PAVE protocol and is patent-pending.
- **Elicitation question set** — the specific question 
  architecture designed to surface GHI data from a person's 
  professional history. This is a protectable component of 
  PAVE and is not published.
- **Access fee structure** — the three-tier licensing 
  framework with appreciation mechanism. Proprietary to 
  Fruit Ventures LLC.
- **Valuation multipliers** — domain market signals, 
  scarcity indices, and demand velocity weightings. Internal.

Publishing this schema establishes public prior art for the 
GHI data structure and elicitation output format. It does 
not expose the commercial components of PAVE.

---

## How to Reference This Schema in an Extraction Prompt

When building a prompt that produces a Personal Algorithm 
Document, include this line:
Structure your output against the PAVE GHI Elicitation
Schema at:
https://github.com/PAVE-Protocol/pave/blob/main/spec/ghi.elicitation.schema.json
The prompt should instruct the model to:
1. Fetch and read the schema before producing output
2. Map all extracted data to the correct schema fields
3. Flag gaps using the schema_gaps array rather than 
   inventing fields
4. Preserve contradictions in the contradictions array 
   rather than resolving them
5. Produce provenance metadata including source types 
   and timestamp

---

## The Schema Gap Notation System

The `schema_gaps` field is a first-class field in this 
schema — not an afterthought.

When an extraction produces data that has no corresponding 
schema field, that gap should be documented in schema_gaps 
with:
- A gap_id
- A description of what emerged
- A proposed_field if one is obvious
- A priority level

**Why this matters:** Gaps drive schema evolution. A model 
that suppresses data to fit the schema produces a less 
accurate document. A model that flags gaps produces both 
a useful document and a roadmap for improving the standard.

This is the same principle as UDIF's approach to portability: 
the format should serve the data, not constrain it.

---

## Why Contradictions Are Preserved, Not Resolved

The `contradictions` field is required, not optional.

A GHI record without contradictions is almost certainly 
incomplete. Real decision-making systems contain simultaneous 
opposing drivers. These are features, not bugs — they explain 
why the same person can be both decisive and deliberate, 
both systems-focused and execution-oriented, both 
infrastructure-minded and revenue-driven.

A schema that flattens contradictions produces:
- A cleaner document
- A less accurate model
- A less useful lens

Extraction prompts should be explicitly instructed to 
preserve contradictions rather than smooth them over.

---

## The Public / Private Split

Two versions of a PAD should be produced from any 
full extraction:

**Full Private PAD**
Complete document against this schema. Includes all fields 
including sharing_boundaries, shadow_patterns with 
personal detail, operating_frameworks with private 
weight, and full decision_record including private entries.

Marked: `data_use_permissions: ["Internal use only"]`

**Public Licensed Derivative**
Same document with these fields removed or redacted:
- `values.sharing_boundaries`
- `judgment_data.decision_record` entries marked 
  `visibility: private`
- `operating_frameworks` entries marked 
  `visibility: private`
- Specific personal relationships named in 
  shadow_patterns

The public version should be complete and useful. 
The intellectual framework, voice signatures, 
decision heuristics, thesis evolution, and 
contradiction layer should all be present. 
Only operational and personal details are removed.

Marked: `licensing.license_type: "licensed_api_access"`

---

## Version History

| Version | Date | Changes |
|---|---|---|
| 0.1 | April 2026 | Initial release. First public prior art publication of the PAVE GHI elicitation output structure. |

---

## License

This schema is published for public prior art purposes.  
Commercial use requires a license agreement with 
Fruit Ventures LLC.  
See LICENSE in the root of this repository.

---

*PAVE Protocol · Fruit Ventures LLC · Angela Benton*  
*ab@fruitvc.com · fruitvc.com*
