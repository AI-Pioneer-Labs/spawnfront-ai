# Spawnfront for AI assistants

[Spawnfront](https://spawnfront.com) is where esports players find teams and teams find players — and where a team gets a hosted site with its roster, news, matches, tournaments and store.

This repo lets you use Spawnfront from your AI assistant. It holds:

- **Agent Skills** (`skills/`) — guided workflows in the open [Agent Skills](https://agentskills.io) format: set up your profile, post a news update, find a scrim, enter a tournament, set up your store.
- **A Claude Code plugin** (`plugins/spawnfront/`) — the Spawnfront connector plus those skills, installable from this repo's marketplace.

The work itself is done by Spawnfront's MCP server at **`https://spawnfront.com/api/mcp`**. It needs no API key and costs nothing: when you connect, Spawnfront asks you to sign in and choose what the assistant can reach — your profile and games, your teams, your site and news, your scrims and tournaments. It can only do what you can do, only on teams whose owner or an admin turned on **Allow AI assistants**, and it hands you a link for anything that stays on Spawnfront: publishing, deleting, payments, accepting players or scrims, and connecting a store, domain or game account. You see everything it changed, and can disconnect it any time, in **Profile › AI assistants**.

## Connect

**Claude** (web, desktop, mobile): Customize › Connectors › **+ Add** › **Add custom connector**, paste `https://spawnfront.com/api/mcp`, then sign in to Spawnfront and press **Allow**. The Free plan allows one custom connector.

**ChatGPT** (paid plans): turn on developer mode in settings and create an app with `https://spawnfront.com/api/mcp`, then sign in to Spawnfront and press **Allow**.

**Claude Code** — install the plugin, which brings the connector and the skills:

```sh
claude plugin marketplace add AI-Pioneer-Labs/spawnfront-ai
claude plugin install spawnfront@spawnfront
```

Then run `/mcp` in Claude Code and sign in to Spawnfront.

The clients below speak the same protocol and should connect the same way, signing in through your browser; we have not checked each of them yet.

**Codex CLI** — in `~/.codex/config.toml`:

```toml
[mcp_servers.spawnfront]
url = "https://spawnfront.com/api/mcp"
```

then `codex mcp login spawnfront`.

**Cursor** — in `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "spawnfront": { "url": "https://spawnfront.com/api/mcp" } } }
```

**VS Code** — in `.vscode/mcp.json`:

```json
{ "servers": { "spawnfront": { "type": "http", "url": "https://spawnfront.com/api/mcp" } } }
```

To use the skills with another agent, copy the folders in `skills/` into the place your agent reads skills from.

## Help

- [Connect an AI assistant](https://spawnfront.com/help/connect-an-ai-assistant)
- [See and disconnect your AI assistants](https://spawnfront.com/help/see-and-disconnect-your-ai-assistants)
- [Allow AI assistants on your team](https://spawnfront.com/help/allow-ai-assistants-on-your-team)
- Support: support@spawnfront.com

## The skills and the server's prompts

Spawnfront's server also offers these workflows as one-click prompts in apps that show them. Each skill says the same steps as its prompt:

| Skill | Server prompt | Tools, in order | Ends at the link |
|---|---|---|---|
| `set-up-profile` | `set_up_my_profile` | `get_my_profile`, `list_my_game_identities`, `update_my_profile`, `set_game_handle` | `link_game_account` |
| `post-news` | `post_a_news_update` | `list_my_teams`, `create_news_draft` | `publish_site` |
| `find-a-scrim` | `find_a_scrim` | `list_my_teams`, `search_scrims`, `list_open_scrim_offers`, `request_scrim` / `respond_to_scrim_offer` / `post_scrim_offer` | `accept_scrim` |
| `enter-a-tournament` | `enter_a_tournament` | `browse_tournaments`, `list_my_teams`, `enter_tournament`, `get_check_in`, `check_in`, `report_match_score` | the match page, once the other team has reported |
| `set-up-store` | `set_up_my_store` | `get_store_status` | `connect_store` |

## License

[MIT](LICENSE)
