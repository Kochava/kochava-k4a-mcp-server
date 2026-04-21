# Kochava for Advertisers — MCP Server

Kochava for Advertisers is the Omnichannel measurement and attribution platform provided by Kochava, incorporating last-click attribution, incrementality, and MMM tools for brands and their agencies.

This MCP server lets any AI tool query live Kochava attribution data, manage campaigns, and create reports — with **no existing account required**. Connect, create a free account in-session, and start querying immediately.

## No Account? No Problem.

You don't need a Kochava account to get started. The server includes two **public tools** that work without any authentication:

1. **`kochava_free_app_analytics_get_tos`** — Review the Free App Analytics Terms of Service
2. **`kochava_free_app_analytics_create_acc_and_get_auth_key`** — Create a free account and receive your API key instantly, right in the conversation

Once you have your API key, set it as the `authentication-key` header and the full suite of 30 tools becomes available.

## Connect

**Endpoint**: `https://analytics.mcp.kochava.com/mcp`
**Transport**: Streamable HTTP
**Authentication**: `authentication-key` header (optional for signup, required for data tools)

### Claude Desktop

Add to `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `~/.config/claude/claude_desktop_config.json` (Linux):

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

### Claude Code

```bash
claude mcp add kochava --transport streamable-http https://analytics.mcp.kochava.com/mcp
```

### Cursor

Settings → MCP → Add Server:
- **URL**: `https://analytics.mcp.kochava.com/mcp`
- **Header**: `authentication-key: YOUR_API_KEY`

### VS Code / GitHub Copilot

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "kochava": {
      "type": "streamable-http",
      "url": "https://analytics.mcp.kochava.com/mcp",
      "headers": {
        "authentication-key": "YOUR_API_KEY"
      }
    }
  }
}
```

## Tools

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

### Campaign Management

| Tool | Description |
|------|-------------|
| `kochava_list_campaigns` | List all campaigns |
| `kochava_get_campaign` | Get campaign details |
| `kochava_create_campaign` | Create a new campaign |
| `kochava_update_campaign` | Update an existing campaign |

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

## Authentication

**Without a key**: You can connect and use the two FAA signup tools to create a free account. Your API key is returned immediately in the conversation.

**With a key**: Set the `authentication-key` header to your Kochava API key. All 30 tools become available.

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
