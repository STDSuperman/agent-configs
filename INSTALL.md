# AI Tools Sync

把本文件的 raw 链接丢给你的 AI 编码工具，即可开始同步 plugins 和 MCP server 配置。

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

例如：获取 `plugins/superpowers.md` → 请求 `${BASE_URL}/plugins/superpowers.md`

## 同步流程

请严格按以下步骤执行：

### 0. 全局优先原则

**所有配置默认安装到全局维度，而非项目维度。**

- Plugins: 通过 marketplace 安装到全局
- MCP: 根据工具类型使用 CLI 命令或 JSON 合并（见步骤4）
- 如需项目级配置，用户需手动调整

### 1. 选择工具

问用户：需要同步哪些工具？列出上表中的工具让用户多选。

### 2. 检测工具

对用户选择的每个工具，执行对应的检测命令：

- 如果命令返回零退出码（找到了可执行文件），标记为「已安装」
- 如果命令返回非零退出码，标记为「未安装」，后续跳过该工具

### 3. 同步 Plugins

Plugins 文件清单（使用 `${BASE_URL}` 拼接获取）：

- `plugins/superpowers.md`
- `plugins/code-simplifier.md`
- `plugins/frontend-design.md`
- `plugins/claude-hud.md`
- `plugins/example-skills.md`
- `plugins/planning-with-files.md`

对每个文件：

1. 获取文件内容
2. 对已安装的工具，执行「安装方式」下对应的安装命令
3. 记录结果

### 4. 同步 MCP

MCP 文件清单（使用 `${BASE_URL}` 拼接获取）：

- `mcp/deepwiki.md`
- `mcp/context7.md`
- `mcp/playwright.md`

对每个文件：

1. 获取文件内容
2. 对已安装的工具，执行「安装方式」下对应的安装命令
3. 记录结果

### 5. 输出摘要

输出同步结果，格式：

```
## 同步结果

### ✅ 已同步
- **Claude Code**: superpowers, code-simplifier, frontend-design, claude-hud, example-skills, planning-with-files (plugins)
- **opencode**: superpowers

### ⚠️ 未安装（已跳过）
- openclaw
- codex

### ❌ 安装失败
- （无）
```
