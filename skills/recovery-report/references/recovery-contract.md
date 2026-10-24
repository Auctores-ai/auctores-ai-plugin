# Impact and recovery detail

## Different date selectors

| Meaning | `get_impact_report.date_reference` | `get_recovery_reservations.date_reference` |
| --- | --- | --- |
| Arrival cohort | `arrival` (observed source value) | `arrival_date` |
| Booking creation cohort | `booking` (observed source value) | `booking_date` |
| Departure cohort | Only if a corresponding value is actually returned; do not assume support | `departure_date` |

Impact accepts a source string, not a calendar date. Reuse the returned value if the source differs. All-time impact does not apply `date_reference`. Weekly/monthly rows use `date` for bucket start; a requested month is normally its first-day bucket. Arbitrary partial-week/month totals cannot be reconstructed from full buckets. Detail filters include the entire end date.

To compare with the Auctores app: its monthly/weekly KPI cards use the latest matching bucket, while the tool's combined metrics cover all returned rows within one group. Compare that specific row's metrics with the card. The app's all-time charts still use weekly/monthly history; an all-time total alone does not reproduce those series.

## Inspect before totaling

Impact returns source `rows`, per-row `metrics`, separate `groups`, top-level `metrics`/`chart`, `definitions`, `data_quality`, `aggregate_scope: returned_rows` and `possibly_truncated`. Each group has a date basis, currency, count, metrics and chart. Combined metrics/chart are supplied only for one unambiguous group. Weekly/monthly basis groups can represent overlapping populations; do not total them or add all-time plus monthly rows. If `groups` and `definitions` are absent, the server is using the older contract: explain that the updated impact endpoint is needed instead of attempting to repair its combined metrics in the skill.

The server keeps currencies separate and leaves unknown currency null. Groups with missing currency or missing weekly/monthly date basis retain raw rows but no aggregate. Explain the source gap; do not supply a currency or total it yourself. For a requested subset of valid period rows within one group, use unrounded row amounts then round for display; chart amounts may already be rounded.

Source impact counts distinguish checked-in/realised, cancelled and confirmed. `realization_rate` is the settled-booking rate, checked-in / (checked-in + cancelled), matching the Auctores app's denominator. `checked_in_share_of_total` includes future bookings and is separately named. Both are null when their denominator is zero. Use the returned definitions; date-filtered calculations must keep the same group and denominator.

Recovery detail returns `data` rows, `filters`, `interpretation` and `pagination`. It contains reservation ID, booking/arrival/departure dates, currency, `total_gross_amount` and `checked_in`. An ID filter is exact, unlike at-risk search. False does not distinguish future, cancelled, no-show or other outcomes. Group gross amounts by currency and report them as gross booking values; realised recovered revenue comes from the impact report.

Do not expect detail and impact totals to agree until date basis, time window, population, pagination, currency and source refresh align. The tools do not expose a complete current-status reconciliation or cash/ledger audit. Missing matching evidence should remain a stated limitation.
