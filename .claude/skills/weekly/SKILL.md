---
name: weekly
description: Weekly review with blocker detection. Analyze past 7 days, identify stuck tasks (3+ days), plan next week. Use on Sundays or whenever doing weekly planning.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Weekly Review Skill

Facilitates your weekly review process by analyzing the past week's daily notes, detecting blockers, and helping plan the next week.

## Usage

Invoke with `/weekly` on Sundays or whenever you do weekly planning.

```
/weekly
```

## What This Skill Does

### 1. Reviews Daily Notes
- Reads last 7 days of daily notes from `Daily Notes/YYYY/Mnn/`
- Counts completed vs incomplete tasks per day
- Calculates completion rate

### 2. Detects Blockers
- Identifies tasks appearing 3+ days without completion
- Lists as blockers that need attention
- Helps surface systemic issues

### 3. Guides Reflection
- Reviews accomplishments
- Identifies challenges and patterns
- Captures lessons learned

### 4. Plans Next Week
- Creates weekly review note in `Daily Notes/YYYY/Mnn/YYYY-Www.md`
- Sets ONE focus for the week
- Identifies key tasks

## Blocker Detection

Tasks that appear in 3 or more days without being completed are flagged:

```markdown
## Blockers (3+ days without completion)
- [ ] Review PR #123 — 4 days consecutive
- [ ] Update documentation — 3 days consecutive

These tasks may need:
- Breaking into smaller steps
- Removing blockers
- Delegating
- Dropping if not important
```

## Weekly Review Output

The skill creates a weekly review note:

```markdown
# Weekly Review: 2025-W02

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
- [ ] Task X — 4 days consecutive
- [ ] Task Y — 3 days consecutive

## Next Week

### ONE Focus
>

### Key Tasks
- [ ]
- [ ]
- [ ]

## Notes
```

## Review Process

### Step 1: Data Collection (automatic)
- Scan daily notes from past 7 days
- Extract task completion data
- Identify recurring incomplete tasks

### Step 2: Reflection (10 minutes)
- Review wins and celebrate progress
- Analyze challenges and extract lessons
- Acknowledge blockers

### Step 3: Planning (10 minutes)
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
- `/push` - Commit after completing review
- `/onboard` - Load context for informed review
