---
name: daily
description: Create daily notes and manage morning/evening routines. Structure daily planning, task review, and reflection. Use for daily productivity routines or when asked to create today's note.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Daily Workflow Skill

Creates daily notes and provides structured workflows for morning planning and evening reflection.

## Usage

Invoke with `/daily` or ask Claude to create today's note.

### Create Today's Note
```
/daily
```

Or simply ask:
- "Create today's daily note"
- "Start my day"
- "Help me with evening reflection"

## Daily Note Creation

### What Happens
1. **Checks if today's note exists**
   - If yes: Opens the existing note
   - If no: Creates new note from template

2. **Template Processing**
   - Replaces `{{date}}` with today's date
   - Replaces `{{date:format}}` with formatted dates
   - Handles date arithmetic (e.g., `{{date-1}}` for yesterday)

3. **Automatic Organization**
   - Places note in `Daily Notes/` folder
   - Names file with today's date (YYYY-MM-DD.md)
   - Preserves template structure

### Template Variables
Your daily template can use:
- `{{date}}` - Today's date in default format
- `{{date:dddd}}` - Day name (e.g., Monday)
- `{{date:MMMM DD, YYYY}}` - Formatted date
- `{{date-1:YYYY-MM-DD}}` - Yesterday's date
- `{{date+1:YYYY-MM-DD}}` - Tomorrow's date
- `{{time}}` - Current time

## Morning Routine

### Steps
1. Create today's daily note (if not exists)
2. Pull incomplete tasks from yesterday
3. Identify today's ONE priority

### Morning Questions
- "What's your ONE thing for today?"
- "What might get in the way?"

## Evening Reflection

### Capture
1. Mark completed tasks with [x]
2. Add notes and learnings

### Reflect
- What went well today?
- What could be better?
- What did I learn?

### Prepare
1. Identify tomorrow's priority
2. Move incomplete tasks to tomorrow or delete
3. Commit changes (`/push`)

## Configuration

- Daily notes folder: `Daily Notes/`
- Template location: `Templates/Daily Template.md`
- Date format: `YYYY-MM-DD`

## Integration

Works with:
- `/push` - Commit end-of-day changes
- `/weekly` - Weekly planning uses daily notes
- `/onboard` - Load context before planning
