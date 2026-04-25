# deepwiki

GitHub 仓库的 AI 驱动文档查询服务。

## 安装方式

### Claude Code

```bash
claude mcp add --transport http deepwiki https://mcp.deepwiki.com/mcp
```

### opencode / codex

将以下 JSON 合并到配置文件的 `mcpServers` 字段：

```json
{
  "deepwiki": {
    "type": "http",
    "url": "https://mcp.deepwiki.com/mcp"
  }
}
```