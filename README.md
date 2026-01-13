# Obsidian Personal PKM

A minimal personal knowledge management system designed to work seamlessly with [Claude Code](https://claude.ai/code) and [TaskNotes](https://github.com/callumalpass/tasknotes) for advanced task management.

## Features

- **Task Management** - Individual task files with YAML metadata, referenced via wikilinks
- **Daily Notes** - Structured daily planning with automatic task carryover
- **Morning/Evening Workflow** - Separate skills for morning setup and evening review
- **Blocker Detection** - Weekly reviews identify stuck tasks (3+ days incomplete)
- **Organized Structure** - Notes organized by `YYYY/Mnn/` for scalability
- **Git Integration** - Version control with smart commit messages
- **Note Organization** - Agent for vault maintenance and hygiene

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/leonardocouy/obsidian-personal-pkm.git
cd obsidian-personal-pkm
```

### 2. Open in Obsidian

Open the folder as an Obsidian vault.

### 3. Install Required Plugins

- **Periodic Notes** - For daily/weekly note structure
- **TaskNotes** - For task file management (each task = individual file)

### 4. Personalize

Copy `CLAUDE.local.md.template` to `CLAUDE.local.md` and customize with your preferences.

### 5. Start Using

```bash
# In Claude Code

# Task Management
/task-create "Task Name"  # Create a new task file
/task-done "Task Name"    # Mark task as completed

# Daily Workflow
/daily-setup    # Morning: create note, pull yesterday's tasks
/daily-review   # Evening: reflect, prepare tomorrow
/weekly         # Weekly review with blocker detection

# Utilities
/push           # Commit changes
/onboard        # Load vault context
```

## Structure

```
.
├── 00_Inbox/
│   └── Tasks/              # TaskNotes task files
│       ├── Review PR 123.md
│       └── Update docs.md
├── 20_Daily Notes/
│   └── YYYY/
│       └── Mnn/
│           ├── YYYY-MM-DD.md    # Daily notes
│           └── YYYY-Www.md      # Weekly reviews
├── Templates/
│   ├── Daily Template.md   # Daily note structure
│   └── Task Template.md    # Task file structure
├── Archives/               # Old/completed notes
├── .claude/
│   ├── skills/             # Automation skills
│   ├── commands/           # Quick commands
│   └── agents/             # Specialized AI agents
├── CLAUDE.md               # AI context and instructions
└── README.md               # This file
```

## Task Management

Tasks are stored as **individual markdown files** in `00_Inbox/Tasks/` and referenced via **wikilinks** in daily notes.

### Task File Format

```yaml
---
tags:
  - task
status: open              # open, in-progress, done
priority: medium          # low, medium, high
due: 2026-01-20           # optional deadline
scheduled: 2026-01-15     # when to work on it
projects: []              # optional project links
---

# Task Name

Task description and notes.
```

### Task References in Daily Notes

```markdown
## Tasks

### Must Do
- [ ] [[Review PR 123]]
- [ ] [[Fix production bug]]

### Work
- [ ] [[Update documentation]]
- [x] [[Write tests]] ✅ 2026-01-13
```

### Why Task Files?

- **Backlinks** - See all daily notes mentioning a task
- **Rich Metadata** - Priority, due dates, projects in YAML
- **TaskNotes Integration** - Inline widgets, views, filtering
- **Portability** - Plain markdown, no vendor lock-in

## Commands

| Command | Description |
|---------|-------------|
| `/task-create` | Create new task file with YAML and add to daily note |
| `/task-done` | Mark task complete, update daily note and task file |

### `/task-create`

Creates a new task file and adds a wikilink to today's daily note.

```bash
/task-create "Review PR 123"              # Basic task
/task-create "Fix bug" --priority high    # With priority
/task-create "Deploy" --due 2026-01-20    # With due date
/task-create                              # Interactive mode
```

### `/task-done`

Marks a task as completed in both the daily note and task file.

```bash
/task-done "Review PR 123"   # Complete specific task
/task-done                   # Interactive: select from open tasks
```

## Skills

| Skill | Description |
|-------|-------------|
| `/daily-setup` | Morning: create note, pull incomplete tasks (wikilinks), auto-reschedule overdue |
| `/daily-review` | Evening: reflect on day, add completion timestamps, update task file status |
| `/weekly` | Weekly review with blocker detection (tasks 3+ days stuck) |
| `/push` | Stage, commit, and push all changes with smart messages |
| `/onboard` | Load vault context at start of session |

### `/daily-setup`

Morning routine that:
- Creates today's note in `20_Daily Notes/YYYY/Mnn/`
- Reads yesterday's note for incomplete task wikilinks
- Reads task files to check scheduled dates
- Auto-reschedules overdue tasks (updates `scheduled` in YAML)
- Shows yesterday's summary

```bash
/daily-setup  # Start your morning
```

### `/daily-review`

Evening routine that:
- Reviews task completion from today's note
- Adds completion timestamps: `- [x] [[Task]] ✅ 2026-01-13`
- Updates task file status: `status: open` → `status: done`
- Guides reflection with prompts
- Sets tomorrow's priority

```bash
/daily-review  # End your day
```

### `/weekly`

Weekly review with blocker detection:
- Analyzes past 7 days of daily notes
- Detects blockers - task wikilinks appearing 3+ days without completion
- Reads task files for priority/due date context
- Calculates completion rate
- Creates weekly review note

```bash
/weekly  # Sunday review
```

**Blocker Detection:**
```markdown
## Blockers (3+ days without completion)

| Task | Days Stuck | Priority | Due |
|------|------------|----------|-----|
| [[Review PR 123]] | 4 days | high | 2026-01-15 |
| [[Update docs]] | 3 days | medium | - |
```

### `/push`

Smart Git workflow:
- Stages all changes
- Creates meaningful commit messages
- Pulls and pushes to remote
- Never force pushes

```bash
/push                        # Auto-generate commit message
/push "Weekly review done"   # Custom message
```

### `/onboard`

Loads vault context:
- Reads CLAUDE.md for conventions
- Scans recent daily notes
- Lists inbox items
- Understands current state

```bash
/onboard           # Full context
/onboard 00_Inbox  # Specific folder
```

## Agents

### note-organizer

Specialized agent for vault maintenance:
- Process Inbox items
- Fix broken wiki-links
- Archive old notes
- Suggest connections between notes

**Usage**: Ask Claude to "organize my notes" or "process my inbox"

## Workflows

### Morning Routine

1. `/daily-setup` - Create note with yesterday's context and tasks
2. Review tasks to continue (auto-rescheduled if overdue)
3. Set your ONE focus
4. Add new tasks with `/task-create`
5. `/push` - Commit changes

### During the Day

- Create tasks with `/task-create "New task"`
- Complete tasks with `/task-done "Task name"`
- Update daily note as needed

### Evening Routine

1. `/daily-review` - Reflect on day
2. Answer reflection prompts
3. Review task completion (timestamps added automatically)
4. Set tomorrow's priority
5. `/push` - Commit changes

### Weekly Review (Sunday)

1. `/weekly` - Run review with blocker detection
2. Celebrate wins
3. Address blockers (break down, delegate, or drop)
4. Plan next week
5. Process `00_Inbox/`
6. `/push` - Commit changes

## Customization

### Personal Overrides

Create `CLAUDE.local.md` (gitignored) for personal settings:

```markdown
## Personal Info
- Name: Your Name
- Timezone: America/Sao_Paulo

## Preferences
- Morning Routine: 7:00 AM
- Weekly Review: Sunday
```

### Custom Template

Edit templates in `Templates/` folder:
- `Daily Template.md` - Daily note structure
- `Task Template.md` - Task file structure

### Add Custom Skills

Create new skills in `.claude/skills/your-skill/SKILL.md`:

```yaml
---
name: your-skill
description: What it does
allowed-tools: Read, Write, Edit
user-invocable: true
---

# Skill Instructions

[Your skill documentation]
```

## Git Workflow

The vault is designed for Git version control:

```bash
# Initial setup (already done if you cloned)
git init
git remote add origin YOUR_REPO_URL

# Daily usage via /push skill
/push  # Handles add, commit, push
```

### Recommended .gitignore

Already configured to ignore:
- `CLAUDE.local.md` - Personal overrides
- `.obsidian/workspace*` - Obsidian workspace
- `.obsidian/cache` - Obsidian cache
- `.trash/` - Obsidian trash
- `.DS_Store` - macOS files

## Requirements

- [Obsidian](https://obsidian.md/) - Note-taking app
- [Periodic Notes](https://github.com/liamcain/obsidian-periodic-notes) - Obsidian plugin for daily/weekly notes
- [TaskNotes](https://github.com/callumalpass/tasknotes) - Obsidian plugin for task management
- [Claude Code](https://claude.ai/code) - AI coding assistant
- Git - Version control

## Credits

Inspired by:
- [obsidian-claude-pkm](https://github.com/ballred/obsidian-claude-pkm) by ballred
- [collaborator/pkm-framework](https://github.com/devkade/collaborator) by devkade

## License

MIT
