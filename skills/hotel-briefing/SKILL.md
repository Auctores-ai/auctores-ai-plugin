---
name: hotel-briefing
description: Brief a hotel team on the coming days or weeks from Auctores: expected occupancy after likely cancellations and no-shows, Smart Overbooking suggestions (extra rooms to offer), data freshness and prediction accuracy. Use for the daily revenue meeting and forward planning; not a market-demand forecast or a list of individual bookings at risk.
---

# Hotel briefing

Read [common guidance](references/common.md) before using the tools. Produce a useful hotel briefing grounded in the requested period.

## Choose the useful view

- For a broad “how are we doing?” or revenue-meeting brief, use `get_report_summary` and `get_data_freshness`. The summary's recommendation/impact sections may cover the full stored history, not the requested fortnight.
- For “what should I review next week?” or a specific occupancy/extra-availability chart, start with freshness and `get_overbooking_timeline` using explicit `date_from`, `date_to`, `limit`, and optional `room_type`. Skip a broad summary when it adds no value.
- Use `get_overbooking_recommendations` for a concise allowance table, `get_room_category_report` for category-specific cancellation/arrival context, and `get_overrides_overview` only when overrides matter. Omit `room_type` for property-wide requests. Follow pagination when a whole-period total is required.
- Use `get_latest_overbooking_report` only for a requested underlying raw snapshot. `get_latest_model_run` or `list_model_runs` can explain a run-history follow-up; neither refreshes the model.
- For prediction-quality questions, read [accuracy interpretation](references/accuracy.md) and use `get_accuracy_report`. Keep quality warnings from an existing summary visible even if no extra accuracy call is needed.

## Interpret the outlook

Projected occupancy is cancellation-adjusted **current bookings**, not a forecast of all future demand. Suggested overbooking is model/strategy advice, not proof of a PMS update or rooms that will sell. Extra availability is most useful when demand exists on busy dates; cancellation risk alone cannot demonstrate that demand.

Use returned daily rows to identify a few dates worth review, explaining capacity, current bookings, predicted cancellations and suggested allowance where available. Do not invent an “optimal” cap, strategy percentage or guarantee. Date sums are room-nights, not unique guests/bookings or a same-night allowance; do not add a property total to category rows. Room-category data lacks the full property's capacity and allowance fields.

Check coverage before operational advice. If the report ends before the requested period, lead with that gap. A historical explanation may still be useful when clearly dated. Configuration changes, Auto Apply and PMS actions require separate evidence and cannot be executed through these tools.

## Answer

Give the main takeaway with property, dates, successful snapshot date and latest attempt status when material. For supported dates, a short table can show date, expected occupancy/cancellation risk, suggested extra rooms and reason to review. State relevant gaps or uncertainty and the most useful next review; do not turn every brief into a full report.
