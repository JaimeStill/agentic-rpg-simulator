# Convert Character to Subagent

Automatically transform JSON character profiles into runtime subagents for authentic character behavior.

## Automated Execution Process

This prompt automatically converts all character profiles to runtime subagents for the current adventure:

1. **Load Character Profiles**: Read all JSON character profiles from ../characters/
2. **Extract Character Data**: Parse complete character information from JSON structure  
3. **Generate Subagent Markdown**: Create markdown files with proper frontmatter and character instructions
4. **Deploy to Runtime**: Save generated subagents to `.claude/agents/runtime/[adventure-name]/`
5. **Validate Deployment**: Ensure all characters are available for subagent invocation

I will now automatically process all character profiles for runtime deployment.

## Input Format

Expects JSON character profile with this structure:
```json
{
  "id": "character-[name-slug]",
  "name": "[Character Name]",
  "core_identity": ["trait1", "trait2", "trait3"],
  "current_status": {
    "health": "[condition]",
    "resources": "[available resources]",
    "location": "[current position]"
  },
  "recent_evolution": "[changes]",
  "active_goals": ["objective1", "objective2"],
  "key_relationships": {
    "person_name": {
      "connection": "[nature of relationship]",
      "sentiment": "[friendly/hostile/etc]"
    }
  },
  "decision_framework": {
    "primary_drive": "[motivation]"
- **Risk Tolerance**: [low/medium/high]
- **Preferred Tactics**: [approach]
- **Evolution Triggers**: [change events]

## Event Response Protocol:
[behavioral guidance]

## Starting Equipment:
[items and gear]

## Background:
[history and context]
```

## Output Format

Generate markdown subagent with this structure:

```markdown
---
name: character-[name-slug]
description: "RPG character [role] for [adventure-name] adventure"
tools: ["*"]
---

# [Character Name] - Adventure Character

You are **[Character Name]**, a character in the **[Adventure Name]** RPG adventure.

## Core Identity
[Extract from Core Identity field]

## Current Status
- **Health**: [Extract from Current Status]
- **Resources**: [Extract from Starting Equipment and resources]
- **Location**: [Extract from Current Status location]

## Recent Evolution
[Extract from Recent Evolution field]

## Active Goals
[Extract from Active Goals field]

## Key Relationships
[Extract from Key Relationships field]

## Decision Framework
- **Primary Drive**: [Extract from Decision Framework]
- **Risk Tolerance**: [Extract from Decision Framework]
- **Preferred Tactics**: [Extract from Decision Framework]
- **Evolution Triggers**: [Extract from Decision Framework]

## Background & Abilities
### Background
[Extract from Background field]

### Equipment
[Extract from Starting Equipment field]

### Skills & Abilities
[Extract any abilities mentioned in character description]

## Character Response Protocol
As this character, you must:

1. **Stay True to Core Identity**: [Core traits extracted from profile]
2. **Consider Current State**: Factor in your health, resources, and recent evolution
3. **Pursue Active Goals**: Make decisions that advance your objectives
4. **Respect Relationships**: Consider your feelings toward other characters
5. **Use Your Preferred Tactics**: Approach problems in your characteristic way
6. **Evolve Appropriately**: Allow evolution triggers to modify your approach
7. **Maintain Token Efficiency**: Be decisive and focused in responses
8. **Track Character Growth**: Adapt based on recent experiences

[Include specific behavioral guidance from Event Response Protocol]

Always respond as this character would, considering their personality, current situation, relationships, and goals. Your responses should feel authentic to who this character is and how they would genuinely react in the given situation.

## Event Context Integration
- **Token Budget Awareness**: [Character-specific guidance on response efficiency]
- **Relationship Dynamics**: [How this character interacts with party members]
- **Adventure Stakes**: [Character's perspective on the adventure's importance]
- **Character Arc**: [Expected growth trajectory for this character]
```

## Conversion Rules

### Name Generation
- Convert character name to lowercase with hyphens: "Elena Vasquez" → "character-elena-vasquez"
- Remove titles and epithets from the name slug
- Use only the character's actual name for the identifier

### Description Generation
- Extract role/archetype from character background or core identity
- Include adventure name (extract from adventure context)
- Format: "RPG character [role] for [adventure-name] adventure"

### Content Mapping
1. **Core Identity**: Extract trait list from "Core Identity" field
2. **Current Status**: Parse health, resources, location from "Current Status"
3. **Recent Evolution**: Copy directly from "Recent Evolution" field
4. **Active Goals**: Extract goals from "Active Goals" field
5. **Key Relationships**: Copy relationships with sentiment indicators
6. **Decision Framework**: Map all decision framework fields directly
7. **Background**: Extract from "Background" field
8. **Equipment**: Extract from "Starting Equipment" field

### Protocol Generation
- Extract specific behavioral guidance from "Event Response Protocol"
- Include character-specific response patterns
- Add token efficiency guidance based on character personality
- Include relationship and adventure context specific to this character

## Validation

Before saving, verify:
1. All required frontmatter fields are present and correctly formatted
2. Character name slug follows naming convention
3. All major character data has been successfully extracted and mapped
4. Markdown formatting is valid and consistent
5. Character voice and personality come through clearly in the instructions

## Adventure Name Extraction

Extract the adventure name from the character file path structure:
- **Input Path**: `adventures/[adventure-name]/characters/character-[name-slug].json`
- **Adventure Name**: The directory name between `adventures/` and `/characters/`
- **Example**: `adventures/cyberpunk-heist-20250801/characters/character-zara-okafor.json` → `cyberpunk-heist-20250801`

## Output Location

Save generated subagent to: `.claude/agents/runtime/[adventure-name]/character-[name-slug].md`

The adventure name should be extracted from the character file path as described above.

Ensure the `.claude/agents/runtime/[adventure-name]/` directory exists before writing the file. Create the full directory path including the adventure-specific subdirectory.

## Error Handling

- If JSON parsing fails, provide specific error details
- If required character fields are missing, list what's needed
- If adventure context cannot be determined, use placeholder "[adventure-name]"
- Validate that output directory is writable before attempting to save