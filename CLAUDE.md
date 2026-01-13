# Personal PKM Vault - Claude Instructions

This is a personal knowledge management vault designed to work seamlessly with Claude Code.

## Vault Structure

```
00-personal/
├── Daily Notes/    # Daily notes (YYYY-MM-DD.md)
├── Templates/      # Reusable templates
├── Inbox/          # Quick captures to process later
├── Archives/       # Old/completed notes
└── .claude/        # Claude Code integration
    ├── skills/     # /daily, /weekly, /push, /onboard
    └── agents/     # note-organizer
```

## Available Skills

| Skill | Description | Usage |
|-------|-------------|-------|
| `/daily` | Create/manage daily notes | Morning planning, evening reflection |
| `/weekly` | Weekly review and planning | Sunday reviews, week planning |
| `/push` | Commit and push to Git | After making changes |
| `/onboard` | Load vault context | Start of session |

## Available Agents

| Agent | Description |
|-------|-------------|
| `note-organizer` | Process inbox, organize notes, maintain vault hygiene |

## Conventions

### File Naming
- Daily notes: `YYYY-MM-DD.md` (e.g., `2024-01-15.md`)
- Templates: Descriptive name with "Template" suffix

### Folders
- `Daily Notes/` - One file per day, created via `/daily`
- `Inbox/` - Quick captures, processed regularly
- `Templates/` - Reusable note templates
- `Archives/` - Old notes, completed items

### Tags
- `#daily-note` - Daily notes
- `#inbox` - Items to process
- `#archived` - Archived notes

## Workflow

### Morning
1. `/daily` - Create today's note
2. Set focus and tasks
3. `/push` - Commit changes

### During Day
- Capture ideas in Inbox/
- Update daily note as needed

### Evening
1. Open daily note
2. Complete reflection section
3. `/push` - Commit changes

### Weekly
1. `/weekly` - Run weekly review
2. Process Inbox/
3. Archive old notes
4. `/push` - Commit changes

## Communication

- **Language**: Portuguese (pt-BR) for interaction
- **Content**: English for note content and documentation
- **Style**: Direct, concise responses

## Notes for Claude

- Always check if daily note exists before creating
- Use template from `Templates/Daily Template.md`
- Respect user's folder structure
- Ask before moving or deleting files
- Commit changes with meaningful messages
