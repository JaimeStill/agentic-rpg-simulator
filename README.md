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
- **Character profiles** with personalities, goals, and decision frameworks
- **Initial world state** based on your scenario
- **Adventure-specific prompts** for simulation, summarization, and narration

### 3. Event Processing
Each event follows a strict protocol:
1. Load compressed state from previous event
2. Describe the situation (300 tokens)
3. Characters take actions (150 tokens each)
4. Resolve mechanics (combat, social, exploration)
5. Update character and world states
6. Save state for next event

### 4. Token Economy
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
└── [adventures]/       # Generated adventures
    ├── scenario.yml
    ├── characters/
    ├── events/
    └── prompts/
```

## Quick Start

1. **Generate a new adventure**:
   ```
   Prompt: prompts/generate-adventure.md
   ```
   Choose from existing scenarios or create custom.

2. **Run the adventure**:
   ```
   Prompt: [adventure-name]/prompts/simulate-adventure.md
   ```

3. **Review progress**:
   ```
   Prompt: [adventure-name]/prompts/summarize-adventure.md
   ```

## Key Features

### State Compression
All persistent data is compressed into YAML state packages, enabling unlimited adventure length within fixed context windows.

### Character Evolution
Characters adapt based on experiences:
- Personality shifts from major events
- Relationship changes through interactions
- Tactical evolution from successes/failures

### Flexible Scenarios
From 5-event short stories to 20-event campaigns, across any genre:
- Fantasy quests
- Sci-fi diplomacy
- Mystery investigations
- Post-apocalyptic survival
- Superhero team-ups
- Cyberpunk heists

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

## Advanced Usage

### Continue From Any Point
Load a specific event state to branch the narrative:
```
State: [adventure]/events/event-5-state.yml
Prompt: [adventure]/prompts/simulate-adventure.md
```

### Narrative Export
Transform compressed events into rich prose:
```
Prompt: [adventure]/prompts/narrate-adventure.md
```

## Contributing

Scenarios that produce compelling adventures can be saved to `scenarios/` for others to enjoy. Follow the existing format and include descriptive metadata.

## License

This project is designed for creative storytelling and narrative experimentation within AI language models.