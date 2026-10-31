# Auctores for Claude

Put guest-arrival predictions into the way your hotel works. The Auctores plugin connects Claude to your [Auctores](https://www.auctores.ai) account, read-only, and adds five workflows: a briefing for the revenue meeting, Smart Overbooking suggestions and why availability changed, a recovered-revenue report, a review of bookings likely to cancel or not show up, and a Cancellation Intelligence analysis. Claude can use the same data, in chats and scheduled tasks, to plan front office and housekeeping staff, guest messages and marketing on the guests likely to arrive.

## What this plugin contains

- **Auctores connector**: the remote MCP server at `https://mcp.auctores.ai/mcp` (22 read-only tools).
- **Five skills:**
  - `hotel-briefing`: the coming weeks for your revenue meeting: expected occupancy, Smart Overbooking suggestions, data freshness and prediction accuracy.
  - `reservation-risk-review`: bookings most likely to cancel or not show up.
  - `cancellation-analysis`: Cancellation Intelligence patterns by channel, room type, stay profile, season and timing.
  - `recovery-report`: recovered revenue for a period, with the bookings behind it.
  - `availability-explanation`: why extra availability changed, using your strategy, date-range overrides and recorded PMS updates.

## What it connects to and sends

- The plugin talks only to the Auctores MCP server at `https://mcp.auctores.ai/mcp`.
- You sign in with your Auctores account. Sign-in uses Auctores' OAuth server (Supabase Auth) and the consent page at `app.auctores.ai`.
- Claude sends the parameters of your question (hotel, date range, filters) to the MCP server. The server returns only data your Auctores account already sees in the app: expected occupancy, Smart Overbooking suggestions, reservation IDs, stay dates, room types, risk scores, cancellation statistics and recovered revenue. No guest names, email addresses or phone numbers.
- Everything is read-only. The plugin cannot change your availability, strategy, Auto Apply setting or anything in your PMS. It runs no local code and stores nothing.

## Install

- **Claude (web and desktop app):** open **Customize > Plugins**, select **Discover**, find **Auctores** and select **Add**. Then open the plugin's **Connectors** tab and connect Auctores with your Auctores account. The plugin then also works in the mobile app, Cowork and Claude Code. Directory plugins are available on Pro, Max, Team and Enterprise plans.
- **Claude Code:**

  ```
  /plugin install auctores --marketplace Auctores-ai/auctores-ai-plugin
  ```

  Requires Claude Code 2.1.275 or later. Then run `/mcp` and sign in.

## Requirements

An Auctores account with a hotel connected through its PMS (Apaleo or Mews) and set up in Auctores.

## Example prompts

- Brief me on the next two weeks for my hotel.
- Which bookings arriving next week are most likely to cancel or not show up?
- Which booking channels have the highest cancellation and no-show rates, and how close to arrival do guests cancel?
- How much revenue did Auctores recover for us last month, and which bookings are behind it?
- Why is no extra availability suggested on some dates in the next two weeks?
- How many extra rooms does Smart Overbooking suggest for next weekend?
- Show expected occupancy for each day of the week after next, so we can plan staff and housekeeping.
- Draft a short, friendly pre-arrival message for the bookings arriving in the next three weeks that are likely to cancel.
- How many rooms do we expect to actually be occupied next Saturday?

## Support

Questions or problems: info@auctores.ai. Privacy policy: https://app.auctores.ai/overbooking/privacy

## License

Copyright (c) 2026 Auctores Technologies OÜ. All rights reserved. See [LICENSE](LICENSE).
