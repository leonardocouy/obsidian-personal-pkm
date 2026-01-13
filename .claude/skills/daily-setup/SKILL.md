---
name: daily-setup
description: Morning routine - create today's daily note, pull incomplete tasks from yesterday (via wikilinks), auto-reschedule overdue tasks. Use at the start of your day.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Daily Setup Skill

Creates today's daily note and automatically pulls context from yesterday to help you start your day with clarity. Integrates with TaskNotes plugin for task management via wikilinks.

## Usage

Invoke with `/daily-setup` in the morning.

```
/daily-setup
```

Or ask:
- "Start my day"
- "Create today's note"
- "Morning routine"

## What This Skill Does

### 1. Creates Today's Note
- Checks if today's note exists in `20_Daily Notes/YYYY/Mnn/`
- If not, creates from `Templates/Daily Template.md`
- Uses proper folder structure: `20_Daily Notes/2026/M01/2026-01-15.md`

### 2. Reads Yesterday's Note
- Finds yesterday's daily note
- Extracts completed tasks: `- [x] [[Task Name]]`
- Extracts incomplete tasks: `- [ ] [[Task Name]]` (wikilink format)
- Gets any insights from Reflection section

### 3. Processes Task Files (TaskNotes Integration)
For each incomplete task wikilink found:
- Read task file from `00_Inbox/Tasks/{Task Name}.md`
- Parse YAML frontmatter
- If `scheduled` date < today: update to today's date
- This auto-reschedules overdue tasks

### 4. Populates Today's Note
- **Yesterday Summary**: What was accomplished yesterday
- **Tasks to Continue**: Incomplete tasks carried forward (as wikilinks)
- Shows a quick summary to the user

## Folder Structure

Notes are organized by year and month:
```
20_Daily Notes/
├── 2026/
│   ├── M01/
│   │   ├── 2026-01-13.md
│   │   ├── 2026-01-14.md
│   │   └── 2026-01-15.md
│   └── M02/
│       └── ...
```

Task files are stored in:
```
00_Inbox/
└── Tasks/
    ├── Review PR 123.md
    ├── Update documentation.md
    └── ...
```

## Task Format

Tasks use **wikilinks** to reference task files:
- Incomplete: `- [ ] [[Task Name]]`
- Completed: `- [x] [[Task Name]] ✅ 2026-01-13`

Each task file has YAML frontmatter:
```yaml
---
tags: [task]
status: open          # open, in-progress, done
priority: medium      # low, medium, high
due: 2026-01-20       # optional deadline
scheduled: 2026-01-15 # when to work on it
projects: []          # optional project links
---
```

## Template Variables

The daily template supports:
- `{{date}}` - Today's date (YYYY-MM-DD)
- `{{date:dddd, MMMM DD, YYYY}}` - Formatted date
- `{{date-1:YYYY-MM-DD}}` - Yesterday's date
- `{{date+1:YYYY-MM-DD}}` - Tomorrow's date

## Morning Workflow

1. Run `/daily-setup`
2. Review yesterday's summary
3. Check tasks to continue (auto-rescheduled if overdue)
4. Set today's ONE priority in Focus section
5. Add new tasks with `/task-create`

## Example Output

```
Good morning! Here's your daily setup:

Created: 20_Daily Notes/2026/M01/2026-01-15.md

Yesterday's Summary:
- Completed 5 tasks
- Finished project proposal
- Had team meeting

Tasks to Continue:
- [ ] [[Review PR 123]] (rescheduled from 2026-01-14)
- [ ] [[Update documentation]]

What's your ONE focus for today?
```

## Edge Cases

### Early Morning (before 4 AM)
If running before 4 AM, considers "yesterday" as 2 days ago to handle late-night sessions properly.

### No Yesterday Note
If yesterday's note doesn't exist, creates today's note with empty Yesterday Summary section.

### First Day of Month
Creates new month folder (e.g., `M02/`) automatically.

### Task File Not Found
If a wikilink references a task file that doesn't exist, it's still carried over but without auto-rescheduling.

## Integration

Works with:
- `/daily-review` - Evening companion skill
- `/weekly` - Weekly reviews use daily notes
- `/task-create` - Create new task files
- `/task-done` - Mark tasks as completed
- `/push` - Commit after setup
- `/onboard` - Load full vault context

## Requirements

- **TaskNotes plugin** - For task file management and inline widgets
- **Periodic Notes plugin** - For daily note structure
