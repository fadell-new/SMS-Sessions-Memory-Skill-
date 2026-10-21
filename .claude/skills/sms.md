# SMS (Sessions Memory Skill)

The SMS skill ensures that the AI maintains a persistent, human-readable state of the project to eliminate "context drift" between different sessions and AI agents.

## 🎯 Goal
Maintain a `status.md` file in the project root that tracks the current objective, completed work, and pending tasks.

## 🚀 Triggers
You MUST invoke this skill and update `status.md` during the following events:
1. **Initialization**: When first starting work on a project or when this skill is first invoked.
2. **Significant Milestones**: After completing a feature, fixing a major bug, or finishing a planning phase.
3. **Session End**: Immediately before ending a session or stopping work for the day.
4. **Context Shift**: When switching from one major task or objective to another.

## 📋 `status.md` Schema
Maintain the following structure in the project root:

```markdown
# Project Status: [Project Name]
Last Updated: [YYYY-MM-DD HH:mm]

## 🎯 Current Objective
(The single most important goal currently being pursued)

## ✅ Completed
- [x] Task A (Completed on Date)
- [x] Task B (Completed on Date)

## 🚧 In Progress
- [ ] Task C (Current status, blockers, or next immediate step)

## ⏳ Pending / Todo
- [ ] Task D (Planned)
- [ ] Task E (Future consideration)

## 📝 Notes & Context
(Crucial architectural decisions, "gotchas," or references to specific files that the next session needs to know)
```

## 🛠 Update Rules
- **Read-Before-Write**: Always read the existing `status.md` before updating it to preserve history.
- **Incremental Updates**: Append to the "Completed" section; do not overwrite previous achievements.
- **Atomic Updates**: Update the "Current Objective" and "In Progress" sections to reflect the exact state of the working tree.
- **Timestamping**: Always update the "Last Updated" timestamp.

## 🏁 Initialization Process
If `status.md` does not exist:
1. Analyze the current codebase, folder structure, and git history (if available).
2. Identify completed milestones and pending goals.
3. Create the `status.md` file using the schema above.
