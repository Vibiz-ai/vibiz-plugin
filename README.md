# Vibiz for Claude

Vibiz is your AI marketing team. This plugin connects Claude to the Vibiz MCP server and adds six skills, so Claude follows proven marketing workflows: set up a brand, make ads that test real angles, write UGC video scripts, report on what worked, cut wasted ad spend, and plan a week of social posts. Anything that spends credits, publishes, or pauses ads always asks for your approval first.

## What's included

### Connector
- **Vibiz MCP server:** `https://mcp.vibiz.ai/mcp` (remote, OAuth sign-in)

### Skills

| Skill | Use it when you say… |
|---|---|
| `brand-setup` | "Add my brand from mysite.com" / "Is my brand kit complete?" |
| `ad-creative-sprint` | "Make 3 ads for my summer offer" |
| `ugc-video-ad` | "I need a TikTok-style video ad for my product" |
| `weekly-marketing-report` | "How did my marketing do last week?" |
| `ad-performance-triage` | "Which Meta ads are wasting money?" |
| `social-content-calendar` | "Plan and schedule this week's Instagram posts" |

## Setup

1. Install the plugin from the Claude directory.
2. The first time a skill uses Vibiz, Claude asks you to sign in to Vibiz (OAuth). Log in and allow access.
3. Try: "Add my brand from https://example.com, then make my first ad."

You need a Vibiz account (https://www.vibiz.ai). Ad and social reports need your ad and social accounts connected in the Vibiz app. Generating creatives uses Vibiz credits, and Claude always shows the cost first.

## What this plugin runs, sends and stores

- The plugin contains only instructions (skills) and one MCP server declaration. It runs no local code, scripts or hooks.
- All actions go to the Vibiz MCP server at `https://mcp.vibiz.ai/mcp`, over HTTPS, after you sign in with OAuth. Data sent includes the brand URLs, briefs and post text you give Claude, plus requests for your Vibiz data (brand kit, creatives, ad and social metrics).
- No data is sent to any other destination. Vibiz's handling of your data is described in its privacy policy: https://www.vibiz.ai/privacy
- Publishing posts, pausing ads and deleting require you to approve each action in a Vibiz approval card.

## Support

- Docs: https://www.vibiz.ai/docs/mcp
- Support: https://www.vibiz.ai/support
- Email: lautaro@vibiz.ai

## License

MIT
