# Weaver Marketplace

Weaver 影游创作的 Codex 插件目录（**test 测试环境分支**）。当前提供 `weaver-film@weaver`，连接 [Weaver 远程 MCP（测试环境）](https://api.yy.vi-relay.com/api/v1/mcp/film)，使用自己的 Weaver 测试环境账号完成 OAuth 授权。

## 安装

### Codex CLI

在终端添加 marketplace、安装影游插件，再完成 Weaver OAuth 授权。

```bash
codex plugin marketplace add https://github.com/jackmeng/weaver-agent-kit.git --ref test
codex plugin add weaver-film@weaver
codex mcp login weaver-film
```

### ChatGPT Desktop 本地安装（Codex 模式）

1. 首次使用时，在终端执行上面的 `codex plugin marketplace add` 命令。
2. 在 ChatGPT Desktop 的 **Plugins（插件）** 中选择 **Weaver (影游创作平台)**，打开 **Weaver 影游创作** 并安装。如果刚添加 marketplace 后没有看到它，重启 Desktop 后再检查。
3. 如果 Desktop 提示连接 Weaver，按提示完成 OAuth 授权。
4. 在 Desktop 的 **Codex 模式** 新建本地会话，通过 `@` 选择已安装的 Weaver 插件。

macOS 上也可以在添加 marketplace 后从终端打开插件详情页。

```bash
open 'codex://plugins/install/weaver-film?marketplace=weaver'
```

### ChatGPT Work Mode

这个仓库提供 Codex 本地 marketplace。当前尚未验证通过该 marketplace 安装的 Weaver 能在 ChatGPT Work Mode 调用 MCP 工具。插件显示已安装或能读取创作指南时，仍需在 Work Mode 新会话中实际调用 `list_projects` 验收。

在具备自定义 MCP 创建权限的 Business、Enterprise 或 Edu 工作区，可以在 ChatGPT 网页端打开 **Plugins → + → Add custom MCP server**，填写 `https://api.yy.vi-relay.com/api/v1/mcp/film`，创建插件并按提示完成 OAuth。再在 Work Mode 新建会话，选中该插件并测试 `list_projects`。个人 Plus 用户可以按上文使用 Codex CLI，或在 Desktop 的 Codex 模式验证本地安装。

参考 [OpenAI 自定义 MCP 接入说明](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt)。

## 首次验证

安装并授权后，新开一个你准备使用的会话，发送：

> 使用 Weaver 的 `list_projects` 工具查看我的影游项目。

工具实际返回项目列表即接入成功，空列表也算。CLI 和 Desktop 的结果分别验证。

## 更新

```bash
codex plugin marketplace upgrade weaver
codex plugin add weaver-film@weaver
```

更新后新开会话，再运行一次「首次验证」。如果通过 GitHub 地址添加了 marketplace，更新以 GitHub 上的 `test` 为准，本地未推送的修改不会出现在这次更新里。

## 排查

| 现象 | 检查 |
| --- | --- |
| Desktop 找不到 Weaver | 确认已添加 `weaver` marketplace，重启 Desktop 后从 Plugins 进入，或在 macOS 用上面的链接打开详情页。 |
| Weaver 提示未授权 | 从 Desktop 的连接提示完成授权。CLI 可执行 `codex mcp login weaver-film`。 |
| 授权后仍找不到 `list_projects` | 新开会话，确认当前使用的是 Desktop Codex 还是 Work Mode，再对照上面的接入方式验证。工具缺失时无法通过首次验证。 |

## 随包 Skill

`filmgame-sop` 是影游创作入口，覆盖剧本、剧情树、资产、分镜和视频。阶段指南与专业创作规范由远程 MCP 的 `get_workflow_guide` 提供。

 
## 其他客户端

### WorkBuddy

直接将下面话术发送给 WorkBuddy：

```text
帮我在 WorkBuddy 中连接 Weaver Remote MCP，让我可以在这里创作互动影游。

1. 新增一个名为 Weaver 的远程 HTTP MCP 连接器，地址填 `https://api.yy.vi-relay.com/api/v1/mcp/film`
2. 写入后提醒我去连接器管理页点击 Trust（信任）并完成 Weaver 账户 OAuth 授权
3. 授权就绪后告诉我，并给出 3 个可直接开始的创作示例（eg）
```

> 如配置中存在旧的本地测试连接器（如 `filmgame-local`），建议移除后再使用云端 `Weaver`，避免工具名冲突。

### Claude / Hermes / 通用 Remote MCP 客户端

直接将下面话术发送给 Claude 或其他支持远程 MCP 连接器的客户端：

```text
帮我在 当前Agent 中连接 Weaver Remote MCP，让我可以在这里创作互动影游。

1. 新建一个名为 Weaver 的连接器
2. 连接地址填 `https://api.yy.vi-relay.com/api/v1/mcp/film`
3. 保存后完成 Weaver 账户授权
4. 授权就绪后告诉我，并给出 3 个可直接开始的创作示例（eg）
```

## 创作示例

授权完成后，直接把下面任一句发给你的 Agent 即可：

- **eg 1（从零创作）**：「帮我从零创作一个悬疑反转题材的互动影游，先完成剧本策划」
- **eg 2（接着推进已有项目）**：「查一下我已有的影游项目和当前进度，告诉我下一步该做什么」
- **eg 3（局部提效）**：「读取项目《项目名》的第 1 个剧情节点，按规范拆镜并写好分镜提示词」
