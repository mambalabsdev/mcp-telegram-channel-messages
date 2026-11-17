# Telegram Channel Messages MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-telegram-channel-messages)](https://www.npmjs.com/package/@mambalabsdev/mcp-telegram-channel-messages) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-telegram-channel-messages)](https://github.com/mambalabsdev/mcp-telegram-channel-messages/blob/main/LICENSE)

An MCP server for the Mamba Labs Telegram Channel Messages actor on Apify. Public Telegram channel posts as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes public Telegram channel usernames or t.me links and returns one row per message, newest first, with text, date, views, reactions, media links, links, and forward and reply details, plus a free summary row per channel.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-telegram-channel-messages": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-telegram-channel-messages"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_telegram_channel_messages` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Get the last 50 posts from the Telegram channel durov with their view counts."
- "What did the telegram channel post since November 1, and which post had the most views?"

## Tool

`get_telegram_channel_messages`. One tool. Example arguments:

```json
{
  "channels": [
    "durov"
  ],
  "max_messages_per_channel": 20
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `channels` | array | no | Public channel usernames (durov or @durov) or links (https://t.me/durov, https://t.me/s/durov). A post link such as https://t.me/durov/542 starts reading at that post and goes back from there. Private invite links do not work: only public channels have a web preview. |
| `max_messages_per_channel` | number | no | Messages to read from each channel, newest first. Telegram shows 20 a page. Default 20, maximum 5000. |
| `since_date` | string | no | Optional. A date such as 2026-11-01, or a number of days back such as 7. Reading stops at the first older message. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `message-row`, one channel message | $0.002 | $0.0019 | $0.0018 | $0.0017 |
| `apify-actor-start`, per run start | $0.005 | $0.005 | $0.005 | $0.005 |

Channel summaries, service messages, channels with no public preview, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/telegram-channel-messages](https://apify.com/mambalabs/telegram-channel-messages)

## License

MIT. See [LICENSE](LICENSE).
