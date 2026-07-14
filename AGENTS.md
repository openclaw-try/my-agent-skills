# AGENTS.md — 园丁盒个人 AI 技能仓库 (my-agent-skills)

## 技能仓库定位
这是 `openclaw-try` 组织的全局 AI 技能与规范中心仓库。本仓库定义了所有可供加载的 Agent 技能，以及自动同步、备份和自进化的规则。

## AI 运作指引（启动钥匙）
当任何 AI 助手在开发中读取到本仓库或与之关联时，必须遵守以下指令：

1. **技能池架构 (Skills Pool Architecture)**:
   - 所有可用技能存放在 `pool/` 目录下。
   - 实际被 IDE 激活的技能应放置在用户全局配置 `~/.gemini/config/skills/` 目录下。

2. **按需激活决策 (Selective Installation)**:
   - 当用户要求配置当前开发项目（如 `try-teacher`）的技能时，AI 应：
     1. 读取当前工作区的开发特征（猜测技术栈与框架）。
     2. 从本地技能池 `pool/` 中提取与该项目最匹配的技能清单及简短简介。
     3. 在对话中以“配置建议书”形式呈现给用户，列出必选和可选建议。
     4. 获得用户确认后，将选中的技能目录复制到 `~/.gemini/config/skills/` 目录下激活。

3. **双向自动同步 (Bi-directional Sync)**:
   - **更新技能池**：从 GitHub `main` 分支拉取最新更新到 `skills_pool/` 目录下。
   - **备份修改**：将本地 `skills_pool/` 下的修改（如新建自定义技能）自动 commit 并 push 到 `openclaw-try/my-agent-skills`。

4. **自进化机制 (Self-Evolution)**:
   - 当用户通过 `/learn` 命令或口头要求 AI 学习特定偏好（编码风格、架构规范、提问格式）时，AI 应在全局或本项目的 `AGENTS.md` 中进行持久化写入。
   - 如果此偏好为通用技能规则，AI 应将其转化为新的自定义技能写入 `pool/` 目录下，并自动备份至本技能库。
