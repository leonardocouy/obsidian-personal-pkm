# Personal PKM Vault - Claude Instructions

This is a personal knowledge management vault designed to work seamlessly with Claude Code.

## Vault Structure

```
.
├── Daily Notes/           # Organized by year/month
│   └── YYYY/
│       └── Mnn/
│           ├── YYYY-MM-DD.md    # Daily notes
│           └── YYYY-Www.md      # Weekly reviews
├── Templates/             # Reusable templates
├── Inbox/                 # Quick captures to process later
├── Archives/              # Old/completed notes
└── .claude/               # Claude Code integration
    ├── skills/            # /daily-setup, /daily-review, /weekly, /push, /onboard
    └── agents/            # note-organizer
```

## Available Skills

| Skill | Description | Usage |
|-------|-------------|-------|
| `/daily-setup` | Morning routine - create note, pull yesterday's tasks | Start of day |
| `/daily-review` | Evening routine - reflect, prepare tomorrow | End of day |
| `/weekly` | Weekly review with blocker detection | Sunday reviews |
| `/push` | Commit and push to Git | After making changes |
| `/onboard` | Load vault context | Start of session |

## Available Agents

| Agent | Description |
|-------|-------------|
| `note-organizer` | Process inbox, organize notes, maintain vault hygiene |

## Conventions

### File Naming
- Daily notes: `YYYY-MM-DD.md` in `Daily Notes/YYYY/Mnn/`
- Weekly reviews: `YYYY-Www.md` in same folder as daily notes
- Templates: Descriptive name with "Template" suffix

### Folders
- `Daily Notes/YYYY/Mnn/` - Organized by year and month
- `Inbox/` - Quick captures, processed regularly
- `Templates/` - Reusable note templates
- `Archives/` - Old notes, completed items

### Tags
- `#daily-note` - Daily notes
- `#inbox` - Items to process
- `#archived` - Archived notes

## Workflow

### Morning
1. `/daily-setup` - Create today's note with yesterday's context
2. Review tasks to continue
3. Set ONE focus
4. `/push` - Commit changes

### During Day
- Capture ideas in Inbox/
- Update daily note as needed

### Evening
1. `/daily-review` - Reflect on day
2. Complete reflection prompts
3. Set tomorrow's priority
4. `/push` - Commit changes

### Weekly
1. `/weekly` - Run weekly review
2. Review blockers (tasks 3+ days incomplete)
3. Plan next week
4. Process Inbox/
5. `/push` - Commit changes

## Communication

- **Language**: Portuguese (pt-BR) for interaction
- **Content**: English for note content and documentation
- **Style**: Direct, concise responses

## Notes for Claude

- Daily notes go in `Daily Notes/YYYY/Mnn/YYYY-MM-DD.md`
- Weekly reviews go in `Daily Notes/YYYY/Mnn/YYYY-Www.md`
- Always check if note exists before creating
- Use template from `Templates/Daily Template.md`
- `/daily-setup` pulls incomplete tasks from yesterday automatically
- `/weekly` detects blockers (tasks appearing 3+ days without completion)
- Respect user's folder structure
- Ask before moving or deleting files
- Commit changes with meaningful messages
