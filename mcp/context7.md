# context7

编程库和框架的最新文档查询服务。

## 安装方式

### Claude Code

```bash
claude mcp add --transport http context7 https://mcp.context7.com/mcp --header "CONTEXT7_API_KEY: your-api-key-here"
```

### opencode / codex

将以下 JSON 合并到配置文件的 `mcpServers` 字段：

```json
{
  "context7": {
    "type": "http",
    "url": "https://mcp.context7.com/mcp",
    "headers": {
      "CONTEXT7_API_KEY": "your-api-key-here"
    }
  }
}
```

**注意**: 需要替换 `your-api-key-here` 为你的 Context7 API key。获取方式：访问 https://context7.com 注册账号并在设置页面获取。