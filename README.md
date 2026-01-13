# Obsidian Personal PKM

A minimal personal knowledge management system designed to work seamlessly with [Claude Code](https://claude.ai/code).

## Features

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

### 3. Personalize

Copy `CLAUDE.local.md.template` to `CLAUDE.local.md` and customize with your preferences.

### 4. Start Using

```bash
# In Claude Code
/daily-setup    # Morning: create note, pull yesterday's tasks
/daily-review   # Evening: reflect, prepare tomorrow
/weekly         # Weekly review with blocker detection
/push           # Commit changes
/onboard        # Load vault context
```

## Structure

```
.
├── Daily Notes/
│   └── YYYY/
│       └── Mnn/
│           ├── YYYY-MM-DD.md    # Daily notes
│           └── YYYY-Www.md      # Weekly reviews
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
| `/daily-setup` | Morning: create note, pull incomplete tasks, show yesterday summary |
| `/daily-review` | Evening: reflect on day, set tomorrow's priority |
| `/weekly` | Weekly review with blocker detection (tasks 3+ days stuck) |
| `/push` | Stage, commit, and push all changes with smart messages |
| `/onboard` | Load vault context at start of session |

### `/daily-setup`

Morning routine that:
- Creates today's note in `Daily Notes/YYYY/Mnn/`
- Reads yesterday's note
- Pulls incomplete tasks automatically
- Shows yesterday's summary

```bash
/daily-setup  # Start your morning
```

**Daily Note Template includes:**
- **Yesterday Summary** - Auto-populated from yesterday
- **Tasks to Continue** - Incomplete tasks pulled automatically
- **Focus** - The ONE thing for the day
- **Tasks** - Organized by priority (Must Do, Work, Personal)
- **Ideas & Thoughts** - Capture section
- **Notes from Today** - General notes
- **Reflection** - End of day review
- **Related** - Links to adjacent days

### `/daily-review`

Evening routine that:
- Opens today's note
- Guides reflection with prompts
- Helps set tomorrow's priority

```bash
/daily-review  # End your day
```

**Reflection prompts:**
- What went well today?
- What could be better?
- What did I learn?
- What's tomorrow's #1 priority?

### `/weekly`

Weekly review with blocker detection:
- Analyzes past 7 days of daily notes
- Calculates task completion rate
- **Detects blockers** - Tasks appearing 3+ days without completion
- Creates weekly review note
- Plans next week

```bash
/weekly  # Sunday review
```

**Blocker Detection:**
```markdown
## Blockers (3+ days without completion)
- [ ] Review PR #123 — 4 days consecutive
- [ ] Update documentation — 3 days consecutive
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

1. `/daily-setup` - Create note with yesterday's context
2. Review tasks to continue
3. Set your ONE focus
4. Add new tasks
5. `/push` - Commit changes

### During the Day

- Quick capture ideas in `Inbox/`
- Update daily note as needed
- Mark tasks complete

### Evening Routine

1. `/daily-review` - Reflect on day
2. Answer reflection prompts
3. Set tomorrow's priority
4. `/push` - Commit changes

### Weekly Review (Sunday)

1. `/weekly` - Run review with blocker detection
2. Celebrate wins
3. Address blockers
4. Plan next week
5. Process `Inbox/`
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
- [Periodic Notes](https://github.com/liamcain/obsidian-periodic-notes) - Obsidian plugin for daily/weekly/monthly notes
- [Claude Code](https://claude.ai/code) - AI coding assistant
- Git - Version control

## Credits

Inspired by:
- [obsidian-claude-pkm](https://github.com/ballred/obsidian-claude-pkm) by ballred
- [collaborator/pkm-framework](https://github.com/devkade/collaborator) by devkade

## License

MIT
