---
name: cancellation-analysis
description: Analyse historical hotel cancellation and no-show patterns with Auctores Cancellation Intelligence: rates by channel, room type, travel purpose, stay profile, season and timing (booking window, how close to arrival guests cancel). Use for comparisons and "where do our cancellations come from?" questions; not predictions for individual bookings or proof of why guests cancel.
---

# Cancellation analysis

Read [common guidance](references/common.md). Choose only the analytical views needed for the question.

## Tool and period selection

| Question | Tool and supported inputs |
| --- | --- |
| Which channels, categories, purposes or stay profiles? | `get_cancellation_breakdown`; `period: history\|current_year` |
| How has the rate changed; what is seasonal? | `get_cancellation_trends`; `period: history\|last_year`, `date_from`, `date_to`, `reference_date`, `seasonality: month\|week` |
| How early are bookings made or cancellations made? | `get_cancellation_timing`; `period: history\|current_year`, `dimension: lead_time\|days_before_arrival\|days_blocked` |

All need the composite property scope. Analytics currently supports Apaleo and BeSafe; other Auctores/PMS features may still work for other vendors. Use an already known vendor or `get_overbooking_task` if needed; honor `UNSUPPORTED_ANALYTICS_VENDOR` and source availability. Do not replace unavailable history with reservation predictions.

Breakdown/timing have no arbitrary date-range filter: do not claim an exact last-month channel/timing analysis from all-history rows. Explain that limit and use supported periods, or trends for a date-bounded overall comparison. `current_year` selects source bucket 1; `history` includes nonnegative source year buckets. If exact calendar coverage is absent, say so.

Trends use completed UTC **arrival weeks**, not the dates cancellations were processed. State the returned week coverage and excluded current week. `last_year` means a trailing year relative to `reference_date`, not the previous calendar year. Date filters select week-start dates; do not present partial-month selections as exact calendar-month reservation counts.

## Metric interpretation

- Cancellation rate = cancelled / finalized; no-show rate = no-shows / finalized. Use the stored finalized denominator, not confirmed bookings or all visible rows. Preserve null for zero denominators and show counts/sample size.
- Use the selected summary/breakdown rollup. Never add summary, channel, room and detail rows together. A missing unambiguous total stays unavailable even if some breakdowns are usable.
- “Most cancellations” can mean volume; “highest rate” means frequency within a group's finalized sample. Clarify through labels, and highlight very small samples rather than declaring their apparent rank representative. Cancellation plus no-show rate must be labeled combined.
- Four-week rolling rates are weighted by finalized counts within a 21-day lookback plus the current point; missing weeks are not zero observations. Seasonal `average_rate` is the unweighted mean of available yearly rates, not a pooled hotel rate.
- Timing bucket IDs are source codes. Use returned labels (0-3, 4-7, 8-14, 15-30, 31+ days). For lead time, report cancellation rate; for days before arrival or inventory days blocked, cancellation share usually answers the question. Label its denominator: cancellations across included buckets. Surface excluded rows when they affect completeness.
- Retain `quality_warning`, warnings and `available: false` sections. Source/model timestamps do not establish analytics refresh time.
- Compare like periods, dimensions and denominators. Differences describe association; they do not establish that a channel, campaign or policy caused cancellations.

## Answer

Lead with the largest supported pattern and period. Use a compact table with cancellations, finalized reservations and rate (or cancellations and share for timing). Explain sample/coverage limits next to the finding. Recommend a review question grounded in the evidence; do not claim to have changed channel policy or prices.
