---
name: ad-creative-sprint
description: Turn a product or offer into a small set of on-brand ad creatives (image, carousel, video or product shot) with distinct angles, clear costs and the user's approval before credits are spent. Use when the user asks to "make ads", "create creatives for my offer", "test new angles" or "I need ads for Instagram/TikTok/Facebook".
---

# Ad creative sprint

Goal: 2–4 creatives that test genuinely different angles, not four versions of the same idea, made only after the user approves the cost.

## Workflow

1. **Pick the brand.** If it isn't already clear, call `list_vibiz` and let the user choose. Use the slug as `vibiz`.
2. **Reuse before you make.** Call `vibiz_list_creatives` with `target: {"vibiz": "<slug>"}` and `limit: 5`. If something fits, offer it first: it costs nothing.
3. **Write the brief.** Collect, asking only for what's missing:
   - **Offer:** what is being sold, price or promo if any
   - **Audience:** who, and the problem they have
   - **Placement:** for example `instagram_portrait`, `facebook_feed`, `tiktok_story`
   - **Must-say lines and must-avoid claims**
4. **Propose angles.** Suggest 2–4 angles, one line each, from different families:
   - Pain → relief ("Tired of…? Meet…")
   - Outcome / transformation (before → after)
   - Social proof (reviews, numbers the user confirmed)
   - Offer / urgency (promo, limited time)
   - Objection handling ("Too expensive? Here's the math")
   Let the user keep, drop or edit them.
5. **Price it.** Call `vibiz_plan_ad_creative` with `format`, `brief` (offer + angle + audience + must-say lines), `count`, `placement` and `vibiz`. Show the credit cost and balance. Nothing is spent at this step.
   - Not affordable: say the feature isn't available on the current plan or balance, and that they can manage their account in the Vibiz app (https://www.vibiz.ai).
6. **Make it, on a clear yes only.** Call `vibiz_create_ad_creative` with exactly the same arguments as the plan. The progress card updates itself: do not poll `vibiz_generation_status`.
7. **Wrap up.** For each creative, give the angle it tests and one line on what to watch (for example "if CTR beats the other angle after ~1,000 impressions, scale it"). Launching paid ads happens in the Vibiz app.

## Choosing a format

| Format | Use for |
|---|---|
| `image` | Fast tests, feed placements, simple offers |
| `carousel` | Several products, step-by-step, feature lists |
| `video` | Motion for Reels/TikTok when there's no person on camera |
| `ugc` | Creator-style talking video; see the `ugc-video-ad` skill |
| `product_shot` | A product photo placed in a scene; needs `extra_fields` with `productTitle`, `productImageUrl` and `recipeId` |

## Rules

- Never call `vibiz_create_ad_creative` without the user's yes to the cost shown by the plan.
- Don't change arguments between plan and create; if the user edits the brief, plan again.
- No invented testimonials, numbers or guarantees.
