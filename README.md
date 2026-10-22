# Auctores for Claude

Ask Claude about your hotel's [Auctores](https://www.auctores.ai) data in plain language: expected occupancy after predicted cancellations and no-shows, bookings likely to cancel, where cancellations come from, recovered revenue, and why extra availability changed.

## What this plugin contains

- **Auctores connector**: the remote MCP server at `https://mcp.auctores.ai/mcp` (22 read-only tools).
- **Five skills** that guide Claude through common hotel workflows:
  - `auctores-hotel-briefing`: the coming days, Smart Overbooking suggestions, data freshness and prediction accuracy.
  - `auctores-reservation-risk-review`: bookings most likely to cancel or not show up.
  - `auctores-cancellation-analysis`: Cancellation Intelligence patterns by channel, room type, stay profile, season and timing.
  - `auctores-recovery-report`: recovered revenue for a period, with the bookings behind it.
  - `auctores-availability-explanation`: why extra availability changed, using strategy, paused dates and recorded PMS updates.

## What it connects to and sends

- The plugin talks only to the Auctores MCP server at `https://mcp.auctores.ai/mcp`.
- You sign in with your Auctores account. Sign-in uses Auctores' OAuth server (Supabase Auth) and the consent page at `app.auctores.ai`.
- Claude sends the parameters of your question (hotel, date range, filters) to the MCP server. The server returns only data your Auctores account already sees in the app: expected occupancy, Smart Overbooking suggestions, reservation IDs, stay dates, room types, risk scores, cancellation statistics and recovered revenue. No guest names, email addresses or phone numbers.
- Everything is read-only. The plugin cannot change your availability, strategy, Auto Apply setting or anything in your PMS. It runs no local code and stores nothing.

## Install

- **Claude (web, desktop, mobile):** add Auctores from the Claude directory, or upload this plugin under Customize → Plugins.
- **Claude Code:**

  ```
  /plugin install auctores --marketplace Auctores-ai/auctores-ai-plugin
  ```

Then connect the Auctores connector and sign in with your Auctores account.

## Requirements

An Auctores account with a hotel connected through its PMS (apaleo or Mews) and set up in Auctores. Cancellation Intelligence through this plugin is currently available for apaleo hotels.

## Example prompts

- Brief me on the next two weeks for my hotel.
- Which bookings arriving next week are most likely to cancel or not show up?
- Which booking channels have the highest cancellation rate, and how close to arrival do guests cancel?
- How much revenue did Auctores recover for us last month, and which bookings are behind it?
- Why is no extra availability suggested for my hotel on a specific date?

## Support

Questions or problems: info@auctores.ai. Privacy policy: https://app.auctores.ai/overbooking/privacy

## License

Copyright (c) 2026 Auctores Technologies OÜ. All rights reserved. See [LICENSE](LICENSE).
