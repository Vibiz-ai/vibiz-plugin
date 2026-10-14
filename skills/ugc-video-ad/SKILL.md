---
name: ugc-video-ad
description: Write and produce creator-style (UGC) video ads for TikTok, Reels and Shorts with Vibiz, starting from scroll-stopping hooks and a short script. Use when the user asks for "a UGC video", "a TikTok ad", "a creator-style video", "a talking-head ad" or "a Reel for my product".
---

# UGC video ad

UGC ads work when the first 2 seconds stop the scroll and the rest sounds like a real person, not an ad. Get the script right before spending credits.

## Workflow

1. **Brand and product.** Confirm the brand (`list_vibiz` if needed) and the one product or offer the video is about.
2. **Draft 3 hooks**, each under 10 words and each from a different style:
   - Callout: "If you run a coffee shop, watch this."
   - Confession: "I wasted $400 before I found this."
   - Result first: "This got me 37 orders in a weekend." (only with numbers the user confirms)
   - Contrarian: "Stop posting every day. Do this instead."
3. **Write the script** for the length:

   | Length | Structure |
   |---|---|
   | 4s | Hook + product shown |
   | 6s | Hook → one benefit → call to action |
   | 8s | Hook → problem → product as the fix → call to action |

   Keep it spoken and simple: short sentences, no jargon, one call to action.
4. **Let the user pick** a hook and approve the script. Offer 2–3 variations only if they want to test hooks against each other.
5. **Price it.** Call `vibiz_plan_ad_creative` with:
   - `format: "ugc"`
   - `brief`: product, audience, chosen hook and the full script
   - `duration`: `4s`, `6s` or `8s` (default `8s`)
   - `resolution`: `720p` by default, `1080p` if they want higher quality
   - `placement`: `tiktok`, `reels` or `shorts`
   - `count`: 1–4 (one per hook being tested)
   Show the credit cost and balance.
6. **Make it on a clear yes.** Call `vibiz_create_ad_creative` with the same arguments. The card updates by itself; don't poll.
7. **Next.** Suggest posting the best one organically first (`social-content-calendar`) and judging it by 3-second view rate and watch time before paying to boost it.

## Rules

- Never imply a real person endorsed the product unless the user confirms it.
- No health, income or results claims the user can't back up.
- Never create without explicit approval of the cost.
