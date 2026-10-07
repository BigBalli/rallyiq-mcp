# RallyIQ for Claude and other MCP clients

![RallyIQ](assets/icon.svg)

Ask an AI assistant how a tennis player should play an opponent and get an answer from shot-by-shot match data instead of memory: where to serve on each court, which returns work against that server, which rally patterns to favour and avoid, who is likely to win, and why a match turned.

This repository holds:

- the connection details for the **RallyIQ remote MCP server** at `https://bigballi.com/RallyIQ/mcp`,
- a **Claude plugin** that adds that server plus a `tennis-scouting` skill, which teaches Claude how to read the numbers.

The server is run by [RallyIQ](https://bigballi.com/RallyIQ/), which models more than 11,000 ATP and WTA matches charted shot by shot by volunteers for the [Match Charting Project](https://www.tennisabstract.com/charting/meta.html). Each shot is valued by how much it changed its hitter's chance of winning the point. How it works: [method](https://bigballi.com/RallyIQ/method).

## What you can ask

- "Give me a game plan for Sinner against Alcaraz on clay."
- "Where does Iga Swiatek serve on break points, and is her serve easy to read?"
- "What are Coco Gauff's biggest weaknesses, and who is best equipped to exploit them?"
- "Why did Djokovic lose the 2023 Wimbledon final?"
- "Which active WTA players choose their shot direction best?"

## Tools

All tools are read-only (`readOnlyHint: true`) and need no account.

| Tool | What it answers |
|---|---|
| `get_game_plan` | One player against an opponent, optionally on one surface: the match forecast with a 90% range, first-serve directions and the optimal mix on each court against that returner, the opponent's serve, the best returns against that server, rally shots to favour and avoid, career shot ratings side by side and the charted head-to-heads. |
| `get_player` | One player's scouting report: serve and return points won against an average opponent, shot ratings per 100 shots with tour percentiles, first-serve habits including on break points, how exploitable the serve is, the shots they hurt opponents with and the shots they are most exposed to, and similar players. |
| `explain_match` | Why a charted match went the way it did: each player's points against expectation split into direction choice, shot selection and execution, by stroke and by set, and the points each left on the table. |
| `get_leaders` | The top 10 ATP or WTA players on one of ten tactical measures, active or across eras. |

Every value comes with a 90% margin and a link to the full page on RallyIQ.

## Setup

### Claude (claude.ai, Desktop, mobile)

Settings → Connectors → Add custom connector, then paste `https://bigballi.com/RallyIQ/mcp`. No sign-in is needed.

### Claude Code

Install the plugin, which adds the server and the `tennis-scouting` skill:

```
/plugin marketplace add BigBalli/rallyiq-mcp
/plugin install rallyiq@rallyiq
```

Or add only the server:

```
claude mcp add --transport http rallyiq https://bigballi.com/RallyIQ/mcp
```

### Other MCP clients

Any client that supports remote MCP servers over Streamable HTTP can use `https://bigballi.com/RallyIQ/mcp` with no credentials. The server speaks protocol versions 2026-07-28, 2025-11-25, 2025-06-18 and 2025-03-26 and answers with JSON (no SSE, no sessions).

## Privacy

The server receives the tool name and its arguments (for example two player names and a surface), uses them to answer, and does not store them. It never sees your conversation or your account. Full policy: [bigballi.com/RallyIQ/privacy](https://bigballi.com/RallyIQ/privacy).

## Support

Email g@bigballi.com, or see [bigballi.com/RallyIQ/connect](https://bigballi.com/RallyIQ/connect).

## License

The contents of this repository are released under the MIT License. The data served by the RallyIQ MCP server is not part of this repository: it derives from the Match Charting Project and is licensed [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/), which requires crediting the Match Charting Project wherever it is used.
