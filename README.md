# Agentic RPG Simulator

A lightweight, token-efficient RPG adventure engine that processes narrative events within strict context boundaries. Each adventure unfolds through a series of discrete events, with character decisions and world state compressed between scenes.

## Overview

The Agentic RPG Simulator creates dynamic, multi-character adventures where:
- Each event is processed independently with compressed state handoffs
- Characters make autonomous decisions based on evolving profiles
- Token budgets enforce concise, impactful storytelling
- Adventures can span any genre from fantasy to cyberpunk

## How It Works

### 1. Choose or Create a Scenario
Select from pre-built scenarios or create your own:
```
Prompt: prompts/generate-adventure.md
```

Available scenarios include cyberpunk heists, first contact crises, murder mysteries, and more. Each defines the theme, party size, and narrative arc.

### 2. Adventure Generation  
The system creates:
- **Character profiles** with deep cultural backgrounds and authentic personalities
- **Character subagents** for authentic behavioral responses during events
- **Initial world state** based on your scenario
- **Adventure-specific prompts** for automated simulation, summarization, and narration

### 3. Automated Event Processing
Each event runs through a complete automated workflow:
1. **Character Subagent Setup**: Convert YAML profiles to runtime subagents
2. **Event State Detection**: Determine current adventure progress and next event
3. **Character Actions**: Invoke character subagents for authentic responses
4. **Mechanic Resolution**: Process actions through game mechanics
5. **Character Evolution**: Extract growth and update persistent profiles  
6. **State Persistence**: Save compressed state and detailed transcripts
7. **Subagent Refresh**: Update runtime subagents with character evolution

### 4. Character Development System
Characters grow authentically throughout adventures:
- **Subagent-Driven Behavior**: Each character responds through dedicated subagent context
- **Persistent Evolution**: Character growth tracked in database-ready YAML profiles
- **Session Continuity**: Runtime subagents maintain character development between events
- **Bidirectional Sync**: Evolution flows between persistent profiles and active subagents

### 5. Token Economy
Every action has a token cost:
- Simple actions: 50 tokens
- Complex actions: 100 tokens  
- Signature moves: 150 tokens

This forces meaningful choices and prevents context overflow.

## Project Structure

```
agentic-rpg-simulator/
├── CLAUDE.md           # Core engine rules (loaded by default)
├── prompts/            # Command prompts
│   ├── generate-adventure.md
│   └── generate-scenario.md
├── scenarios/          # Pre-built adventure configurations
├── schemas/            # Data structure definitions
└── adventures/         # All generated adventures
    └── [adventure-name]/
        ├── scenario.yml
        ├── characters/
        ├── events/
        ├── logs/      # Event transcripts (optional)
        └── prompts/
```

## Quick Start

1. **Generate a new adventure**:
   ```
   Prompt: prompts/generate-adventure.md
   ```
   Choose from existing scenarios or create custom.

2. **Run the adventure** (fully automated):
   ```
   Prompt: adventures/[adventure-name]/prompts/simulate-adventure.md
   ```
   This automatically processes the next event with character subagent participation, evolution tracking, and state persistence.

3. **Review progress**:
   ```
   Prompt: adventures/[adventure-name]/prompts/summarize-adventure.md
   ```

4. **Read event transcripts** (if logging enabled):
   ```
   File: adventures/[adventure-name]/logs/event-[X].yaml
   ```

## Key Features

### Authentic Character Behavior
Characters respond through dedicated subagent contexts with cultural authenticity:
- Deep character backgrounds with genuine motivations
- Subagent-driven responses that maintain consistent personality
- Real-time character evolution tracking and persistence
- Bidirectional synchronization between profiles and runtime behavior

### State Compression & Persistence
Hybrid data management for scalability and portability:
- YAML profiles for database-ready persistent character data
- Runtime subagents for authentic behavioral responses during events
- Compressed state packages enabling unlimited adventure length
- Automatic state synchronization and recovery systems

### Character Evolution
Characters grow authentically based on experiences:
- Personality development from major events and relationship changes
- Goal evolution and tactical adaptation from successes/failures
- Cultural and background-informed character responses
- Persistent growth that carries forward throughout adventures

### Flexible Scenarios
From 5-event short stories to 20-event campaigns, across any genre:
- Fantasy quests
- Sci-fi diplomacy
- Mystery investigations
- Post-apocalyptic survival
- Superhero team-ups
- Cyberpunk heists

### Event Logging
Optional detailed event transcripts capture the full narrative experience:
- Complete character actions and dialogue
- Mechanic resolutions and outcomes  
- Rich scene descriptions and atmosphere
- Configurable detail levels and formats

### Mechanic Adaptability
Combat, social, and exploration systems that learn from player patterns and adjust difficulty dynamically.

## Design Philosophy

**Single Event Scope**: Each scene stands alone while building on compressed history
**Token Economy**: Every word counts, encouraging impactful storytelling
**Emergent Narrative**: Characters drive the story through their decisions
**Clean Handoffs**: Complete state preservation between events

## Creating Custom Scenarios

Use the scenario generator:
```
Prompt: prompts/generate-scenario.md
```

Or copy an existing scenario from `scenarios/` and modify:
- Adjust party size (1-6 characters)
- Set event count (5-20)
- Define theme and initial situation
- Configure complexity distribution
- Enable event logging with `store_event_logs: true`

## Advanced Usage

### Continue From Any Point
Load a specific event state to branch the narrative:
```
State: adventures/[adventure]/events/event-5-state.yml
Prompt: adventures/[adventure]/prompts/simulate-adventure.md
```

### Narrative Export
Transform compressed events into rich prose:
```
Prompt: adventures/[adventure]/prompts/narrate-adventure.md
```

## Contributing

Scenarios that produce compelling adventures can be saved to `scenarios/` for others to enjoy. Follow the existing format and include descriptive metadata.

## License

This project is designed for creative storytelling and narrative experimentation within AI language models.