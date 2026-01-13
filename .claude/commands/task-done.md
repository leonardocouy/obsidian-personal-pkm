# Task Done Command

Marks a task as completed - updates the daily note with completion timestamp and changes the task file status to done.

## Usage

```
/task-done "Task Name"
/task-done
```

If no task name is provided, lists open tasks from today's daily note for selection.

## Workflow

### 1. Get Task to Complete

**If task name provided:**
Use the provided name directly.

**If no task name (interactive mode):**
1. Read today's daily note: `20_Daily Notes/YYYY/Mnn/YYYY-MM-DD.md`
2. Find all incomplete task wikilinks: `- [ ] [[Task Name]]`
3. Present list for selection:

```
📋 Open tasks in today's note:

1. [[Review PR 123]]
2. [[Update documentation]]
3. [[Fix bug in auth]]

Which task did you complete? (number or name)
>
```

### 2. Update Daily Note

Find the task in today's daily note and update:

**Before:**
```markdown
- [ ] [[Task Name]]
```

**After:**
```markdown
- [x] [[Task Name]] ✅ 2026-01-13
```

### 3. Update Task File

Find task file: `00_Inbox/Tasks/{Task Name}.md`

Update YAML frontmatter:

**Before:**
```yaml
status: open
```

**After:**
```yaml
status: done
```

### 4. Confirm Completion

```
✅ Task completed!

📋 [[Task Name]] ✅ 2026-01-13

Updated:
- 20_Daily Notes/2026/M01/2026-01-13.md (marked complete)
- 00_Inbox/Tasks/Task Name.md (status: done)

🎉 Keep it up!
```

## Examples

### Direct completion
```
/task-done "Review PR 123"

✅ Task completed!
📋 [[Review PR 123]] ✅ 2026-01-13
```

### Interactive mode
```
/task-done

📋 Open tasks in today's note:

1. [[Review PR 123]]
2. [[Update documentation]]
3. [[Fix bug in auth]]

Which task did you complete? (number or name)
> 1

✅ Task completed!
📋 [[Review PR 123]] ✅ 2026-01-13
```

### Multiple completions
```
/task-done "Review PR 123"
/task-done "Update documentation"

# Or in interactive mode, can complete multiple
```

## Edge Cases

### Task Not in Daily Note
If task wikilink not found in today's daily note:
```
⚠️ Task [[{Task Name}]] not found in today's note.

Options:
1. Add completed task to today's note
2. Search in other recent notes
3. Cancel

What would you like to do?
```

### Task File Not Found
If task file doesn't exist in `00_Inbox/Tasks/`:
```
⚠️ Task file not found: 00_Inbox/Tasks/{Task Name}.md

I'll still mark it complete in the daily note.
Note: Task file status won't be updated.

Continue? (yes/no)
```

### Task Already Completed
If task already has `[x]`:
```
ℹ️ Task [[{Task Name}]] is already marked complete.
```

### No Open Tasks
If no incomplete tasks in today's note:
```
🎉 All tasks in today's note are already completed!
Great job!
```

### Multiple Occurrences
If task appears multiple times in daily note, update all occurrences.

## Output Format

The completion timestamp follows this format:
```
- [x] [[Task Name]] ✅ YYYY-MM-DD
```

Where:
- `[x]` = completed checkbox
- `[[Task Name]]` = wikilink to task file
- `✅` = visual completion indicator
- `YYYY-MM-DD` = completion date

## Integration

Works with:
- `/task-create` - Create new tasks
- `/daily-setup` - Morning routine shows tasks to continue
- `/daily-review` - Evening routine processes completions
- `/weekly` - Weekly review counts completions
