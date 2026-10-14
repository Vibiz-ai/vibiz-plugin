---
name: ad-performance-triage
description: Review live ad campaigns and individual ads on one platform in Vibiz, sort them into scale / keep / fix / pause, and prepare pauses for the user's approval. Use when the user asks "which ads are wasting money?", "what should I pause?", "which ad is best?" or "clean up my Meta/Google/TikTok ads".
---

# Ad performance triage

Find the money leaks and the winners on one platform, then act only with the user's approval.

## Workflow

1. **Scope.** Confirm the brand and the platform: `meta`, `google`, `tiktok`, `linkedin`, `pinterest` or `twitter`. Use the last 7 days unless the user says otherwise.
2. **Campaigns.** Call `vibiz_ads_campaigns` with `platform`, `action: "list"`, `fromDate` and `toDate` (YYYY-MM-DD). Only set `includeExternal: true` if the user wants campaigns built outside Vibiz too.
3. **Ads.** Call `vibiz_ads_creatives` with `platform` and `action: "list"` for the same dates. Use `action: "analytics"` with an `adId` only when one ad needs a day-by-day look.
4. **Sort every ad into a bucket.** Ask for the user's target cost per result or ROAS. If they don't have one, use the account's own average as the line.

   | Bucket | Rule of thumb |
   |---|---|
   | Scale | Clearly better than target, with enough data (about 1,000+ impressions or 10+ results) |
   | Keep | Near target, or still learning (too little data to judge) |
   | Fix | High CTR but poor conversion (landing page or offer), or low CTR with good conversion (creative) |
   | Pause | Clearly worse than target with enough data, or spending with zero results |

5. **Show the result** as a table (ad, spend, results, cost per result or ROAS, bucket, reason), plus the total spend in the Pause bucket ("$84 this week went to ads with no sales").
6. **Pause, with approval.** If the user wants to pause:
   - Call `vibiz_ads_pause` with `platform`, `level` (`campaign` or `creative`) and `ids`. It answers `approval_required`.
   - Call `vibiz_review_action` with `tool: "vibiz_ads_pause"` and exactly the same arguments, so the user approves in the card.
   - After approval, call `vibiz_ads_pause` again with the same arguments plus the `approval_token` from the card.
   - Turning ads back on happens in the Vibiz app (https://www.vibiz.ai).
7. **Replace losers.** Offer new creatives for the winning angle with `ad-creative-sprint`.

## Rules

- Never invent, reuse or edit an `approval_token`, and never change arguments after approval.
- Campaign ids are platform campaign ids; ad ids are the internal ids returned by `vibiz_ads_creatives`. Don't mix them up.
- Don't recommend deleting when pausing is enough.
