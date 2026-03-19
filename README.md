# action-feishu - GitHub Action 飞书通知工具

## 功能介绍
`action-feishu` 是一个轻量级的 GitHub Action 插件，能够监听仓库的各类事件（如 Issue 创建/更新、Push、PR 等），并将事件信息格式化后推送到飞书群聊（通过飞书机器人 Webhook）。

## 快速开始

### 1. 配置飞书机器人
- 打开飞书群聊 → 设置 → 群机器人 → 添加机器人 → 选择「自定义机器人」
- 复制机器人的 **Webhook 地址**（后续需要配置到 GitHub Secrets）
- （可选）如需安全验证，可记录下「自定义关键词」（本 Action 已兼容关键词验证）

### 2. 配置 GitHub Action Workflow
在你的仓库 `.github/workflows` 目录下复制 `.github/workflows/notify-feishu.yml`，内容如下：

### 3. 配置 GitHub Secrets
在仓库 → Settings → Secrets and variables → Actions → New repository secret：
- 名称：`FEISHU_WEBHOOK_URL`
- 值：第一步复制的飞书机器人 Webhook 地址

## 环境变量说明

| 环境变量 | 必选 | 说明 |
|----------|------|------|
| `FEISHU_WEBHOOK_URL` | ✅ | 飞书机器人的 Webhook 地址 |
| `FEISHU_MESSAGE_TITLE` | ❌ | 通知消息的标题（其实用来填飞书机器人的自定义关键词） |

## Issue 增强功能

如果需要让 Issue 通知内容更美观、结构化，请确保你的仓库使用符合以下规范的 Issue 模板：

```
仓库模板路径：.github/ISSUE_TEMPLATE/
模板格式参考：https://github.com/laoshuikaixue/VoiceHub/tree/main/.github/ISSUE_TEMPLATE
```

✅ 增强效果：
- Issue 内容按模板字段拆分，结构化展示
- 自动提取关键信息（如类型、优先级、描述）

## 支持的事件类型
| 事件 | 说明 |
|------|------|
| `push` | 代码推送（含分支、提交信息、提交人） |
| `pull_request` | 合并请求（创建/更新/关闭） |
| `issues` | Issue 操作（创建/编辑/关闭/重开） |
| `release` | 版本发布 |