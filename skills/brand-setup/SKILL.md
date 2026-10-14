---
name: brand-setup
description: Set up or audit a brand in Vibiz from its website or Instagram URL, then check the brand kit (logo, colors, fonts, tone, audience) and fix the gaps before any ads are made. Use when the user says "add my brand", "set up my business", "onboard this site", or asks for ads for a brand Vibiz doesn't have yet.
---

# Brand setup

A good brand kit is what makes every later ad look and sound like the business. This skill gets the brand into Vibiz and makes sure the kit is complete before anything is generated.

## Workflow

1. **Find the brand.** Call `list_vibiz` with `query` set to the brand name or domain the user mentioned.
   - Listed: confirm the name with the user and use its slug. Never guess between two similar brands.
   - Not listed: go to step 2.
2. **Onboard it.** Call `vibiz_onboard_brand` with `url` (website or Instagram). It is safe to repeat: a matching website reuses the existing brand.
   - The setup card updates by itself. Do not poll.
   - Without a card, call `vibiz_onboard_brand` again with `vibiz` set to the slug to check progress. Continue when `setup.ready` is true.
3. **Audit the kit.** Call `vibiz_get_branding` with `target: {"vibiz": "<slug>"}` and check each field:

   | Field | Good enough when |
   |---|---|
   | Logo | A real logo URL, not empty |
   | Colors | 2–5 colors, including a primary |
   | Fonts | At least a heading font |
   | Tone | A short, specific description ("warm, expert, a bit playful"), not "Not specified" |
   | Target audience | Who, plus a need ("busy parents who want 10-minute dinners") |
   | Headline | One clear line about what the business offers |

4. **Report and fill gaps.** Show the kit as a short table. For each missing or weak field, propose a concrete value based on the website, and ask the user to confirm. Tell them they can edit the kit in the Vibiz app (https://www.vibiz.ai) if this connector can't save it.
5. **Next step.** Offer one of: make a first ad (`ad-creative-sprint`), a UGC video (`ugc-video-ad`), or `vibiz_get_recommendations` for what to do next.

## Rules

- Only act on the brand the user picked. If a request names a brand that isn't listed, onboard it; never fall back to another brand.
- Don't invent facts about the business (prices, awards, claims). Ask instead.
