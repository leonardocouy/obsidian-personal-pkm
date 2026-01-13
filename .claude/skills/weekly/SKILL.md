---
name: weekly
description: Weekly review with blocker detection. Analyze past 7 days, identify stuck tasks (3+ days via wikilinks), calculate completion rate, plan next week. Use on Sundays or whenever doing weekly planning.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Weekly Review Skill

Facilitates your weekly review process by analyzing the past week's daily notes, detecting blockers via task wikilinks, and helping plan the next week.

## Usage

Invoke with `/weekly` on Sundays or whenever you do weekly planning.

```
/weekly
```

## What This Skill Does

### 1. Reviews Daily Notes
- Reads last 7 days of daily notes from `20_Daily Notes/YYYY/Mnn/`
- Counts completed vs incomplete tasks per day (wikilink format)
- Calculates completion rate

### 2. Detects Blockers (Task File Based)
- Identifies task wikilinks appearing 3+ days without completion
- Reads task files from `00_Inbox/Tasks/` for additional context
- Lists as blockers that need attention
- Shows task priority and due date from YAML frontmatter

### 3. Calculates KPIs
- Total tasks completed
- Total tasks incomplete
- Completion rate percentage
- Average tasks per day

### 4. Guides Reflection
- Reviews accomplishments
- Identifies challenges and patterns
- Captures lessons learned

### 5. Plans Next Week
- Creates weekly review note in `20_Daily Notes/YYYY/Mnn/YYYY-Www.md`
- Sets ONE focus for the week
- Identifies key tasks

## Blocker Detection

Tasks that appear in 3 or more days without being completed are flagged:

```markdown
## Blockers (3+ days without completion)

| Task | Days Stuck | Priority | Due Date |
|------|------------|----------|----------|
| [[Review PR 123]] | 4 days | high | 2026-01-15 |
| [[Update documentation]] | 3 days | medium | - |

These tasks may need:
- Breaking into smaller steps
- Removing blockers
- Delegating
- Dropping if not important
```

The skill reads each task file to show:
- Priority from YAML frontmatter
- Due date if set
- Scheduled date

## Weekly Review Output

The skill creates a weekly review note:

```markdown
# Weekly Review: 2026-W02

## Summary
- Days reviewed: 7
- Tasks completed: 23
- Tasks incomplete: 8
- Completion rate: 74%

## This Week's Wins
1.
2.
3.

## Challenges & Lessons
- Challenge:
- Lesson:

## Blockers (3+ days without completion)

| Task | Days Stuck | Priority | Due |
|------|------------|----------|-----|
| [[Task X]] | 4 days | high | 2026-01-20 |
| [[Task Y]] | 3 days | low | - |

## Next Week

### ONE Focus
>

### Key Tasks
- [ ] [[Task 1]]
- [ ] [[Task 2]]
- [ ] [[Task 3]]

## Notes
```

## Task Format

Tasks use **wikilinks** to reference task files:
- Incomplete: `- [ ] [[Task Name]]`
- Completed: `- [x] [[Task Name]] ✅ 2026-01-13`

Task files in `00_Inbox/Tasks/` have YAML frontmatter:
```yaml
---
tags: [task]
status: open
priority: high
due: 2026-01-20
scheduled: 2026-01-15
---
```

## Review Process

### Step 1: Data Collection (automatic)
- Scan daily notes from past 7 days
- Extract task completion data (wikilinks)
- Map which tasks appear on which days
- Identify recurring incomplete tasks

### Step 2: Task File Analysis
- For each blocker task, read `00_Inbox/Tasks/{Task Name}.md`
- Extract priority, due date, scheduled date
- Show context in blocker report

### Step 3: Reflection (10 minutes)
- Review wins and celebrate progress
- Analyze challenges and extract lessons
- Acknowledge blockers

### Step 4: Planning (10 minutes)
- Set ONE focus for next week
- Identify 3-5 key tasks
- Decide what to do with blockers

## Best Practices

### Consistent Timing
- Same day each week (Sunday recommended)
- Same time if possible
- Treat as non-negotiable

### Handle Blockers
For each blocker, decide:
- **Break down**: Split into smaller tasks
- **Unblock**: Identify and remove obstacle
- **Delegate**: Assign to someone else
- **Drop**: Remove if no longer important

### Follow-through
- Commit changes after review (`/push`)
- Share highlights if relevant
- Celebrate wins

## Integration

Works with:
- `/daily-setup` - Creates daily notes for the week
- `/daily-review` - Evening reflections aggregate here
- `/task-create` - Create new task files
- `/task-done` - Mark tasks as completed
- `/push` - Commit after completing review
- `/onboard` - Load context for informed review

## Requirements

- **TaskNotes plugin** - For task file management
- **Periodic Notes plugin** - For daily/weekly note structure
