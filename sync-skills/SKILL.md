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

