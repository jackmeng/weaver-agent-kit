# Weaver Marketplace

Weaver 影游创作的插件与 MCP 接入指南。当前提供 `weaver-film@weaver`，连接 [Weaver 平台](https://www.weavercreate.com/) 的远程 MCP 服务，使用自己的 Weaver 账号完成 OAuth 授权即可开始创作。

## 安装

### ChatGPT（Codex）

直接将下面话术发送给 ChatGPT（Codex）：

```text
帮我安装 Weaver Plugin，让我可以在这里创作互动影游。

1. 添加插件目录：执行 `codex plugin marketplace add https://github.com/jackmeng/weaver-agent-kit.git --ref main`
2. 安装插件：执行 `codex plugin add weaver-film@weaver`
3. 新建任务后完成 Weaver 账户授权
就绪后告诉我，可以开始创作了。
```

> 提示：macOS 添加插件目录后，也可以在终端执行 `open 'codex://plugins/install/weaver-film?marketplace=weaver'` 直接打开插件详情页；
> 网页端自定义 MCP 接入参考 [OpenAI 自定义 MCP 接入说明](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt)。

### WorkBuddy / Claude / Hermes / 通用 Remote MCP 客户端

直接将下面话术发送给 WorkBuddy、Claude、Hermes 或其他支持远程 MCP 连接器的客户端：

```text
帮我在当前 Agent 中连接 Weaver Remote MCP，让我可以在这里创作互动影游。

1. 新建一个名为 Weaver 的远程 HTTP MCP 连接器
2. 连接地址填 `https://api.weavercreate.com/api/v1/mcp/film`
3. 保存（如提示需信任请点击 Trust）并完成 Weaver 账户 OAuth 授权
4. 授权就绪后告诉我，并给出 3 个可直接开始的创作示例（eg）
```

## 首次验证

安装并授权后，新开一个会话，发送：

> 使用 Weaver 的 `list_projects` 工具查看我的影游项目。

工具实际返回项目列表即接入成功（空列表也算）。

## 排查

| 现象                                 | 检查                                                                                                                                                                      |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Desktop 找不到 Weaver                | 确认已添加 `weaver` marketplace，重启 Desktop 后从 Plugins 进入；macOS 可在终端运行 `open 'codex://plugins/install/weaver-film?marketplace=weaver'` 打开详情页。          |
| Weaver 提示未授权                    | 按客户端的连接提示重新完成 OAuth 授权；Codex CLI 可执行 `codex mcp login weaver-film`。                                                                                   |
| 授权后仍找不到 `list_projects`       | 新开会话，确认插件/连接器已启用且已完成 Trust 与 OAuth 授权，再重新运行「首次验证」。                                                                                     |
| WorkBuddy中自定义mcp没有Weaver       | 因为自定义连接器的列表不会刷新，重启workbuddy会刷新自定义连接器的列表                                                                                                     |

## 随包 Skill

`filmgame-sop` 是影游创作入口，覆盖剧本、剧情树、资产、分镜和视频。各阶段指南与专业创作规范由远程 MCP 的 `get_workflow_guide` 实时提供，即使未安装本地插件、仅直连远程 MCP 也可完整加载。

## 创作示例

授权完成后，直接把下面任一句发给你的 Agent 即可：

- **eg 1（从零创作）**：「帮我从零创作一个悬疑反转题材的互动影游，先完成剧本策划」
- **eg 2（接着推进已有项目）**：「查一下我已有的影游项目和当前进度，告诉我下一步该做什么」
- **eg 3（局部提效）**：「读取项目《项目名》的第 1 个剧情节点，按规范拆镜并写好分镜提示词」
