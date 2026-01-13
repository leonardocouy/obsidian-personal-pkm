# Task Create Command

Creates a new task file with proper YAML frontmatter and adds a wikilink to today's daily note.

## Usage

```
/task-create "Task Name"
/task-create "Task Name" --priority high
/task-create "Task Name" --due 2026-01-20
/task-create
```

If no task name is provided, prompt the user for one.

## Workflow

### 1. Get Task Details

If task name not provided as argument:
```
What's the task name?
> [User input]
```

Ask for priority:
```
Priority? (low/medium/high) [default: medium]
> [User input or enter for default]
```

Ask for due date (optional):
```
Due date? (YYYY-MM-DD or leave empty)
> [User input or empty]
```

### 2. Create Task File

Create file at: `00_Inbox/Tasks/{Task Name}.md`

Content:
```yaml
---
tags:
  - task
status: open
priority: {priority}
due: {due_date if provided}
scheduled: {today's date YYYY-MM-DD}
projects: []
---

# {Task Name}

## Description


## Notes

```

### 3. Add to Daily Note

Find today's daily note: `20_Daily Notes/YYYY/Mnn/YYYY-MM-DD.md`

If it exists, add wikilink to the Tasks section:
```markdown
- [ ] [[Task Name]]
```

Add under "### Must Do" or "### Work" section based on priority:
- high → Must Do
- medium/low → Work

### 4. Confirm Creation

```
✅ Task created!

📄 File: 00_Inbox/Tasks/{Task Name}.md
📋 Added to: 20_Daily Notes/2026/M01/2026-01-13.md
📊 Priority: {priority}
📅 Due: {due_date or "not set"}

Task is ready to work on!
```

## Examples

### Basic task
```
/task-create "Review PR 123"

✅ Task created!
📄 File: 00_Inbox/Tasks/Review PR 123.md
📋 Added to: 20_Daily Notes/2026/M01/2026-01-13.md
📊 Priority: medium
📅 Due: not set
```

### High priority with due date
```
/task-create "Fix production bug" --priority high --due 2026-01-15

✅ Task created!
📄 File: 00_Inbox/Tasks/Fix production bug.md
📋 Added to: 20_Daily Notes/2026/M01/2026-01-13.md
📊 Priority: high
📅 Due: 2026-01-15
```

### Interactive mode
```
/task-create

What's the task name?
> Write documentation for API

Priority? (low/medium/high) [default: medium]
> high

Due date? (YYYY-MM-DD or leave empty)
> 2026-01-20

✅ Task created!
📄 File: 00_Inbox/Tasks/Write documentation for API.md
```

## Edge Cases

### Daily Note Doesn't Exist
If today's daily note doesn't exist, suggest running `/daily-setup` first:
```
⚠️ Today's daily note doesn't exist yet.
Run /daily-setup first, or I can create just the task file.

Create task file only? (yes/no)
```

### Task File Already Exists
If task file already exists, ask:
```
⚠️ Task file already exists: 00_Inbox/Tasks/{Task Name}.md

Options:
1. Add to daily note anyway (don't overwrite task file)
2. Choose a different name
3. Cancel

What would you like to do?
```

### Invalid Characters in Name
Sanitize filename by removing: `/ \ : * ? " < > |`
Inform user if name was modified.

## Integration

Works with:
- `/task-done` - Mark task as completed
- `/daily-setup` - Creates daily note where tasks are added
- `/daily-review` - Reviews task completion
