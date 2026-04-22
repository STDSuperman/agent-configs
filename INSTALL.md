# AI Tools Sync

把本文件的 raw 链接丢给你的 AI 编码工具，即可开始同步 skills/plugins 和 MCP server 配置。

## 支持的工具

| 工具 | 检测命令 | 插件安装机制 |
|------|---------|-------------|
| Claude Code | `which claude` | `claude plugin marketplace add <owner/repo>` + `claude plugin install <name>@<marketplace>` |
| opencode | `which opencode` | Fetch 远程 INSTALL.md |
| openclaw | `which openclaw` | 参见各 skill 文件 |
| codex | `which codex` | 参见各 skill 文件 |

## 远程文件访问

> ⚠️ 你当前不在本仓库目录中，无法直接读取相对路径的文件。
> 请使用以下 base URL 拼接相对路径来远程获取文件内容（通过 WebFetch 或 curl）：

```
BASE_URL = https://raw.githubusercontent.com/STDSuperman/agent-configs/master
```

例如：获取 `skills/superpowers.md` → 请求 `${BASE_URL}/skills/superpowers.md`

## 同步流程

请严格按以下步骤执行：

### 1. 选择工具

问用户：需要同步哪些工具？列出上表中的工具让用户多选。

### 2. 检测工具

对用户选择的每个工具，执行对应的检测命令：

- 如果命令返回零退出码（找到了可执行文件），标记为「已安装」
- 如果命令返回非零退出码，标记为「未安装」，后续跳过该工具

### 3. 同步 Skills

Skills 文件清单（使用 `${BASE_URL}` 拼接获取）：

- `skills/superpowers.md`
- `skills/claude-hud.md`
- `skills/example-skills.md`
- `skills/planning-with-files.md`

对每个文件：

1. 获取文件内容，查看头部的「兼容」字段
2. 对于用户选中且已安装的每个工具：
   - 如果该工具出现在兼容列表中，执行「安装方式」下对应工具的安装命令
   - 如果不在兼容列表中，跳过
3. 记录安装结果（成功/失败/跳过）

### 4. 同步 MCP

MCP 文件清单（使用 `${BASE_URL}` 拼接获取）：

- `mcp/deepwiki.md`
- `mcp/context7.md`
- `mcp/playwright.md`

对每个文件：

1. 获取文件内容，读取「配置」部分的 JSON
2. 将该 JSON 中的 mcpServers 条目合并到每个已安装工具的全局 MCP 配置文件中
3. 如果有「安装说明」部分，先执行安装步骤再配置

各工具的全局 MCP 配置路径：
- Claude Code: `~/.claude/settings.json` 中的 `mcpServers` 字段
- opencode: `~/.opencode/opencode.json` 中的 `mcpServers` 字段
- openclaw: 参见 openclaw 文档
- codex: `~/.codex/config.json` 中的 `mcpServers` 字段

### 5. 输出摘要

输出同步结果，格式：

```
## 同步结果

### ✅ 已同步
- **Claude Code**: superpowers, planning-with-files, claude-hud, example-skills
- **opencode**: superpowers

### ⚠️ 未安装（已跳过）
- openclaw
- codex

### ❌ 安装失败
- （无）
```
