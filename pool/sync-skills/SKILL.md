---
name: sync-skills
description: Use when the user requests to update, sync, or upgrade their AI skills, or superpowers framework.
---

# Sync Skills

## Overview
This skill synchronizes the global AI skills directory with the latest community-best-practice skills from the `obra/superpowers` repository.

## Instructions for the AI Agent:

### 1. 同步与更新技能池 (Sync Upstream & Personal Repo)
当用户要求“更新技能”、“同步技能”或“升级技能”时，请针对技能池仓库执行操作：
1. **拉取个人仓库最新代码**：
   ```bash
   git -C /Users/wangpengcheng/.gemini/config/skills_pool pull origin main
   ```
2. **宣布完成**：告知用户技能池（skills_pool）已更新。

### 2. 备份自定义技能 (Backup Workflow)
当用户要求“备份技能”或“把技能 push 上去”时：
1. **提交并推送**：
   ```bash
   git -C /Users/wangpengcheng/.gemini/config/skills_pool add .
   git -C /Users/wangpengcheng/.gemini/config/skills_pool commit -m "update: sync custom skills"
   git -C /Users/wangpengcheng/.gemini/config/skills_pool push origin main
   ```
2. **同步本地 active 目录**：如果有修改 `sync-skills` 自身，确保将其同步复制回 `~/.gemini/config/skills/sync-skills/`。
3. **宣布完成**：告知用户所有自定义技能已成功备份到 GitHub！

### 3. 顾问式项目技能配置 (Advisory Skill Configuration Workflow)
当用户提到“配置当前项目技能”、“安装项目技能”或“读取项目钥匙”时，请执行以下顾问式匹配流程：

1. **读取项目钥匙**：
   - 检查项目根目录下是否存在 `AGENTS.md`。
   - 读取并提取其中的 `## AI 开发流钥匙` (或 `AI Skills Key`) 章节。
   - 解析出技能库链接 `Skills Repo`（如 `git@github.com:openclaw-try/my-agent-skills.git`）和声明使用的技能列表 `Required Skills` 或 `声明技能`。

2. **环境感知扫描**：
   - 扫描当前工作区的文件和配置，猜测技术栈：
     - 若包含 `package.json` 且其中包含 `jest`/`mocha`/`vitest`/`playwright`，或有 `tests/` 目录：推荐 `test-driven-development`。
     - 若包含复杂目录（多模块、MVC、多路由等）：推荐 `subagent-driven-development`。
     - 若包含多媒体格式（`.mp4`/`.wav`/`.mov` 等）：推荐 `video-editing`（如果技能池中存在）。

3. **整理建议书**：
   - 扫描本地 `~/.gemini/config/skills_pool/pool/` 下的所有技能，读取每个技能 `SKILL.md` 中的 `name` 和 `description`。
   - 构建一份顾问式的**技能配置建议书**，分门别类列出：
     - **🔑 项目声明必选 (Required)**
     - **💡 智能感知推荐 (Recommended)** 及其推荐原因。
     - **📦 技能池其他备选 (Optional)**。

4. **与用户交互确认**：
   - 将建议书发送在对话中，并礼貌地询问用户：
     > “我建议为您激活上述推荐技能。请问您是否需要调整此配置？（例如：‘同意推荐’、‘不要 TDD，加上 A 技能’）”
   - 等待用户回复。

5. **执行激活 (Apply)**：
   - 根据用户最终确认的技能列表，执行以下命令：
     1. 清空 `~/.gemini/config/skills/` 目录下除 `sync-skills` 之外的所有文件夹。
     2. 将用户确认的技能文件夹从 `~/.gemini/config/skills_pool/pool/<skill>` 复制到 `~/.gemini/config/skills/<skill>`。
   - 宣布激活成功，列出当前已激活的技能，引导用户开始开发。



