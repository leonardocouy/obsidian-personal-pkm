---
name: onboard
description: Load CLAUDE.md context files from vault for comprehensive understanding. Discovers recent notes, vault structure, and current state. Use at start of session or when Claude needs full vault context.
allowed-tools: Read, Glob, Grep
user-invocable: true
---

# Onboard Skill

Loads context from your personal vault to provide comprehensive understanding for intelligent assistance.

## Usage

Invoke with `/onboard` or ask Claude to learn about your vault.

### Full Context Load
```
/onboard
```

### Specific Folder Context
```
/onboard Daily Notes
```

## What This Skill Does

1. **Discovers Context Files**
   - Reads CLAUDE.md for vault conventions
   - Scans vault structure
   - Identifies key folders

2. **Loads Recent Activity**
   - Recent daily notes
   - Inbox items pending processing
   - Recently modified files

3. **Builds Understanding**
   - Vault structure and organization
   - Workflow preferences
   - Current state of notes

## Context Loading

### What Gets Loaded
```
00-personal/
├── CLAUDE.md              # [1] Primary context - loaded first
├── Daily Notes/           # [2] Recent notes scanned
├── Inbox/                 # [3] Pending items listed
├── Templates/             # [4] Available templates
└── Archives/              # [5] Archived notes (not loaded by default)
```

### Recent Activity
Automatically considers:
- Last 7 days of daily notes
- All Inbox items
- Recently modified files

## Smart Context Loading

### Selective Loading
For focused assistance:
```
/onboard Daily Notes      # Only daily notes context
/onboard Inbox            # Only inbox items
```

## Use Cases

### Starting a Session
```
/onboard
"Help me plan my day"
```

### Processing Inbox
```
/onboard Inbox
"Help me process these items"
```

### Weekly Review
```
/onboard
"Analyze my week"
```

## Best Practices

### Keep Context Updated
- Review CLAUDE.md occasionally
- Update after workflow changes
- Remove outdated information

### Be Specific
- Clear folder descriptions
- Specific preferences
- Concrete examples

## Privacy & Security

### Never Include in CLAUDE.md
- Passwords or credentials
- Personal identification numbers
- Financial account details
- Private API keys

### Safe Context Examples
- "I use daily notes for task planning"
- "Inbox is for quick captures"
- "I prefer morning work sessions"

## Integration

Works with:
- All other skills (provides context)
- `/daily` - Better daily planning with context
- `/weekly` - Informed weekly reviews
