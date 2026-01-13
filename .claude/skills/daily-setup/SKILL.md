---
name: daily-setup
description: Morning routine - create today's daily note, pull incomplete tasks from yesterday, show yesterday's summary. Use at the start of your day.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Daily Setup Skill

Creates today's daily note and automatically pulls context from yesterday to help you start your day with clarity.

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
- Checks if today's note exists in `Daily Notes/YYYY/Mnn/`
- If not, creates from `Templates/Daily Template.md`
- Uses proper folder structure: `Daily Notes/2025/M01/2025-01-15.md`

### 2. Reads Yesterday's Note
- Finds yesterday's daily note
- Extracts completed tasks (lines with `[x]`)
- Extracts incomplete tasks (lines with `[ ]`)
- Gets any insights from Reflection section

### 3. Populates Today's Note
- **Yesterday Summary**: What was accomplished yesterday
- **Tasks to Continue**: Incomplete tasks carried forward
- Shows a quick summary to the user

## Folder Structure

Notes are organized by year and month:
```
Daily Notes/
├── 2025/
│   ├── M01/
│   │   ├── 2025-01-13.md
│   │   ├── 2025-01-14.md
│   │   └── 2025-01-15.md
│   └── M02/
│       └── ...
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
3. Check tasks to continue
4. Set today's ONE priority in Focus section
5. Add any new tasks

## Example Output

```
Good morning! Here's your daily setup:

Created: Daily Notes/2025/M01/2025-01-15.md

Yesterday's Summary:
- Completed 5 tasks
- Finished project proposal
- Had team meeting

Tasks to Continue:
- [ ] Review PR #123
- [ ] Update documentation

What's your ONE focus for today?
```

## Edge Cases

### Early Morning (before 4 AM)
If running before 4 AM, considers "yesterday" as 2 days ago to handle late-night sessions properly.

### No Yesterday Note
If yesterday's note doesn't exist, creates today's note with empty Yesterday Summary section.

### First Day of Month
Creates new month folder (e.g., `M02/`) automatically.

## Integration

Works with:
- `/daily-review` - Evening companion skill
- `/weekly` - Weekly reviews use daily notes
- `/push` - Commit after setup
- `/onboard` - Load full vault context
