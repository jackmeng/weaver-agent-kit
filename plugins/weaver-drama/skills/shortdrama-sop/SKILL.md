---
name: shortdrama-sop
description: 短剧创作入口，适用于故事设定、角色体系、剧情节拍、分集大纲、分集剧本、资产出图、分镜与镜头视频。
metadata:
  keywords: "短剧, 故事设定, 角色, 节拍, 分集大纲, 剧本, 资产, 出图, 分镜, 镜头视频"
---

# 短剧创作入口

调用任何短剧写入、修改或 AI 生成工具前，**必须**先用 `get_workflow_guide(name="指南名")` 或 `skills/get` 读取服务端最新阶段指南，按其中的顺序和验收规则执行。

| 指南 | 何时读取 |
| --- | --- |
| `shortdrama-sop` | 首次接入、定位当前制作阶段或确认总流程 |
| `shortdrama-story-setting` | 创作故事设定、人物、剧情节拍或分集大纲 |
| `shortdrama-script` | 读取原稿、生成或修改分集剧本 |
| `shortdrama-assets` | 整理角色、场景、道具或生成形象图 |
| `shortdrama-storyboard` | 生成分镜、编辑镜头或生成视频 |

先用 `get_project_detail` 查看作品。有原稿时，可调用 `get_source_script`。OAuth 2.1 注入身份，无需传 `userId`，项目级工具传 `projectId`。
