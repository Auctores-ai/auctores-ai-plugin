---
name: recovery-report
description: Report the room revenue Auctores recovered for a hotel and the bookings behind it, keeping realised revenue, future bookings and cancellations apart. Use for recovery reviews and booking reconciliation; not total hotel revenue, invoices or prediction accuracy.
---

# Recovery report

Read [common guidance](references/common.md) and [impact and detail contract](references/recovery-contract.md). Preserve the user's meaning of “this month”: arrival/stay cohort, booking creation, or another explicitly supported date basis.

## Retrieve and reconcile

- Use `get_impact_report` for source-reported impact: `timeframe: all_time\|weekly\|monthly`, optional `date_reference` and bounded `limit`. A calendar date is not a date-reference selector. For a month request, use monthly rows on one basis and select the requested bucket locally.
- If the user's basis is ambiguous, use a clearly stated arrival-cohort assumption for a routine overview; ask when it would materially change an accounting/reconciliation answer. “Bookings made” means booking basis. Discover actual basis values from returned rows if not known.
- Use the server's `groups` for each date basis and currency. Combined `metrics`/`chart` are null/empty when the response has multiple groups; this is not zero recovery. Choose the requested group and period, retaining `data_quality` warnings. Do not add groups from different date bases or currencies.
- Impact has no `date_from`, `date_to` or `offset`. If a filled limit prevents reaching a requested old period, increase the limit within its 1000 maximum only as needed; at the cap, state incomplete coverage. Missing period rows are unavailable, not zero recovery. Do not substitute lifetime values for this month.
- For booking evidence/export questions, use `get_recovery_reservations` with explicit dates, `date_reference`, optional `checked_in` or exact `reservation_id`, `limit` and `offset`. Follow every page for requested full totals. The detail response's `date_reference` values differ from impact's.
- Summarize detail by original currency and checked-in flag without converting currencies or inferring cancelled/pipeline status from false. Gross booking amounts and impact aggregates can differ in period, population, outcome definition or source refresh; test those explanations before comparing totals.

## What can be claimed

Use “Auctores reports ... as realised recovery” for the source's realised metric. Do not call it audited incremental revenue, cash received, profit or a proven causal effect. Checked-in status alone does not establish incrementality or payment. Do not derive fees/invoices from marketing pricing.

Separate reported realised, cancelled and confirmed/pipeline values where the source actually supplies them. Detail supplies only gross and checked-in state; it cannot reconstruct all three groups. A quality or refresh limitation remains visible even when a figure is nonzero.

Use the server's `realization_rate`: checked-in / (checked-in + cancelled), excluding pending bookings. It is null with no settled bookings. `checked_in_share_of_total` is a different measure that includes pending bookings in its denominator. Label the measure and preserve the returned definition.

## Answer

State property, exact period/date basis, currency and refresh information available for that source. Lead with source-reported recovery for that scope; show booking evidence separately and label previews. Explain any mismatch without forcing the two sources to reconcile or claiming that accuracy validates revenue.
