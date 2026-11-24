# YingYou Plugin Marketplace & Remote MCP 接入

影游创作平台（YingYou / FilmGame）官方 **Codex Plugin Marketplace** 与远程 MCP 接入指南。

详细 SOP、阶段指南与专业创作规范均由服务端 `get_workflow_guide` 实时下发，服务端更新后全客户端即时生效，无需重复更新本地文件。

---

## 一、开放 MCP 端点

对外统一基址：`https://api.yy.vi-relay.com/api/v1/`

| 业务线 / 场景 | 远程 MCP 地址 | 适用场景 |
| --- | --- | --- |
| 影游（全量） | `https://api.yy.vi-relay.com/api/v1/mcp/film` | 完整影游项目、剧本策划、剧情树、资产、分镜、视频与高清 |
| 影游（剧本场景） | `https://api.yy.vi-relay.com/api/v1/mcp/film/script` | 仅需项目管理、剧本策划与剧情树时使用（工具数精简） |
| 影游（资产场景） | `https://api.yy.vi-relay.com/api/v1/mcp/film/assets` | 仅需角色/场景/道具资产、音色与出图时使用 |
| 影游（分镜与视频场景） | `https://api.yy.vi-relay.com/api/v1/mcp/film/storyboard` | 仅需拆镜、镜头提示词、视频生成与高清时使用 |
| 短剧（演示） | `https://api.yy.vi-relay.com/api/v1/mcp/drama` | 短剧六步创作流程演示 |

---

## 二、一键复制接入话术

### 1. Codex（CLI / Desktop App）— 插件市场安装

直接将下面话术发送给 Codex：

```text
帮我安装 YingYou 影游插件，让我可以在这里创作互动影游。

1. 添加插件目录：执行 `codex plugin marketplace add https://github.com/jackmeng/yingyou-agent-kit.git --ref main`
2. 安装插件：执行 `codex plugin add yingyou-film@yingyou`
3. 新建任务后完成 YingYou 账户授权
4. 授权就绪后告诉我，并给出 3 个可直接开始的创作示例（eg）
```

> 短剧演示插件请将第 2 步改为 `codex plugin add yingyou-drama@yingyou`；日常升级执行 `codex plugin marketplace upgrade yingyou`。

### 2. WorkBuddy

直接将下面话术发送给 WorkBuddy：

```text
帮我在 WorkBuddy 中连接 YingYou Remote MCP，让我可以在这里创作互动影游。

1. 新增一个名为 YingYou 的远程 HTTP MCP 连接器，地址填 `https://api.yy.vi-relay.com/api/v1/mcp/film`
2. 写入后提醒我去连接器管理页点击 Trust（信任）并完成 YingYou 账户 OAuth 授权
3. 授权就绪后告诉我，并给出 3 个可直接开始的创作示例（eg）
```

> 如配置中存在旧的本地测试连接器（如 `filmgame-local`），建议移除后再使用云端 `YingYou`，避免工具名冲突。

### 3.Claude / Hermes / 通用 Remote MCP 客户端

直接将下面话术发送给 Hermes 或其他支持远程 MCP 连接器的客户端：

```text
帮我在 Hermes 中连接 YingYou Remote MCP，让我可以在这里创作互动影游。

1. 新建一个名为 YingYou 的连接器
2. 连接地址填 `https://api.yy.vi-relay.com/api/v1/mcp/film`
3. 保存后完成 YingYou 账户授权
4. 授权就绪后告诉我，并给出 3 个可直接开始的创作示例（eg）
```
---

## 三、授权后开场示例（eg）

授权完成后，直接把下面任一句发给你的 Agent 即可：

- **eg 1（从零创作）**：「帮我从零创作一个悬疑反转题材的互动影游，先完成剧本策划」
- **eg 2（接着推进已有项目）**：「查一下我已有的影游项目和当前进度，告诉我下一步该做什么」
- **eg 3（局部提效）**：「读取项目《项目名》的第 1 个剧情节点，按规范拆镜并写好分镜提示词」

---

## 四、仓库结构

```text
.
├── README.md
├── .agents/
│   └── plugins/
│       └── marketplace.json                          # Codex 插件市场索引
└── plugins/
    ├── yingyou-film/                                 # 影游插件包
    │   ├── .codex-plugin/plugin.json
    │   ├── .mcp.json
    │   └── skills/filmgame-sop/SKILL.md
    └── yingyou-drama/                                # 短剧插件包
        ├── .codex-plugin/plugin.json
        ├── .mcp.json
        └── skills/shortdrama-sop/SKILL.md
```
