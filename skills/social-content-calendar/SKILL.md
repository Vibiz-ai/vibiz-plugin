---
name: social-content-calendar
description: Plan a week of on-brand social posts with Vibiz from the brand kit and what already performed, then schedule them to connected Instagram, TikTok, LinkedIn, Facebook or X accounts with the user's approval. Use when the user asks for "a content calendar", "posts for this week", "what should I post?" or "schedule posts".
---

# Social content calendar

A realistic week of posts the brand can actually publish, built on what has worked before.

## Workflow

1. **Context.** Confirm the brand. Then gather, in parallel:
   - `vibiz_get_branding` with `target: {"vibiz": "<slug>"}` for tone and audience
   - `vibiz_social_list_accounts` with the same `target` for connected accounts. If none are connected, share the `connectUrl` it returns.
   - `vibiz_social_list_posts` with `status: "published"` to see recent posts
   - Optional: `vibiz_growth_report` with `range: "30d"` for top posts
2. **Agree the plan.** Ask how many posts (default 3–5 for the week) and which platforms.
3. **Use a content mix:**

   | Type | Share | Example |
   |---|---|---|
   | Value / how-to | ~40% | "3 ways to keep coffee fresh" |
   | Proof / behind the scenes | ~30% | Customer story, making-of |
   | Offer | ~20% | Promo, new product |
   | Community / fun | ~10% | Question, poll, trend |

4. **Draft the calendar** as a table: day, time (local), platform, type, caption, hashtags, media. Adapt captions per platform: short and punchy for TikTok/Instagram, more context for LinkedIn. Reuse finished creatives from `vibiz_list_creatives` as media, or offer to make new ones with `ad-creative-sprint`.
5. **Review.** Let the user edit or approve each post.
6. **Schedule, with approval, one post at a time:**
   - Call `vibiz_social_publish` with `target`, `content`, `platforms` (each with its `accountId`), optional `hashtags` and `mediaUrls`, and `scheduledFor` as an ISO datetime. It answers `approval_required`.
   - Call `vibiz_review_action` with `tool: "vibiz_social_publish"` and the exact same arguments.
   - After the user approves in the card, call `vibiz_social_publish` again with the same arguments plus the `approval_token`.
7. **Confirm** with `vibiz_social_list_posts` (`status: "scheduled"`).

## Rules

- Never publish or schedule without an approval card. Never invent, reuse or edit an `approval_token`.
- Don't post claims, prices or promos the user hasn't confirmed.
- Use the user's timezone for times. Ask if it's unclear.
