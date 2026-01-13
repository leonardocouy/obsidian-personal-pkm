---
name: weekly
description: Facilitate weekly review process with reflection and planning. Review past week's daily notes, identify patterns, plan next week. Use on Sundays or whenever doing weekly planning.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Weekly Review Skill

Facilitates your weekly review process by analyzing the past week's daily notes and helping plan the next week.

## Usage

Invoke with `/weekly` or ask Claude to help with your weekly review.

```
/weekly
```

## What This Skill Does

1. **Reviews Daily Notes**
   - Reads last 7 days of daily notes
   - Identifies completed and incomplete tasks
   - Spots patterns and themes

2. **Guides Reflection**
   - Reviews accomplishments
   - Identifies challenges
   - Captures lessons learned

3. **Plans Next Week**
   - Sets priorities for the week
   - Identifies key tasks
   - Suggests focus areas

## Review Process

### Step 1: Reflection (10 minutes)
- Review daily notes from past week
- Identify wins and challenges
- Capture lessons learned

### Step 2: Planning (10 minutes)
- Set ONE big thing for the week
- Identify key tasks
- Block time for important work

## Interactive Prompts

The skill guides you through:

1. **"What were your top 3 wins this week?"**
   - Celebrates progress
   - Builds momentum
   - Documents achievements

2. **"What were your main challenges?"**
   - Identifies obstacles
   - Plans solutions
   - Learns from difficulties

3. **"What's your ONE focus for next week?"**
   - Forces prioritization
   - Creates focus
   - Drives meaningful progress

## Weekly Review Output

```markdown
# Weekly Review: YYYY-MM-DD

## Last Week's Wins
1.
2.
3.

## Challenges & Lessons
- Challenge:
- Lesson:

## Next Week

### ONE Focus
>

### Key Tasks
- [ ]
- [ ]
- [ ]

## Notes
```

## Automation Features

### Auto-Archive
Suggest moving daily notes older than 30 days to Archives.

### Pattern Detection
- Identify recurring incomplete tasks
- Spot productivity patterns
- Highlight common themes

## Best Practices

### Consistent Timing
- Same day each week (Sunday recommended)
- Same time if possible
- Treat as non-negotiable

### Follow-through
- Commit changes after review (`/push`)
- Share highlights if relevant
- Celebrate wins

## Integration

Works with:
- `/daily` - Reviews daily notes from the week
- `/push` - Commit after completing review
- `/onboard` - Load context for informed review
