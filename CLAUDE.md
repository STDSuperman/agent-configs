# agent-configs

用于多机器间同步 AI 编码工具配置（skills、MCP server 等），通过 `INSTALL.md` 的 raw 链接一键拉取安装。

## 安装相关约定

- `INSTALL.md` 是唯一入口，`BASE_URL` 指向 master 分支 raw 地址，所有文件以相对路径挂在其中的清单下。
- 新增/删除 `skills/*.md` 或 `mcp/*.md` 必须同步更新 `INSTALL.md` 对应清单，否则不会被同步。

## 文件职责分工

| 文件 | 职责 |
|------|------|
| INSTALL.md | 流程指引 + 文件清单，不含具体安装命令 |
| skills/*.md / mcp/*.md | 具体安装方式（「安装方式」章节按工具分节） |

新增 skill/mcp 时只需：1. 子目录添加文件（含安装方式）；2. INSTALL.md 清单加一行。

## 元规则

用户给出的任何规则化/长期性要求，必须即时提炼为最精准的核心点合入本文件，禁止罗列、禁止啰嗦。
