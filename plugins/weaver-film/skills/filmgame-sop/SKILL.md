---
name: filmgame-sop
description: 互动影游创作入口。用于剧本策划、剧情树和分支、角色场景道具、资产出图、图片提示词、分镜运镜、镜头视频与高清，以及直接写入或 CRUD。
metadata:
  keywords: "影游, 互动影游, 剧本策划, 剧情树, 分支, 角色, 场景, 道具, 资产, 图片提示词, 出图, 分镜, 运镜, 镜头视频, 高清, 直接写入, CRUD"
---

# 影游创作入口

## 核心原则

调用任何影游写入、修改或 AI 生成工具前，**必须**通过 `get_workflow_guide(name="指南名")` 或 `skills/get` 读取服务端最新的阶段指南和相关专业规范。按指南检查画布锁并编写正文或提示词，切勿凭记忆创作或跳过锁检查。

## 服务端指南速查

| 指南 | 何时读取 |
| --- | --- |
| `filmgame-sop` | 首次接入、选择当前阶段或确认完整流程 |
| `filmgame-script` | 故事设定、人物体系、剧情节拍、全局路线或剧本大纲 |
| `filmgame-story-tree` | 设计分支、连线、剧情节点或补写正文 |
| `filmgame-assets` | 建立角色、场景、道具资产，补提示词或出图 |
| `filmgame-storyboard` | 拆镜、编排镜头、修改分镜提示词 |
| `filmgame-video` | 批量生成镜头视频、查任务或做高清超分 |
| `filmgame-writing` | 编写或修改策划正文、剧情树骨架或节点正文 |
| `filmgame-image-prompt` | 写资产图片提示词，确认构图与画风的分工 |
| `filmgame-video-prompt` | 写分镜、运镜及视频提示词，核对素材引用 |

## 基础约定

先用 `list_projects` 找项目，或用 `create_project` 新建。用 `get_project_progress` 查进度后，再选择阶段指南。OAuth 2.1 注入身份，无需传 `userId`。项目级工具传 `projectId`。调用破坏性删除工具前，须取得用户明确确认。
