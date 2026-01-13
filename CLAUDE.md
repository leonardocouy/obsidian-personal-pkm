# Personal PKM Vault - Claude Instructions

This is a personal knowledge management vault designed to work seamlessly with Claude Code and TaskNotes plugin for task management.

## Vault Structure

```
.
├── 00_Inbox/
│   └── Tasks/             # TaskNotes task files (one file per task)
│       ├── Task Name.md
│       └── ...
├── 20_Daily Notes/        # Organized by year/month
│   └── YYYY/
│       └── Mnn/
│           ├── YYYY-MM-DD.md    # Daily notes
│           └── YYYY-Www.md      # Weekly reviews
├── Templates/
│   ├── Daily Template.md  # Daily note structure
│   └── Task Template.md   # Task file structure
├── Archives/              # Old/completed notes
└── .claude/
    ├── skills/            # /daily-setup, /daily-review, /weekly, /push, /onboard
    ├── commands/          # /task-create, /task-done
    └── agents/            # note-organizer
```

## Task Management (TaskNotes Integration)

Tasks are stored as **individual markdown files** in `00_Inbox/Tasks/` and referenced via **wikilinks** in daily notes.

### Task File Format

```yaml
---
tags:
  - task
status: open              # open, in-progress, done
priority: medium          # low, medium, high
due: 2026-01-20           # optional deadline
scheduled: 2026-01-15     # when to work on it
projects: []              # optional project links
---

# Task Name

Description and notes.
```

### Task References in Daily Notes

```markdown
- [ ] [[Task Name]]              # Incomplete task (wikilink)
- [x] [[Task Name]] ✅ 2026-01-13 # Completed task with timestamp
```

### Task Workflow

1. Create task: `/task-create "Task Name"` or manually in `00_Inbox/Tasks/`
2. Reference in daily note: `- [ ] [[Task Name]]`
3. Complete task: `/task-done "Task Name"` or manually mark `[x]`
4. Task file status updated: `status: done`

## Available Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `/task-create` | Create new task file with YAML, add to daily note | When adding tasks |
| `/task-done` | Mark task complete, update daily note and task file | When finishing tasks |

## Available Skills

| Skill | Description | Usage |
|-------|-------------|-------|
| `/daily-setup` | Morning routine - create note, pull tasks (wikilinks), auto-reschedule | Start of day |
| `/daily-review` | Evening routine - reflect, add timestamps, update task status | End of day |
| `/weekly` | Weekly review with blocker detection (via task files) | Sunday reviews |
| `/push` | Commit and push to Git | After making changes |
| `/onboard` | Load vault context | Start of session |

## Available Agents

| Agent | Description |
|-------|-------------|
| `note-organizer` | Process inbox, organize notes, maintain vault hygiene |

## Conventions

### File Naming
- Daily notes: `YYYY-MM-DD.md` in `20_Daily Notes/YYYY/Mnn/`
- Weekly reviews: `YYYY-Www.md` in same folder as daily notes
- Task files: `Task Name.md` in `00_Inbox/Tasks/`
- Templates: Descriptive name with "Template" suffix

### Folders
- `00_Inbox/Tasks/` - TaskNotes task files
- `20_Daily Notes/YYYY/Mnn/` - Organized by year and month
- `Templates/` - Reusable note templates
- `Archives/` - Old notes, completed items

### Tags
- `#daily-note` - Daily notes
- `#task` - Task files (required for TaskNotes)
- `#inbox` - Items to process
- `#archived` - Archived notes

## Workflow

### Morning
1. `/daily-setup` - Create today's note with yesterday's context
2. Review tasks to continue (auto-rescheduled if overdue)
3. Set ONE focus
4. Add new tasks with `/task-create`
5. `/push` - Commit changes

### During Day
- Create tasks: `/task-create "New task"`
- Complete tasks: `/task-done "Task name"`
- Capture ideas in 00_Inbox/
- Update daily note as needed

### Evening
1. `/daily-review` - Reflect on day
2. Complete reflection prompts
3. Review task completions (timestamps added)
4. Set tomorrow's priority
5. `/push` - Commit changes

### Weekly
1. `/weekly` - Run weekly review with blocker detection
2. Review blockers (tasks appearing 3+ days in wikilinks without completion)
3. Plan next week
4. Process 00_Inbox/
5. `/push` - Commit changes

## Communication

- **Language**: Portuguese (pt-BR) for interaction
- **Content**: English for note content and documentation
- **Style**: Direct, concise responses

## Notes for Claude

### File Locations
- Daily notes: `20_Daily Notes/YYYY/Mnn/YYYY-MM-DD.md`
- Weekly reviews: `20_Daily Notes/YYYY/Mnn/YYYY-Www.md`
- Task files: `00_Inbox/Tasks/{Task Name}.md`
- Templates: `Templates/`

### Task Operations
- Tasks use wikilinks: `- [ ] [[Task Name]]`
- Completed tasks: `- [x] [[Task Name]] ✅ YYYY-MM-DD`
- Task files have YAML frontmatter with `status`, `priority`, `due`, `scheduled`
- `/daily-setup` reads task files to check `scheduled` date and auto-reschedules
- `/daily-review` updates task file `status: done` when completed
- `/weekly` detects blockers by tracking wikilinks across 7 days

### Best Practices
- Always check if note/file exists before creating
- Use templates from `Templates/` folder
- Respect user's folder structure (00_, 20_ prefixes)
- Ask before moving or deleting files
- Commit changes with meaningful messages
- Read task files to get priority/due context for blockers

## Requirements

- **Obsidian** with these plugins:
  - **Periodic Notes** - For daily/weekly note structure
  - **TaskNotes** - For task file management
