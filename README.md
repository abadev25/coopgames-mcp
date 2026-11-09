<p align="center"><a href="https://coopgames.app"><img src="logo.svg" alt="CoopGames" width="320"></a></p>

# CoopGames MCP server

[Español](README.es.md)

A free, read-only [MCP](https://modelcontextprotocol.io) server that lets AI assistants answer "what can we play together?". Ask for games by number of players, platforms, crossplay, couch co-op or price, and get answers from the [CoopGames](https://coopgames.app) catalog of co-op and multiplayer games.

- **URL:** `https://coopgames.app/mcp`
- **Transport:** Streamable HTTP
- **Auth:** none
- **Registry name:** `app.coopgames/coopgames`

## Connect it

**Claude Code**

```bash
claude mcp add --transport http coopgames https://coopgames.app/mcp
```

**Claude (web and desktop):** Settings → Connectors → Add custom connector → paste `https://coopgames.app/mcp`.

**Cursor** (`~/.cursor/mcp.json`)

```json
{ "mcpServers": { "coopgames": { "url": "https://coopgames.app/mcp" } } }
```

**VS Code** (`.vscode/mcp.json`)

```json
{ "servers": { "coopgames": { "type": "http", "url": "https://coopgames.app/mcp" } } }
```

Any other client that supports remote MCP servers over HTTP works with the same URL.

## Tools

| Tool | Use it for |
|---|---|
| `search_games` | Find games for a group: players (2–8), platforms, online or same screen, co-op or versus, genre, crossplay, free-to-play, one copy for everyone |
| `get_game` | The full multiplayer picture of one game: platforms, player counts, crossplay between every pair of platforms, session length |
| `crossplay_check` | A quick yes or no: can someone on platform A play this game with someone on platform B? |

Platforms: PC, PS5, PS4, Xbox, Switch and Switch 2. Every result links to the game's page on CoopGames.

## Example prompts

- "Four of us want to play tonight: two on PC, one on PS5, one on Xbox. What has crossplay?"
- "Free co-op games for 3 players on Switch"
- "Can I play Helldivers 2 with a friend on Xbox if I'm on PS5?"
- "Couch co-op games for two on PS5"

## Try it without a client

```bash
curl -s https://coopgames.app/mcp \
  -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"search_games","arguments":{"players":4,"platforms":["pc","ps5"],"crossplay":true,"limit":3}}}'
```

## Limits

- Read-only. It never writes anything.
- Requests are rate limited per IP. If you get `429`, wait a minute.
- Please cite CoopGames and link to the game's page when you use the data.

## Links

- Website: [coopgames.app](https://coopgames.app)
- Browse every game: [coopgames.app/games](https://coopgames.app/games)

## License

The text and examples in this repository are under the [MIT License](LICENSE). The catalog data behind the server belongs to CoopGames.
