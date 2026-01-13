---
name: daily-review
description: Evening routine - reflect on the day, mark completed tasks with timestamps, update task file status, identify tomorrow's priority. Use at the end of your day.
allowed-tools: Read, Write, Edit, Glob, Grep
user-invocable: true
---

# Daily Review Skill

Guides you through an evening reflection to close out your day and prepare for tomorrow. Integrates with TaskNotes plugin to update task status.

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
- Finds today's note in `20_Daily Notes/YYYY/Mnn/`
- If it doesn't exist, prompts to run `/daily-setup` first

### 2. Reviews Task Status
- Counts completed vs incomplete tasks (wikilink format)
- Identifies tasks that should be carried to tomorrow
- Highlights any blockers

### 3. Updates Task Completion
For completed tasks `- [x] [[Task Name]]`:
- Adds timestamp if missing: `- [x] [[Task Name]] ✅ YYYY-MM-DD`
- Updates task file (`00_Inbox/Tasks/{Task Name}.md`):
  - Changes `status: open` → `status: done`

### 4. Guides Reflection
Interactive prompts:
- "What went well today?"
- "What could be better?"
- "What did you learn?"
- "What's tomorrow's #1 priority?"

### 5. Prepares for Tomorrow
- Updates Reflection section with your answers
- Marks tomorrow's priority
- Suggests running `/push` to commit changes

## Task Format

Tasks use **wikilinks** to reference task files:
- Incomplete: `- [ ] [[Task Name]]`
- Completed: `- [x] [[Task Name]] ✅ 2026-01-13`

## Evening Workflow

1. Run `/daily-review`
2. Mark tasks as complete (or use `/task-done`)
3. Answer reflection prompts
4. Review incomplete tasks
5. Set tomorrow's priority
6. Run `/push` to save changes

## Example Session

```
🌙 Daily Review for 2026-01-15

📊 Task Summary:
- Completed: 6/8 tasks (75%)
- Remaining: 2 tasks

✅ Completed Tasks (timestamps added):
- [x] [[Review PR 123]] ✅ 2026-01-15
- [x] [[Write documentation]] ✅ 2026-01-15
- [x] [[Fix bug in auth]] ✅ 2026-01-15

⏳ Incomplete Tasks:
- [ ] [[Update API docs]]
- [ ] [[Deploy to staging]]

📝 Task files updated:
- 00_Inbox/Tasks/Review PR 123.md → status: done
- 00_Inbox/Tasks/Write documentation.md → status: done
- 00_Inbox/Tasks/Fix bug in auth.md → status: done

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

### Task File Not Found
If a completed task's file doesn't exist, still adds timestamp but skips file update.

## Integration

Works with:
- `/daily-setup` - Morning companion skill
- `/weekly` - Weekly reviews aggregate daily reflections
- `/task-create` - Create new task files
- `/task-done` - Quick task completion
- `/push` - Commit after review

## Requirements

- **TaskNotes plugin** - For task file management and inline widgets
- **Periodic Notes plugin** - For daily note structure
