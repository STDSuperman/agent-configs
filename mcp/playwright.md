# playwright

浏览器自动化和测试工具。

## 安装方式

### Claude Code

```bash
claude mcp add playwright -- npx @playwright/mcp@latest
```

### opencode / codex

将以下 JSON 合并到配置文件的 `mcpServers` 字段：

```json
{
  "playwright": {
    "type": "stdio",
    "command": "npx",
    "args": ["@playwright/mcp@latest"],
    "env": {}
  }
}
```

使用 `npx` 自动安装，无需预先安装依赖。