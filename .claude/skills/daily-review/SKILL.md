---
name: daily-review
description: Evening routine - reflect on the day, update task status, identify tomorrow's priority. Use at the end of your day.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Daily Review Skill

Guides you through an evening reflection to close out your day and prepare for tomorrow.

## Usage

Invoke with `/daily-review` in the evening.

```
/daily-review
```

Or ask:
- "End my day"
- "Evening reflection"
- "Daily review"

## What This Skill Does

### 1. Opens Today's Note
- Finds today's note in `Daily Notes/YYYY/Mnn/`
- If it doesn't exist, prompts to run `/daily-setup` first

### 2. Reviews Task Status
- Counts completed vs incomplete tasks
- Identifies tasks that should be carried to tomorrow
- Highlights any blockers

### 3. Guides Reflection
Interactive prompts:
- "What went well today?"
- "What could be better?"
- "What did you learn?"
- "What's tomorrow's #1 priority?"

### 4. Prepares for Tomorrow
- Updates Reflection section with your answers
- Marks tomorrow's priority
- Suggests running `/push` to commit changes

## Evening Workflow

1. Run `/daily-review`
2. Answer reflection prompts
3. Review incomplete tasks
4. Set tomorrow's priority
5. Run `/push` to save changes

## Example Session

```
🌙 Daily Review for 2025-01-15

📊 Task Summary:
- Completed: 6/8 tasks (75%)
- Remaining: 2 tasks

⏳ Incomplete Tasks:
- [ ] Review PR #123
- [ ] Update documentation

💭 Let's reflect on today...

What went well today?
> [User input]

What could be better?
> [User input]

What did you learn?
> [User input]

🎯 What's your #1 priority for tomorrow?
> [User input]

✅ Reflection saved! Don't forget to /push your changes.
```

## Reflection Questions

The skill asks these questions to help you process the day:

1. **What Went Well?**
   - Celebrate small wins
   - Recognize progress
   - Build positive momentum

2. **What Could Be Better?**
   - Identify friction points
   - Note process improvements
   - Learn from challenges

3. **What Did I Learn?**
   - Capture insights
   - Document new knowledge
   - Connect to existing notes

4. **Tomorrow's Priority**
   - Single most important task
   - Clear next action
   - Sets morning intention

## Edge Cases

### Late Night (after midnight)
If running after midnight but before 4 AM, reviews the previous calendar day.

### No Tasks Completed
Encourages reflection on blockers and what got in the way.

### All Tasks Completed
Celebrates the achievement and asks what made it possible.

## Integration

Works with:
- `/daily-setup` - Morning companion skill
- `/weekly` - Weekly reviews aggregate daily reflections
- `/push` - Commit after review
