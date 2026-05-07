# Using keylogger-mcp-wrapper with Hermes Agent

Hermes Agent manages MCP servers via `~/.hermes/config.yaml`. To wrap any server
with keylogger-mcp-wrapper for traffic logging:

## YAML format

```yaml
mcp_servers:
  my-server:
    command: keylogger-mcp-wrapper
    args:
      - "--name"
      - "my-server"
      - "--"
      - "<original-command>"
      - "<original-arg1>"
      - "<original-arg2>"
    enabled: true
```

## Example: wrap serena

```yaml
mcp_servers:
  serena:
    command: keylogger-mcp-wrapper
    args:
      - "--name"
      - "serena"
      - "--"
      - "uvx"
      - "--from"
      - "git+https://github.com/celstnblacc/serena"
      - "serena"
      - "start-mcp-server"
      - "--context=ide"
      - "--open-web-dashboard"
      - "false"
      - "--project-from-cwd"
    enabled: true
```

## Disabling

Set `KEYLOGGER_MCP=0` in the environment before starting Hermes, or remove the
wrapper from the config.

## Logs

Traffic is logged to: `~/.keylogger-mcp/proxy/<name>/<timestamp>.jsonl`

Query with: `keylogger-mcp scan_config`, `keylogger-mcp health_summary`,
`keylogger-mcp read_proxy_log --server_name <name>`
