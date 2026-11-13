# Kochava for Advertisers — MCP Server

[![MCP Badge](https://lobehub.com/badge/mcp/kochava-kochava-k4a-mcp-server)](https://lobehub.com/mcp/kochava-kochava-k4a-mcp-server)

Kochava for Advertisers is the Omnichannel measurement and attribution platform provided by Kochava, incorporating last-click attribution, incrementality, and MMM tools for brands and their agencies.

This MCP server lets any AI tool query live Kochava attribution data, manage campaigns, and create reports — with **no existing account required**. Connect, create a free account in-session, and start querying immediately.

## No Account? No Problem.

You don't need a Kochava account to get started. The server includes two **public tools** that work without any authentication:

1. **`kochava_free_app_analytics_get_tos`** — Review the Free App Analytics Terms of Service
2. **`kochava_free_app_analytics_create_acc_and_get_auth_key`** — Create a free account and receive your API key instantly, right in the conversation

Once you have your API key, set it as the `authentication-key` header and the full suite of 50 tools becomes available.

## Connect

**Endpoint**: `https://analytics.mcp.kochava.com/mcp`
**Transport**: Streamable HTTP
**Authentication**: `authentication-key` header (optional for signup, required for data tools)

### Claude Desktop

Edit the config file directly — there's no in-app "Edit Config" shortcut:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux (beta): `~/.config/claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "kochava": {
      "command": "npx",
      "args": [
        "-y", "mcp-remote",
        "https://analytics.mcp.kochava.com/mcp",
        "--header", "authentication-key:YOUR_API_KEY"
      ]
    }
  }
}
```

Requires Node.js (for `npx`). Leave `authentication-key` empty or omit the `--header` argument entirely to start with FAA signup tools only. Fully quit and reopen Claude Desktop after saving for the change to take effect — the connector then shows up under **Customize → Connectors**, where you can review its tool permissions.

### Claude Code

```bash
claude mcp add kochava --transport streamable-http https://analytics.mcp.kochava.com/mcp --header "authentication-key: YOUR_API_KEY"
```

Omit the `--header` argument entirely to start with FAA signup tools only.

### Cursor

Settings → Tools & MCPs → Add Custom MCP, which opens `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project) for editing:

```json
{
  "mcpServers": {
    "kochava": {
      "url": "https://analytics.mcp.kochava.com/mcp",
      "headers": {
        "authentication-key": "YOUR_API_KEY"
      }
    }
  }
}
```

Leave `authentication-key` empty or omit the `headers` block entirely to start with FAA signup tools only.

### VS Code / GitHub Copilot

**Per-project (recommended to start):** add to `.vscode/mcp.json` in your project root:

```json
{
  "servers": {
    "kochava": {
      "type": "http",
      "url": "https://analytics.mcp.kochava.com/mcp",
      "headers": {
        "authentication-key": "YOUR_API_KEY"
      }
    }
  }
}
```

A **Start** button appears above the `kochava` entry directly in the editor — click it to connect, then ask Copilot Chat (in **Agent** mode) something like "list my kochava campaigns" to confirm it's working.

**Available in every project (user-level):** add the same server to `~/.copilot/mcp-config.json` instead, using the `mcpServers` key:

```json
{
  "mcpServers": {
    "kochava": {
      "type": "http",
      "url": "https://analytics.mcp.kochava.com/mcp",
      "headers": {
        "authentication-key": "YOUR_API_KEY"
      }
    }
  }
}
```

This shows up under **User** when you run **Chat: Open Customizations → MCP Servers** from the Command Palette, separately from any per-project **Workspace** servers.

> **Note:** `.vscode/mcp.json`'s `servers` format is VS Code's older, editor-managed MCP support and still works today, but VS Code has marked it for removal in February 2027 in favor of the native `mcpServers` format shown above. Either works now; new setups can use either, but the `~/.copilot/mcp-config.json` form is the one VS Code is standardizing on.

## Tools

50 tools total: 31 read-only, 19 write or delete (create/update/delete operations, plus two backfill tools that re-ingest cost data over a date range).

### Free App Analytics (no auth required)

| Tool | Description |
|------|-------------|
| `kochava_free_app_analytics_get_tos` | Get the FAA Terms of Service link |
| `kochava_free_app_analytics_create_acc_and_get_auth_key` | Create a free account and get an API key in-session |

### Analytics & Reporting

| Tool | Description |
|------|-------------|
| `get_all_apps` | List all apps in your account |
| `get_app_dimensions` | Get dimensions available for an app |
| `run_search_query` | Run an analytics search query |
| `get_event_detail` | Get event-level detail data |
| `get_explorer_data` | Query the analytics explorer |
| `get_funnel_data` | Get funnel analysis data |
| `get_LTV_details` | Get lifetime value details |
| `get_retention_overlay` | Get retention overlay data |
| `get_currencies` | List supported currencies |

### Report Querying

| Tool | Description |
|------|-------------|
| `search_tables` | Search available report tables |
| `get_saved_queries` | List saved report queries |
| `execute_report_query` | Execute a report query |
| `get_query_results` | Get results from an executed query |

### App Management

| Tool | Description |
|------|-------------|
| `kochava_create_app` | Create a new app in your advertiser account |
| `kochava_get_app_settings` | Get an app's SDK key and session tracking settings |
| `kochava_update_app` | Update an existing app's settings |
| `kochava_get_app_group_memberships` | List the App Groups an app belongs to |
| `kochava_update_app_groups` | Change which App Groups an app belongs to |

### Campaign Management

| Tool | Description |
|------|-------------|
| `kochava_list_campaigns` | List all campaigns |
| `kochava_get_campaign` | Get campaign details |
| `kochava_create_campaign` | Create a new campaign |
| `kochava_update_campaign` | Update an existing campaign |

### Event Management

| Tool | Description |
|------|-------------|
| `kochava_create_event` | Create a new event |
| `kochava_update_event` | Update an event, or remap it |

### Tracker Management

| Tool | Description |
|------|-------------|
| `kochava_list_trackers` | List all trackers |
| `kochava_create_tracker` | Create a new tracker |
| `kochava_update_tracker` | Update an existing tracker |
| `kochava_delete_tracker` | Delete a tracker |
| `kochava_get_tracker_metrics` | Get tracker performance metrics |
| `kochava_get_all_media_partners` | List available media partners |
| `kochava_get_agency_networks` | List agency networks |
| `kochava_list_events_for_tracker_creation` | List events available for tracker setup |

### Segment Management

| Tool | Description |
|------|-------------|
| `kochava_list_segments` | List all segments |
| `kochava_create_segment` | Create a new segment |
| `kochava_update_segment` | Update an existing segment |

### Postback Configuration

| Tool | Description |
|------|-------------|
| `kochava_list_postback_templates` | List available postback templates for an app |
| `kochava_configure_postback` | Create or update a postback trigger for a network |
| `kochava_get_partner_configuration` | Get which events are shared with a partner network |

### Attribution Windows

| Tool | Description |
|------|-------------|
| `kochava_get_attribution_windows` | Get attribution reconciliation window settings |
| `kochava_set_attribution_windows` | Set attribution reconciliation window settings |

### SmartLinks

| Tool | Description |
|------|-------------|
| `kochava_list_app_groups` | List App Groups, or find the ones containing an app |
| `kochava_list_smartlink_networks` | List networks eligible for SmartLink use |
| `kochava_create_smartlink` | Create a SmartLink |

### Fraud

| Tool | Description |
|------|-------------|
| `kochava_get_fraud_config` | Get an account's fraud blacklist/whitelist entries |

### Cost Data

| Tool | Description |
|------|-------------|
| `kochava_list_cost_configurations` | List an account's configured cost data connectors |
| `kochava_trigger_cost_backfill` | Trigger a cost data backfill over a date range |
| `kochava_get_cost_backfill_status` | Get the latest cost data backfill status |
| `kochava_recover_cost_backfill` | Retry the unrecovered dates of a finished cost backfill |

## Authentication

**Without a key**: You can connect and use the two FAA signup tools to create a free account. Your API key is returned immediately in the conversation.

**With a key**: Set the `authentication-key` header to your Kochava API key. All 50 tools become available.

**Free App Analytics** gives you 30 days of data retention. Upgrade to Enterprise for unlimited retention — same API key, same MCP connection, zero migration.

## Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| 401 Unauthorized | Missing `authentication-key` header | Add your API key as the `authentication-key` header |
| 403 Invalid token | API key not recognized | Verify your key at [console.kochava.com](https://console.kochava.com) |
| 503 Service unavailable | Auth service temporarily down | Retry in a few seconds |
| `account_exists` | Company name already registered | Use a different company name or log in at [console.kochava.com](https://console.kochava.com) |

## Support

- **Email**: support@freeappanalytics.com
- **Console**: [console.kochava.com](https://console.kochava.com)


<!-- smithery-verification=96309c88075d1d87e141dfb766db8b75e736ac13f39824dc7a00a03eb4dadc6b -->