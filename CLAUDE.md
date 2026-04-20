# agent-configs

AI 编码工具的 skills/plugins 和 MCP server 配置集中管理仓库。

## 仓库结构

```
INSTALL.md          # 入口文件，AI 通过其 raw 链接执行同步
skills/*.md         # Skill 配置，每个文件一个 skill
mcp/*.md            # MCP server 配置，每个文件一个 server
```

## 维护规则

### 新增 Skill

1. 在 `skills/` 下新建 `.md` 文件，格式：
   ```
   # <name>
   - 来源: <github-url>
   - 兼容: <tool1>, <tool2>
   ## 安装方式
   ### <Tool Name>
   ```<install-command>```
   ```
2. 在 `INSTALL.md` 的「同步 Skills」清单中追加相对路径

### 新增 MCP Server

1. 在 `mcp/` 下新建 `.md` 文件，包含「配置」(JSON) 和可选的「安装说明」
2. 在 `INSTALL.md` 的「同步 MCP」清单中追加相对路径

### 修改 INSTALL.md

- `BASE_URL` 指向本仓库 master 分支的 raw 地址，文件清单使用相对路径
- 新增/删除 skill 或 mcp 文件时必须同步更新对应清单
