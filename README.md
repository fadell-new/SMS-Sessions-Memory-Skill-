# 🧠 SMS: Sessions Memory Skill

**SMS (Sessions Memory Skill)** is a behavioral framework designed to eliminate "context drift" in AI-driven software development. It provides a standardized method for AI agents to maintain a persistent, human-readable project state, ensuring seamless continuity across different sessions, models, and AI tools.

## 🚀 The Problem
AI agents often lose track of progress when a session ends, when context windows are cleared, or when switching between different AI tools. This leads to repetitive questions, redundant work, and "forgetting" key architectural decisions.

## 💡 The Solution
SMS solves this by implementing a **File-Based Memory** pattern. Instead of relying on the AI's short-term context window, it forces the AI to maintain a dedicated `status.md` file in the project root. This file serves as the "Single Source of Truth" for the project's current state.

## 🛠 How it Works

### 1. The Behavioral Directive
The core of the skill is located in `.claude/skills/sms.md`. This file contains the instructions that the AI follows to:
- **Trigger Updates**: Knowing exactly when to sync the status (e.g., after a milestone or before session end).
- **Maintain Schema**: Ensuring the `status.md` follows a consistent format.
- **Preserve History**: Following a "Read-Before-Write" rule to avoid erasing previous progress.

### 2. The Status Schema (`status.md`)
The framework tracks:
- **🎯 Current Objective**: The immediate priority.
- **✅ Completed**: A chronological list of finished tasks.
- **🚧 In Progress**: Current activity and any existing blockers.
- **⏳ Pending / Todo**: Future tasks and planned features.
- **📝 Notes & Context**: Critical "gotchas" and architectural decisions.

### 3. Tool Agnostic Integration
Because SMS is based on Markdown files, it is compatible with any AI tool that has filesystem access:
- **Claude Code**
- **OpenCode**
- **Cursor / Windsurf**
- **GitHub Copilot**

## 📖 Quick Start
1. Add the `.claude/skills/sms.md` file to your project.
2. Add a reference to the SMS skill in your `CLAUDE.md` or project instructions.
3. Invoke the skill (e.g., `/skill sms` in Claude Code) to initialize your `status.md`.

## 📄 License
MIT
