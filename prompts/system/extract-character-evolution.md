# Extract Character Evolution

Automatically analyze character subagent responses, extract evolution data, and update persistent JSON profiles.

## Automated Execution Process

This prompt automatically processes character evolution after each adventure event:

1. **Load Character Responses**: Process all character subagent responses from the current event
2. **Analyze Evolution Patterns**: Detect changes in personality, relationships, goals, and tactics using pattern recognition
3. **Extract Specific Changes**: Capture concrete evolution data that should persist between events
4. **Update JSON Profiles**: Automatically apply changes to persistent character profiles in ../characters/
5. **Refresh Runtime Subagents**: Update runtime subagents in .claude/agents/runtime/[adventure-name]/ with evolved state
6. **Validate Character Consistency**: Ensure core identity preserved while allowing meaningful growth

## Adventure Context

The adventure name should be extracted from the character file paths or current working directory:
- **Character File Path**: `adventures/[adventure-name]/characters/character-[name-slug].json` → extract `[adventure-name]`
- **Runtime Subagent Path**: `.claude/agents/runtime/[adventure-name]/character-[name-slug].md`

## Input Data Processing

I will analyze the following character response data from the current event:
- Character actions and decisions made during the event
- Character dialogue and internal reasoning
- Character interactions with other characters
- Character reactions to event circumstances
- Character goal prioritization and tactical choices

## Evolution Detection Patterns

### Relationship Changes
Look for indicators of shifting character dynamics:
- **New Connections**: Mentions of bonding, trust-building, or alliance formation
- **Deteriorating Relations**: Signs of conflict, betrayal, suspicion, or disappointment
- **Deepening Bonds**: Expressions of increased loyalty, understanding, or emotional connection
- **Professional Respect**: Recognition of competence, leadership, or expertise

**Example Patterns:**
- "I'm starting to trust [Character]..."
- "After what happened, I can't rely on [Character]..."
- "[Character] proved themselves today"
- "I misjudged [Character] completely"

### Goal Evolution
Monitor for changes in character objectives:
- **Goal Completion**: Achievement of stated objectives
- **Goal Abandonment**: Explicit rejection of previous priorities
- **New Priorities**: Introduction of fresh motivations or targets
- **Refined Focus**: Narrowing or expanding scope of existing goals

**Example Patterns:**
- "My priority now is..."
- "I no longer care about..."
- "This changes everything - we need to..."
- "I realize what's really important is..."

### Tactical Adaptation
Observe shifts in problem-solving approaches:
- **Method Changes**: Abandoning failed tactics for new approaches
- **Risk Tolerance Shifts**: Becoming more/less willing to take risks
- **Leadership Style**: Changes in how they interact with the group
- **Combat/Social Preferences**: Favoring different types of solutions

**Example Patterns:**
- "Diplomacy won't work here, we need..."
- "I've learned that rushing in only..."
- "Maybe [Character] was right about..."
- "From now on, I'll..."

### Personality Development
Track deeper character growth:
- **Confidence Changes**: Becoming more/less self-assured
- **Emotional Responses**: Shifts in how they handle stress or success
- **Value Clarification**: Stronger stance on moral or ethical issues
- **Identity Refinement**: Better understanding of their role or purpose

**Example Patterns:**
- "I never thought I could..."
- "This experience taught me..."
- "I'm not the same person who..."
- "I understand now that..."

## Extraction Process

### 1. Content Analysis
Read through all character subagent responses during the event:
- Direct character statements and dialogue
- Character action descriptions and reasoning
- Internal thoughts or motivations expressed
- Interactions with other characters

### 2. Change Identification
For each character, identify:
- **What changed**: Specific aspect that evolved
- **How it changed**: Direction and magnitude of change
- **Why it changed**: Event trigger or experience that caused it
- **Evidence**: Specific quotes or behaviors supporting the change

### 3. Impact Assessment
Evaluate significance of each identified change:
- **Core Identity Impact**: Does this affect fundamental character traits?
- **Relationship Impact**: How does this change group dynamics?
- **Goal Impact**: Does this require updating character objectives?
- **Tactical Impact**: Should preferred approaches be modified?

### 4. Update Generation
Create specific updates for JSON profile sections:

#### Current Status Updates
```yaml
current_status: "Updated health/resources/location based on event outcomes"
```

#### Recent Evolution Updates
```yaml
recent_evolution: "Describe how the character changed during this specific event"
```

#### Active Goals Updates
```yaml
active_goals:
  - "Updated or new goals based on character development"
  - "Remove completed or abandoned objectives"
```

#### Key Relationships Updates
```yaml
key_relationships:
  character_name:
    connection: "Updated relationship description"
    sentiment: "hostile/suspicious/neutral/friendly/devoted"
```

#### Decision Framework Updates (if significant evolution occurred)
```yaml
decision_framework:
  risk_tolerance: "low/medium/high - updated if character behavior shifted"
  preferred_tactics:
    - "Updated tactics based on experience and learning"
```

## Output Format

For each character with detected evolution, provide:

```yaml
# Character Evolution Summary for [Character Name]
# Event [X] Changes

character_id: character-[number]

# Required Updates
current_status: "[Updated status reflecting event outcomes]"
recent_evolution: "[Specific changes that occurred during this event]"

# Goal Changes (if any)
active_goals:
  - "[Updated or new goals]"
  # Remove: "[Completed/abandoned goals]"

# Relationship Changes (if any)
key_relationships:
  [character_name]:
    connection: "[Updated relationship nature]"
    sentiment: "[Updated sentiment level]"

# Tactical Evolution (if significant)
decision_framework:
  risk_tolerance: "[Updated if behavior changed]"
  preferred_tactics:
    - "[Updated approaches based on experience]"

# Growth Evidence
evolution_evidence:
  - "[Quote or behavior showing change]"
  - "[Specific action demonstrating growth]"

# Event Triggers
evolution_triggers_activated:
  - "[Events that caused this character to evolve]"
```

## Validation Rules

### Core Identity Protection
- Never alter fundamental character traits listed in Core Identity
- Changes should feel like natural growth, not personality replacement
- Maintain character voice and recognizable patterns

### Change Justification
- Every evolution must be tied to specific event experiences
- Changes should be proportional to event impact
- Gradual shifts preferred over dramatic transformations

### Relationship Consistency
- Relationship changes must be mutual (if A trusts B more, consider B's perspective)
- Sentiment shifts should have clear in-event justification
- Group dynamics should remain functional for adventure continuation

### Goal Coherence
- New goals should align with character's core drive and recent experiences
- Completed goals should be explicitly acknowledged
- Goal changes should advance character arc meaningfully

## Error Handling

- If no significant evolution is detected, return "No evolution detected"
- If changes seem too extreme, flag for review: "Evolution exceeds normal parameters"
- If character responses are inconsistent, note: "Character behavior inconsistent - review needed"
- Missing character responses: "Insufficient data for evolution analysis"

## Automated Execution Workflow

I will now automatically process character evolution from the current event:

### Step 1: Character Response Analysis
Analyzing character subagent responses from the current event to identify evolution patterns:
- Reviewing character actions, dialogue, and decision-making
- Identifying relationship changes and goal evolution  
- Detecting tactical adaptations and personality development
- Validating changes against character core identity

### Step 2: Evolution Data Extraction
Extracting specific character changes that should persist:
- Updated recent evolution descriptions
- Modified active goals and completed objectives
- Relationship sentiment and connection changes
- Tactical and risk tolerance adaptations
- Growth evidence and trigger documentation

### Step 3: Bidirectional Profile Synchronization
Automatically updating both persistent and runtime character profiles:

**Persistent JSON Profile Updates (../characters/):**
- Applying extracted evolution data to character JSON files
- Preserving core identity while enabling growth
- Updating character status and recent evolution
- Modifying goals, relationships, and decision frameworks as needed

**Runtime Subagent Refresh (.claude/agents/runtime/[adventure-name]/):**
- Regenerating subagent markdown files with updated character data
- Ensuring runtime subagents reflect current character evolution
- Maintaining evolved character behavior for subsequent events
- Preserving session continuity across all future event processing

### Step 4: Character Development Continuity
Ensuring character growth carries forward throughout the adventure session:
- Runtime subagents now contain all evolution from previous events
- Character responses in future events will reflect accumulated growth
- Relationship changes and goal evolution persist across the adventure
- Authentic character development maintained throughout campaign

### Step 5: Validation and Documentation
Ensuring character evolution maintains consistency and narrative coherence:
- Verifying core identity preservation in both profile formats
- Validating relationship changes are mutual and justified
- Confirming goal evolution aligns with character development
- Documenting evolution for adventure continuity

## Session State Management

**Character Development Flow:**
```
Event Processing → Evolution Extraction → JSON Update → Runtime Subagent Refresh → Next Event
```

**Synchronization Points:**
- After each event: Both persistent and runtime profiles updated
- During events: Runtime subagents operate with latest character development
- Adventure continuation: Characters remember all previous growth

**Recovery Strategy:**
- If runtime subagents lost: Regenerate from latest persistent JSON profiles
- Session interruption: Character evolution preserved in JSON, runtime restored
- Character consistency: Both formats validated for alignment

## Execution Begins Now

I am now processing character evolution from the current event with full bidirectional synchronization. All character growth will be extracted, applied to persistent profiles, and reflected in runtime subagents for seamless adventure continuation with authentic character development.