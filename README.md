# TimeTrack

A standalone MCP server for logging and querying billable hours.

## Complete Setup Checklist

1. Install `uv`.
2. Run `uv sync`.
3. Verify with `uv run fastmcp inspect main.py:mcp`.
4. Run locally with `uv run fastmcp run main.py:mcp --transport http`.

## What's inside

| Primitive | Name | What it does |
|---|---|---|
| Tool | `log_time` | Logs a new time entry |
| Tool | `get_timesheet` | One employee's entries, optionally filtered by date range |
| Tool | `get_project_summary` | Total hours per project, broken down by employee (real `GROUP BY`) |
| Tool | `list_projects` | Every project with at least one logged entry |
| Resource | `timesheet://projects` | The current set of known project names |
| Prompt | `generate_weekly_report` | Structures a weekly hours report request |

## Connecting an MCP client

```json
{
  "mcpServers": {
    "timetrack": { "url": "http://127.0.0.1:8000/mcp" }
  }
}
```

## Going live: Prefect Horizon

Formerly known as FastMCP Cloud — same team, same idea, current name verified
before writing this. Free for personal projects.

1. Sign in to [Prefect Horizon](https://horizon.prefect.io) with GitHub.
3. Connect the repo — dependencies auto-detected from `pyproject.toml`
4. Configure entrypoint `main.py:mcp`.
5. Deploy — Horizon provides the public MCP URL.

## Files

- `database.py` — SQLite persistence, tested including real aggregation and a
  genuine restart-and-recover proof
- `main.py` — the MCP server entrypoint
