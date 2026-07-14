---
name: sync-skills
description: Use when the user requests to update, sync, or upgrade their AI skills, or superpowers framework.
---

# Sync Skills

## Overview
This skill synchronizes the global AI skills directory with the latest community-best-practice skills from the `obra/superpowers` repository.

## Instructions for the AI Agent:
When this skill is triggered (e.g., when the user asks to "sync skills", "update skills", or "upgrade superpowers"), perform the following steps:

1. **Announce Start**: Say "I am using the sync-skills skill to update your global AI skills from obra/superpowers."
2. **Clone Upstream Repository**:
   Run a command in the current workspace directory to clone the latest superpowers repository:
   ```bash
   git clone --depth 1 https://github.com/obra/superpowers.git .git_superpowers_tmp
   ```
3. **Copy to Global Config**:
   Copy the contents of the `skills/` folder from the cloned repository to the global skills directory:
   ```bash
   mkdir -p /Users/wangpengcheng/.gemini/config/skills
   cp -r .git_superpowers_tmp/skills/* /Users/wangpengcheng/.gemini/config/skills/
   ```
4. **Clean Up**:
   Remove the temporary cloned repository:
   ```bash
   rm -rf .git_superpowers_tmp
   ```
5. **Acknowledge Completion**:
   Inform the user that the global skills have been successfully updated to the latest version of `obra/superpowers`!

## Backing Up Personal Skills (Backup Workflow)
When the user asks to "backup skills" or "push skills to my repository/marketplace":
1. **Announce Start**: Say "I am backing up your custom skills to your GitHub repository (openclaw-try/my-agent-skills)."
2. **Commit and Push**:
   Run the following commands:
   ```bash
   git -C /Users/wangpengcheng/.gemini/config/skills add .
   git -C /Users/wangpengcheng/.gemini/config/skills commit -m "update: sync custom skills"
   git -C /Users/wangpengcheng/.gemini/config/skills push origin main
   ```
3. **Acknowledge Completion**: Inform the user that the local skills have been successfully backed up to GitHub!

## Restoring/Syncing Personal Skills (Pull Workflow)
When the user asks to "sync my personal skills" or "pull skills from my repository":
1. **Announce Start**: Say "I am pulling the latest skills from your personal repository (openclaw-try/my-agent-skills)."
2. **Pull Updates**:
   Run the following command:
   ```bash
   git -C /Users/wangpengcheng/.gemini/config/skills pull origin main
   ```
3. **Acknowledge Completion**: Inform the user that their local skills are now up to date with their GitHub repository!

## Interactive Selective Installation (Marketplace Selector)
When the user asks to "selectively install skills", "choose skills to install" or "install skills from my repo/marketplace":
1. **Announce Start**: Say "I am fetching the available skills list from your repository to let you choose which ones to install."
2. **Clone Repo to Temp**:
   Clone the repository to a temporary directory in the current workspace:
   ```bash
   git clone --depth 1 ssh://git@ssh.github.com/openclaw-try/my-agent-skills.git .git_skills_temp
   ```
3. **Scan Available Skills**:
   Scan all folders inside `.git_skills_temp/` (excluding git files, docs, etc.) that contain a `SKILL.md` file. Parse each `SKILL.md`'s YAML frontmatter to extract the skill `name` and `description`.
4. **Present Selector to User**:
   Call the `ask_question` tool with a single question:
   - `question`: "请选择您想要安装的技能 (Select the skills you want to install):"
   - `is_multi_select`: `true`
   - `options`: List each skill formatted as: `"[Skill Name] - [Description]"` (e.g. `"brainstorming - Use before any creative work to explore intent"`)
5. **Install Selected Skills**:
   Once the user submits their choices:
   - For each selected skill, copy its folder from `.git_skills_temp/<skill_folder>` to `/Users/wangpengcheng/.gemini/config/skills/<skill_folder>`.
6. **Clean Up**:
   Delete the `.git_skills_temp` folder.
7. **Acknowledge Completion**:
   Report the list of successfully installed skills and explain how the user can trigger them.


