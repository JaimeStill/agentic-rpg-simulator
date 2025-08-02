# Agentic RPG Simulator Architecture Guide

## Overview

The Agentic RPG Simulator is a sophisticated narrative generation system that processes RPG adventures through discrete events with strict token budgets. The architecture emphasizes autonomous character behavior, persistent state management, and emergent storytelling through intelligent resource allocation.

## Core Architectural Principles

### 1. Single Event Scope Processing
Each adventure event operates in complete isolation with compressed state handoffs, enabling unlimited adventure length without context overflow. Events are self-contained narrative units that build upon compressed historical data.

### 2. Token Economy Design
The system enforces strict token budgets to drive meaningful narrative decisions:
- **Max Event Tokens**: 2000 (hard limit per event)
- **Action Costs**: 50 (simple), 100 (complex), 150 (signature moves)
- **Mechanic Resolution**: 200 tokens per resolution
- **Event Setup**: 300 tokens for scene description

### 3. Autonomous Character Evolution
Characters evolve authentically through dedicated subagent interactions, with bidirectional synchronization between persistent profiles and runtime behavior contexts.

## System Architecture

### Event Processing Engine

The core engine follows a strict 7-step execution protocol defined in `CLAUDE.md`:

```
1. LOAD STATE → Parse previous event package
2. EVENT SETUP → Describe situation (300 tokens)
3. CHARACTER PHASE → Each character action (150 tokens)
4. MECHANIC PHASE → Resolve actions (200 tokens each)
5. EVOLUTION PHASE → Update character/world states
6. SAVE STATE → Generate next event package
7. HANDOFF → Output complete state for continuation
```

#### Token Budget Distribution
```yaml
Event Budget Allocation:
  setup: 300 tokens (scene description, stakes)
  character_actions: 150 × number_of_agents
  mechanic_resolutions: 200 × number_of_mechanics
  state_update: 200 tokens (evolution + world changes)
  event_summary: 150 tokens (action log entry)
```

#### Complexity Management
Events are classified by complexity affecting token allocation:
- **Low Complexity (1000-1200 tokens)**: Simple encounters, character moments
- **Medium Complexity (1400-1600 tokens)**: Combat, social negotiations, environmental challenges
- **High Complexity (1800-2000 tokens)**: Multi-stage encounters, major revelations

### Character Subagent System

#### Architecture Overview
The system employs a dual-representation character model:

```
Persistent JSON Profiles ←→ Runtime Markdown Subagents
      (State Storage)          (Behavioral Context)
```

#### Bidirectional Synchronization Flow
```
Character Creation → JSON Profile → Convert to Subagent → Runtime Deployment
                                                     ↓
Event Processing → Subagent Invocation → Character Response → Evolution Extraction
                                                     ↓
Profile Update ← Extract Changes ← Analyze Response ← Character Actions
      ↓
Runtime Refresh ← Updated Subagent ← Apply Evolution ← Updated Profile
```

#### Character Profile Structure (`schemas/character-profile.json`)
```json
{
  "core_identity": ["2-3 immutable traits"],
  "current_status": {
    "health": "condition",
    "resources": "available assets",
    "location": "current position"
  },
  "recent_evolution": "changes from recent events",
  "active_goals": ["1-3 immediate objectives"],
  "key_relationships": {
    "character_name": {
      "connection": "relationship nature",
      "sentiment": "hostile|suspicious|neutral|friendly|devoted"
    }
  },
  "decision_framework": {
    "primary_drive": "core motivation",
    "risk_tolerance": "low|medium|high",
    "preferred_tactics": ["approach patterns"],
    "evolution_triggers": ["change catalysts"]
  }
}
```

#### Runtime Subagent Deployment
Subagents are deployed to `.claude/agents/runtime/[adventure-name]/` with markdown format:

```markdown
---
name: character-[name-slug]
description: "RPG character [role] for [adventure-name] adventure"
tools: ["*"]
---

# Character Instructions and Behavioral Context
# Real-time character state and response protocols
```

### State Management Architecture

#### Event State Package Structure (`schemas/event-state.json`)
```json
{
  "event_number": "current event in sequence",
  "world_state": {
    "location": "compressed location description",
    "active_elements": ["threats/opportunities"],
    "resources": ["available assets"]
  },
  "character_states": [
    {
      "id": "character-[name-slug]",
      "status": "health/resources status",
      "evolution": "recent changes",
      "context": "relevant recent actions"
    }
  ],
  "action_log": [
    {
      "event": "number",
      "summary": "outcome description",
      "consequences": ["ongoing effects"]
    }
  ],
  "next_event_setup": {
    "trigger": "event initiation",
    "stakes": "what's at risk",
    "complexity": "low|medium|high"
  }
}
```

#### File Organization Strategy
```
adventures/[adventure-name]/
├── scenario.json              # Adventure configuration
├── characters/                # Persistent JSON profiles
│   └── character-[name].json
├── events/                    # Compressed state packages
│   └── event-[X]-state.json
├── logs/                      # Optional detailed transcripts
│   └── event-[X].[format]
└── prompts/                   # Adventure-specific automation
    ├── simulate-adventure.md
    ├── summarize-adventure.md
    └── narrate-adventure.md
```

### Prompt-Driven Automation System

#### Core Prompt Architecture
The system uses a hierarchical prompt structure:

```
prompts/                           # Global system prompts
├── generate-scenario.md           # Parameter collection & validation
├── generate-adventure.md          # Adventure initialization
└── system/                        # Character management automation
    ├── convert-character-to-subagent.md
    ├── extract-character-evolution.md
    └── invoke-character-subagent.md
```

#### Adventure-Specific Automation
Each adventure generates custom prompts:

**`simulate-adventure.md`**: Complete automation workflow
```markdown
## Automated Execution Workflow

### Phase 1: Character Subagent Setup
Converting character profiles to runtime subagents

### Phase 2: Event State Detection
Determining current adventure progress and next event

### Phase 3: Event Processing with Character Participation
Character subagent invocation → authentic responses → mechanic resolution

### Phase 4: Character Evolution Processing
Extract growth → update JSON profiles → refresh runtime subagents

### Phase 5: State Persistence and Logging
Save event state → create transcripts → prepare next event
```

## Agentic Workflow Patterns

### 1. Adventure Generation Workflow
```
Scenario Selection → Parameter Validation → Character Creation → 
Profile Generation → Adventure Directory Creation → 
Initial State Package → Adventure-Specific Prompts
```

### 2. Event Simulation Workflow
```
Load Previous State → Setup Event Context → 
Character Subagent Invocation → Collect Responses → 
Mechanic Resolution → Extract Character Evolution → 
Update Persistent Profiles → Refresh Runtime Subagents → 
Save Event State → Generate Next Event Setup
```

### 3. Character Evolution Workflow
```
Analyze Subagent Responses → Identify Change Patterns → 
Extract Specific Evolution Data → Update JSON Profile → 
Convert to Runtime Subagent → Deploy Updated Context → 
Maintain Session Continuity
```

### 4. State Persistence Workflow
```
Compress World State → Compress Character States → 
Generate Action Log Entry → Create Next Event Setup → 
Save Event Package → Optional Detailed Transcript → 
Prepare State Handoff
```

## Data Flow Architecture

### Character Data Synchronization
```
JSON Profile ──convert──→ Runtime Subagent ──invoke──→ Character Response
     ↑                                                        ↓
Update Profile ←──extract──← Evolution Analysis ←──analyze──← Response Data
```

### Event Processing Pipeline
```
Previous Event State → Load → Event Setup → Character Actions → 
Mechanic Resolution → Character Evolution → World Updates → 
Next Event State → Save → Handoff
```

### Adventure Continuation Flow
```
Event N State Package → Process Event N+1 → Generate Event N+1 State → 
Load for Event N+2 → Continuous Adventure Progression
```

## Schema-Driven Validation

### Data Structure Definitions
- **`character-profile.json`**: Validates character JSON structure with required fields and constraints
- **`event-state.json`**: Ensures consistent event state package format
- **`scenario.json`**: Validates adventure configuration parameters
- **`character-subagent.md`**: Template specification for runtime subagent format

### Validation Points
1. **Adventure Generation**: Scenario parameter validation before creation
2. **Character Creation**: Profile structure validation against schema
3. **Event Processing**: State package format validation
4. **Subagent Deployment**: Markdown format and frontmatter validation

## Implementation Patterns

### Automated Prompt Execution
The system minimizes manual intervention through:
- **Parameter Collection**: Inverse prompting for missing scenario data
- **Adventure Initialization**: Complete directory structure creation
- **Event Processing**: Fully automated character subagent participation
- **State Management**: Automatic persistence and synchronization

### Error Handling & Recovery
- **Missing Subagents**: Automatic conversion from JSON profiles
- **Session Interruption**: Character evolution preserved in persistent profiles
- **Context Recovery**: Runtime subagent regeneration from latest profiles
- **State Validation**: Schema enforcement at all data boundaries

### Extensibility Design
- **Modular Scenarios**: Drop-in scenario configurations for new adventure types
- **Character Archetypes**: Template-based character generation for specific themes
- **Mechanic Systems**: Pluggable resolution systems for different genres
- **Logging Options**: Configurable transcript formats and detail levels

## Token Efficiency Optimizations

### Budget Enforcement
- **Hard Limits**: Absolute token caps prevent context overflow
- **Graduated Costs**: Action complexity tiers encourage strategic choices
- **Budget Tracking**: Real-time token usage monitoring and reporting

### Narrative Optimization
- **Compressed States**: Essential information preservation without bloat
- **Focused Actions**: Token costs drive decisive character behaviors
- **Efficient Handoffs**: Minimal context required for event continuation

## Example Adventure Flow

### Adventure: "Neural Magic Awakening" (scifi-fantasy-neural-magic-20250802)

#### 1. Adventure Generation
```yaml
Scenario: scifi-fantasy-neural-magic.json
Characters: 2 (Kavitha Subramanian, Tane Rahotu-Williams)
Events: 15 planned
Theme: Futuristic Sci-Fi Fantasy
Token Budget: 2000 per event, 300 setup, 150 per character action
```

#### 2. Character Profiles Created
- **Persistent Storage**: `adventures/scifi-fantasy-neural-magic-20250802/characters/`
- **Subagent Deployment**: `.claude/agents/runtime/scifi-fantasy-neural-magic-20250802/`

#### 3. Event Processing (Event 1)
```yaml
Token Usage:
  setup: 300 (world state, stakes establishment)
  character_actions: 300 (150 × 2 characters)
  mechanic_resolutions: 200 (neural-magical discovery)
  state_update: 200 (character evolution, world changes)
  total: 1000/2000 (efficient usage)
```

#### 4. Character Evolution
- **Kavitha**: Corporate insider → underground protector
- **Tane**: Traditional knowledge → validated scientific integration
- **Profiles Updated**: JSON persistence + runtime subagent refresh

#### 5. State Handoff
```json
{
  "event_number": 1,
  "next_event_setup": {
    "trigger": "Corporate security investigation begins",
    "stakes": "Escape vs. capture choice",
    "complexity": "high"
  }
}
```

This architecture enables sophisticated narrative generation through autonomous character behavior, intelligent resource management, and persistent world evolution, all operating within strict computational boundaries for scalable adventure creation.