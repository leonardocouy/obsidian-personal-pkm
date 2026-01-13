# Obsidian Personal PKM

A minimal personal knowledge management system designed to work seamlessly with [Claude Code](https://claude.ai/code).

## Features

- **Daily Notes** - Structured daily planning with focus, tasks, and reflection
- **Inbox Processing** - GTD-style capture and organize workflow
- **Git Integration** - Version control with smart commit messages
- **Claude Code Skills** - AI-powered automation for common workflows
- **Note Organization** - Agent for vault maintenance and hygiene

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/obsidian-personal-pkm.git
cd obsidian-personal-pkm
```

### 2. Open in Obsidian

Open the folder as an Obsidian vault.

### 3. Personalize

Copy `CLAUDE.local.md.template` to `CLAUDE.local.md` and customize with your preferences.

### 4. Start Using

```bash
# In Claude Code
/daily    # Create today's note
/weekly   # Run weekly review
/push     # Commit changes
/onboard  # Load vault context
```

## Structure

```
.
├── Daily Notes/    # One note per day (YYYY-MM-DD.md)
├── Templates/      # Reusable note templates
├── Inbox/          # Quick captures to process
├── Archives/       # Old/completed notes
├── .claude/        # Claude Code configuration
│   ├── skills/     # Automation skills
│   └── agents/     # Specialized AI agents
├── CLAUDE.md       # AI context and instructions
└── README.md       # This file
```

## Skills

| Skill | Description |
|-------|-------------|
| `/daily` | Create or open today's daily note with structured template |
| `/weekly` | Run weekly review: analyze past week, plan next week |
| `/push` | Stage, commit, and push all changes with smart messages |
| `/onboard` | Load vault context at start of session |

### `/daily`

Creates a daily note with:
- **Focus** - The ONE thing for the day
- **Tasks** - Organized by priority (Must Do, Work, Personal)
- **Ideas & Thoughts** - Capture section
- **Notes from Today** - Meetings and important info
- **Reflection** - End of day review
- **Related** - Links to adjacent days

```bash
/daily                    # Create/open today's note
/daily "morning routine"  # With specific context
```

### `/weekly`

Facilitates weekly review:
- Reviews past 7 days of daily notes
- Identifies wins and challenges
- Plans next week's priorities
- Suggests archiving old notes

```bash
/weekly  # Run full weekly review
```

### `/push`

Smart Git workflow:
- Stages all changes
- Creates meaningful commit messages based on changed files
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
/onboard Inbox     # Specific folder
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

1. `/daily` - Create today's note
2. Set your ONE focus
3. List must-do tasks
4. `/push` - Commit changes

### During the Day

- Quick capture ideas in `Inbox/`
- Update daily note as needed
- Mark tasks complete

### Evening Routine

1. Open daily note
2. Complete reflection section
3. Identify tomorrow's priority
4. `/push` - Commit changes

### Weekly Review (Sunday)

1. `/weekly` - Run guided review
2. Celebrate wins
3. Learn from challenges
4. Plan next week
5. Process `Inbox/`
6. Archive old notes
7. `/push` - Commit changes

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

Edit `Templates/Daily Template.md` to match your preferred structure.

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
# Initial setup
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
- [Claude Code](https://claude.ai/code) - AI coding assistant
- Git - Version control

## Credits

Inspired by [obsidian-claude-pkm](https://github.com/ballred/obsidian-claude-pkm) by ballred.

## License

MIT
