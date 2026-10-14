---
name: weekly-marketing-report
description: Produce a short, numbers-first marketing report for a brand from Vibiz (social, top posts and paid ads across Meta, Google, TikTok, LinkedIn, Pinterest and X) with the 2–3 moves that matter most. Use when the user asks "how did my marketing do?", "what worked last week/month?", "give me a weekly report" or "what should I double down on?".
---

# Weekly marketing report

One read, one decision. The report should take under a minute to read and end with clear next moves.

## Workflow

1. **Brand.** Confirm it (`list_vibiz` if needed).
2. **Pull the data.** Call `vibiz_growth_report` with `vibiz` and `range`:
   - `7d` for "last week" (default), `30d` for "last month", `90d` for "this quarter"
   - Optional `platforms` to narrow it, for example `["meta", "tiktok"]`
3. **Drill down only if needed.** If one platform drives most of the spend or has an anomaly, call `vibiz_ads_campaigns` with `platform` and `action: "list"` for campaign-level numbers.
4. **Write the report** in this shape:

   **Headline:** one sentence, for example "Spend steady, Meta ROAS up 22%, TikTok still unprofitable."

   | Channel | Spend | Results | Efficiency | vs. last period |
   |---|---|---|---|---|

   **What worked:** 1–2 bullets, each with the number behind it.
   **What didn't:** 1–2 bullets, each with the number behind it.
   **Next moves (max 3):** each one an action plus a reason backed by data, for example "Move $20/day from TikTok to the Meta 'busy parents' campaign: ROAS 3.1 vs 0.8."

5. **Offer follow-ups:** make new creatives for the winning angle (`ad-creative-sprint`), triage the losers (`ad-performance-triage`), or plan next week's posts (`social-content-calendar`).

## Rules

- Platforms marked `not_connected` go in one line at the end ("Not connected: Pinterest, X"), not in the table.
- Always show currency with spend. Don't compare platforms on metrics they don't share.
- Don't make up benchmarks. When saying something is "good" or "bad", compare it to the brand's own previous period or to another channel in the same report.
