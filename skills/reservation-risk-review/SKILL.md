---
name: reservation-risk-review
description: Find and explain individual hotel bookings that Auctores predicts are likely to cancel or not show up, including top-risk lists by arrival, departure or stay date and reservation-ID lookups. Use for arrival and stayover reviews; not historical cancellation rates by channel or contacting guests.
---

# Reservation risk review

Read [common guidance](references/common.md). Return the bookings the user asked to review, with risk and coverage clearly labeled.

## Retrieve the right population

Use `get_at_risk_reservations` with `connection_id`, `property_id` and explicit `date_from`/`date_to`:

- “Arriving” uses `date_filter: arrival`; “departing” uses `departure`; “staying/in house during” uses `stayover`. Stayover overlap includes arrival <= end and departure >= start. For “bookings next week” without a narrower meaning, state the stayover assumption unless it materially changes the user's decision.
- Use `max_arrival_probability`, not the deprecated aliases. A requested risk of at least 70% maps to a maximum arrival probability of 0.30. If no threshold is specified, use 0.30 and say so. “Top five” requests need a small limit, not the entire portfolio.
- `reservation_id` is a case-insensitive partial search. Inspect returned IDs before claiming an exact match. For an ID-only lookup without a risk cutoff, set `max_arrival_probability: 1` so lower-risk records are not silently excluded. If it is absent, explain the applied date/status scope; do not say it does not exist in the PMS.
- Add `room_type` only when requested or already established. Dates/IDs from different connections cannot be interchanged.
- Use each row's `model_run_finished_at` for its prediction age. Check `get_data_freshness` for current operational review; rows need not share the newest successful report run. Optional `get_room_category_report` supplies category context, not missing guest data.

## Interpret and rank

Rows are ordered by lowest `arrival_probability`. Cancellation-or-no-show risk is `1 - arrival_probability`, not the probability of a definite cancellation. Keep the combined outcome label. The returned confidence tiers are threshold labels, not validation of model accuracy.

Show reservation ID, room category, arrival/departure and estimated risk in a compact ranked table. Avoid multiplying reservation probabilities by revenue or rooms unless compatible values were actually supplied.

Mention `filters.active_status_filter_available: false` if returned: the server could not apply the active-status filter, so active-booking status is unverified. `cancellation_mix` counts only returned rows by room category; it is neither a property cancellation rate nor the Auctores app's independently filtered full population.

For a requested complete list/count, follow `next_offset` with the same filters. For a top list, label it as a preview and report whether further rows may exist. Empty means no matching returned records under these filters, not zero hotel risk.

To reproduce the Auctores app's room-type chart, read all pages for its date window and threshold, omitting the table-only reservation-ID and room-type filters. Aggregate those page counts by category. To reproduce the table, apply its ID/category filters. A filtered top-five mix cannot be compared with the whole pie.

## Answer

State property, actual date mode and dates, threshold, snapshot age and list coverage. Suggest human review when appropriate, without implying a booking will cancel. This surface supplies no guest contact information and does not send outreach or change reservations.
