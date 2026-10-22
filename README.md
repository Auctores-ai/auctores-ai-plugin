# Auctores for Claude

Ask Claude about your hotel's [Auctores](https://www.auctores.ai) data in plain language: upcoming occupancy after cancellations and no-shows, reservations at risk, cancellation patterns, reported recovery, and why extra availability changed.

## What this plugin contains

- **Auctores connector**: the remote MCP server at `https://mcp.auctores.ai/mcp` (22 read-only tools).
- **Five skills** that guide Claude through common hotel workflows:
  - `auctores-hotel-briefing`: briefing for the coming days, data freshness and prediction quality.
  - `auctores-reservation-risk-review`: reservations most likely to cancel or not show up.
  - `auctores-cancellation-analysis`: historical cancellation and no-show patterns by channel, room category, stay profile, season and timing.
  - `auctores-recovery-report`: recovery Auctores reports for a period, with the bookings behind it.
  - `auctores-availability-explanation`: why extra availability changed, using recommendations, overrides and recorded PMS actions.

## What it connects to and sends

- The plugin talks only to the Auctores MCP server at `https://mcp.auctores.ai/mcp`.
- You sign in with your Auctores account. Sign-in uses Auctores' OAuth server (Supabase Auth) and the consent page at `app.auctores.ai`.
- Claude sends your questions' parameters (hotel, date range, filters) to the MCP server. The server returns only data your Auctores account can already see: forecasts, recommendations, reservation IDs, stay dates, room types, risk scores, cancellation statistics and recovery amounts. No guest names, emails or phone numbers.
- Everything is read-only. The plugin cannot change availability, settings or anything in your PMS. It runs no local code and stores nothing.

## Install

- **Claude (web, desktop, mobile):** add Auctores from the Claude directory, or upload this plugin under Customize → Plugins.
- **Claude Code:**

  ```
  /plugin install auctores --marketplace Auctores-ai/auctores-ai-plugin
  ```

Then connect the Auctores connector and sign in with your Auctores account.

## Requirements

An Auctores account with at least one connected hotel (Apaleo or Mews) and Smart Overbooking set up. Cancellation pattern analysis currently covers Apaleo hotels.

## Example prompts

- Brief me on the next two weeks for my hotel.
- Which 10 reservations arriving next week are most likely to cancel or not show up?
- Which booking channels cancel most, and how close to arrival do cancellations happen?
- What recovery does Auctores report for last month, and which bookings are behind it?
- Why did the extra availability for my hotel change yesterday?

## Support

Questions or problems: info@auctores.ai. Privacy policy: https://app.auctores.ai/overbooking/privacy

## License

Copyright (c) 2026 Auctores. All rights reserved. See [LICENSE](LICENSE).
