# Runtime Character Subagents

This directory contains temporary character subagents organized by adventure for proper isolation and concurrent adventure support.

## Purpose

Character subagents in this directory are:
- **Generated from YAML profiles** in `adventures/[name]/characters/`
- **Organized by adventure** in `[adventure-name]/` subdirectories
- **Active during adventure sessions** for authentic character behavior
- **Automatically managed** by the adventure simulation system
- **Isolated per adventure** - preventing interference between concurrent adventures
- **Temporary** - can be cleaned up after adventure completion

## Directory and File Organization

Character subagents are organized as follows:
- **Directory Structure**: `[adventure-name]/character-[name-slug].md`
- **Adventure Isolation**: Each adventure has its own subdirectory
- **File Naming**: `character-[name-slug].md` (e.g., `character-elena-vasquez.md`)
- **Name Convention**: Slug is lowercase with hyphens, derived from character's actual name
- **ID Matching**: Matches the character ID used in persistent YAML profiles

## Lifecycle Management

### Session Start
1. Read character YAML profiles from adventure directory
2. Convert YAML profiles to markdown subagent format
3. Deploy subagents to this runtime directory
4. Characters become invokable by name during events

### Event Processing
1. Invoke character subagents directly for character actions
2. Subagents respond with authentic character behavior
3. Character evolution occurs within subagent context
4. State changes captured in subagent responses

### Event Conclusion
1. Extract character evolution from subagent responses
2. Update persistent YAML profiles with character changes
3. Regenerate subagents with evolved character state
4. Continue with updated character context

### Session End
1. Final character state captured in YAML profiles
2. Runtime subagents can be safely removed
3. Character evolution persists in adventure directory

## Directory Organization

```
.claude/agents/runtime/
├── README.md (this file)
├── [adventure-name-1]/
│   ├── character-[name1].md (runtime subagent)
│   ├── character-[name2].md (runtime subagent)
│   └── ...
├── [adventure-name-2]/
│   ├── character-[name3].md (runtime subagent)
│   ├── character-[name4].md (runtime subagent)
│   └── ...
└── ...
```

**Example Structure:**
```
.claude/agents/runtime/
├── README.md
├── cyberpunk-heist-20250801/
│   ├── character-zara-okafor.md
│   ├── character-marcus-torres.md
│   └── character-kai-chen.md
└── fantasy-quest-20250802/
    ├── character-elena-vasquez.md
    └── character-ayana-kone.md
```

## Integration Notes

- This directory is **project-specific** and takes priority over user-level agents
- Subagents have access to all tools (`tools: ["*"]`) for full character capabilities
- Character subagents are **isolated from system agents** in parent directories
- Runtime agents are **automatically managed** by adventure simulation prompts

## Cleanup Policy

Runtime subagents can be safely removed when:
- Adventure session is complete
- All character evolution has been captured in YAML profiles
- No active adventure simulation is in progress

**Adventure-Specific Cleanup:**
- Each adventure's runtime directory can be cleaned up independently
- Remove entire `[adventure-name]/` subdirectories when adventures are complete
- Concurrent adventures can maintain separate runtime state
- Cleanup does not affect other running adventures

The adventure simulation system will regenerate these subagents as needed from the persistent YAML character profiles.