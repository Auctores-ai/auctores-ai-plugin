---
name: availability-explanation
description: Explain why Auctores extra availability (Smart Overbooking) changed or was not applied on a date, using the strategy, Auto Apply setting, date-range overrides and recorded PMS updates. Use for "why did it change?" or "why was nothing applied?" questions; read-only, so it cannot change settings or confirm PMS changes that were not logged.
---

# Availability explanation

Read [common guidance](references/common.md). Build a dated evidence trail; do not infer a cause from a recommendation alone.

## Establish the question

Distinguish the **affected stay date(s)** from **when the change was observed/pushed**, plus property and room category if material. “Why did availability change yesterday?” may mean either yesterday's stay dates or a change observed yesterday for next month. Ask for the affected stay dates when they cannot be inferred.

For “what are my settings?” use `get_overbooking_task` alone unless history is requested. Explain returned parameters such as `service_level`, `write_availability`, room scope, cap and cutoff without inventing strategy percentages. Current settings do not prove past settings.

`overbooking_hard_cap_days` is the minimum advance notice for applying overbooking (5 means a five-day lead-time cutoff, not a five-room cap). `overbooking_max_value` is the maximum allowed overbooking per day; null means no explicit daily maximum, not zero. `overbook_full_property: true` makes selected `room_type_ids` irrelevant, with exclusions still meaningful. These configuration definitions do not establish the exact historical application time or an unreturned boundary rule.

## Collect only relevant evidence

1. `get_overbooking_task` gives current strategy, Auto Apply and limits; `get_data_freshness` gives the latest attempt/success and coverage.
2. `get_overrides_overview` with `date_from`/`date_to` gives grouped strategy/pause context. For historical questions, avoid a “current” status filter that would omit expired overrides. Preserve metadata availability.
3. `get_overbooking_timeline` or `get_overbooking_recommendations` gives the latest successful report's suggestion for affected dates. It is not automatically the historical recommendation that caused an older push. The timeline's legacy overlay and grouped v2 overrides are different sources; neither alone proves application.
4. `get_pms_action_logs` requires `date_from` and `date_to`; these filter **overbooking_date (affected stay date)**, not `pushed_at_utc`. Use optional `room_type`/`task_run_id` only when known. Page through matching evidence if completeness is needed; filter observation/push time locally from returned timestamps.
5. Correlate property, affected date, room/service and task run. `list_model_runs` can give bounded recent run context; it cannot reconstruct missing historical settings or an unavailable historical forecast.

## Evidence strength and response

Show a short chronology/table of affected date, event time, recommendation/override/recorded action, amount and result when present.

- A recommendation is a suggestion. An override is configuration context. A log with `success: true` is a source-recorded successful action, not a fresh PMS readback. `success: false` is a failed attempt; null means unknown. Whole-run success does not override an individual action failure.
- An amount of zero is a recorded set-to-zero action, not “no action.” Log amounts are target allowances, not additive increments; do not sum repeated pushes.
- Separate current configuration from the configuration when an action happened. Use matching historical evidence for a causal explanation; proximity in time or a similar amount alone is insufficient.
- If logs, override metadata or historical context are missing, explain exactly which cause cannot be established. An empty history is not proof that the PMS never changed or that another system did it.
- When asked to change strategy, pause Auto Apply, undo an action or push rooms, say the MCP cannot execute that change. Provide the requested explanation or a clearly unexecuted proposal; do not use a browser/database/other connector to bypass the read-only boundary.

Lead with the supported explanation and its confidence, or the specific missing evidence. Cite dated facts in plain language and distinguish confirmed records from hypotheses.
