# FlowUp / Orbyte demo

FlowUp is a human-reviewed retail operations workspace for Malaysian SMEs. It connects checkout, warehouse receiving, finance reporting, supplier performance, and owner decisions. Its calculations prepare information and recommendations; people verify records and approve consequential actions.

## Demo boundaries

- This build uses synthetic demo records only. Enterprise access accepts any valid-looking email and non-empty password, or the one-click demo shortcut; role sign-in can continue without credentials. Nothing is verified or stored. The role session is server-signed and uses the four seeded demo users.
- The demo business date starts at `2026-10-18` and is stored as a date-only Kuala Lumpur business date. It does not advance automatically with the machine clock.
- Cash, card, and DuitNow QR are recorded as cashier-selected payment methods. No bank, acquirer, or DuitNow settlement connection is configured.
- Imported historical sales are report-only; they do not create stock movements or influence live demand forecasts.
- Cashier API responses intentionally omit cost, margin, supplier-price, and profit information.
- Sensitive actions remain human decisions: finance reviews purchasing and loss/refund events; the owner handles price, promotion, and supplier-review decisions.
- No real customer payment details, personal customer records, or supplier credentials are part of the seeded dataset.

## Calculation assumptions

- The attached specification's formula says confirmed net expense equals gross order expense minus approved or settled refunds. Applied to the supplied sample, that gives RM 2,624. A later example in the same document states RM 2,600, which conflicts with the formula and the listed claims; the explicit formula takes precedence.
- The supplier formula produces 98.14% for Supplier A when calculated before rounding; the document lists 98.13%. The 0.01 percentage-point difference is within its stated ±0.01 acceptance tolerance.
- The source does not specify a pseudo-random generator seed for imported daily sales. The demo uses seed `20261018` so the generated sample is repeatable.
- Stock ledger movements are signed: receipts/opening quantities are positive; sales and write-offs are negative. Imported sales never enter this ledger.
- If the supplied workbook and the document's explicit demo values differ, the explicit section 9 values and formulas are the source for the synthetic fixture.
- Finance workbook rows are mapped, validated, and approved before reports use them. Imported stock remains a report reference and never changes on-hand inventory.

## Checks

- Pure calculation suite: `pnpm --filter @workspace/flowup-calc run test`
- Shared library typecheck: `pnpm run typecheck:libs`
- Full workspace typecheck: `pnpm run typecheck`

This is a functional demo, not a production multi-tenant identity, payment, or accounting integration.
