# playwright

浏览器自动化和测试工具。

## 配置

```json
{
  "mcpServers": {
    "playwright": {
      "type": "stdio",
      "command": "npx",
      "args": ["@playwright/mcp@latest"],
      "env": {}
    }
  }
}
```

使用 `npx` 自动安装，无需预先安装。