# Helix - System Requirements (v0.2)

## Source and Traceability
Primary source: `Quotation_Helix_Printer.pdf` (dated content references year 2025).
Extracted source text: `docs/quotation_extracted.txt`.

Note: Page 2 of the PDF appears to be non-selectable/graphic content in this environment. Requirements not legible from text extraction are marked `TBD` and must be completed from the original layout.

## 1) Product Scope
Helix is a dual-nozzle industrial 3D printing platform for food/meat-analogue style materials and ambient process variants.

## 2) Functional Requirements
- `FR-001` The system shall support dual-nozzle deposition.
  Source: quotation page 4, "Dual nozzle Cocuus 3D printer".
- `FR-002` The system shall provide software for machine operation.
  Source: quotation page 4, "Software included".
- `FR-003` The supplier workflow shall include installation and commissioning.
  Source: quotation page 4, footnote `*`.
- `FR-004` The service model shall support online support plus one week onsite maintenance/service.
  Source: quotation page 4, footnote `**`.

## 3) Mechanical and Process Requirements
- `PR-001` Printable area shall be at least `500 x 500 mm`.
  Source: quotation page 4.
- `PR-002` Layer height resolution target shall be `0.2 mm`.
  Source: quotation page 4.
- `PR-003` Operating pneumatic pressure shall support `6 bar`.
  Source: quotation page 3.
- `PR-004` Machine mass reference shall be approximately `375.5 kg`.
  Source: quotation page 3.

## 4) Electrical Requirements
- `ER-001` Installed power reference shall be `1.5 kW`.
  Source: quotation page 3.
- `ER-002` Electrical supply shall be `3 x 400 V`.
  Source: quotation page 3.

## 5) Software and IT Requirements
- `SR-001` Operator workstation software shall run on Windows 10 (64-bit).
  Added by customer request on 2026-03-12.
- `SR-002` Operator workstation software shall run on Windows 11 (64-bit).
  Added by customer request on 2026-03-12.
- `SR-003` Klipper host runtime shall run on Linux (CB1/CM4/Raspberry Pi OS class environment).
  Engineering baseline: native Klipper deployment model.
- `SR-004` Remote support workflow shall be compatible with standard Windows 10/11 corporate environments (firewall/proxy-aware where possible).
  Added by engineering for operability.
- `SR-005` Software deliverables shall include installation instructions for both Windows 10 and Windows 11 operator stations.
  Added by engineering for deployment quality.

## 6) Compliance Requirements
The machine and electrical system shall conform to the cited directives/norms:
- `CR-001` 1644/2008 (Rules for marketing and implementation in service of machines).
- `CR-002` 2006/42/EC (Machinery Directive).
- `CR-003` 2014/30/EU (EMC regulation).
- `CR-004` 2014/35/EN (Low Voltage Directive).
- `CR-005` UNE-EN ISO 12100:2012.
- `CR-006` EN ISO 13849-1:2016.
- `CR-007` EN ISO 13849-2:2013.
- `CR-008` EN 349:1994 +A1:2008.
- `CR-009` EN 7731:2008.
Source: quotation page 3.

## 7) Commercial Constraints (Reference)
- Quotation validity: `90 days`.
- Payment terms: `35% downpayment`, `40% before shipment`, `25% after commissioning`.

## 8) Open Items (TBD from page 2 artwork)
- Full machine envelope dimensions.
- Axis speeds/accelerations from original table.
- Detailed utility requirements beyond power and pressure.
- Any environmental limits (temperature, humidity, IP rating).

## 9) Change Log
- `2026-03-12` v0.2: Added Windows 10/11 client requirements and explicit Linux Klipper host requirement.
- `2026-03-12` v0.1: Initial requirements baselined from quotation + customer OS request.
