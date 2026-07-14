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
