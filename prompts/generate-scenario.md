# Generate Scenario

Create a new RPG adventure scenario through guided configuration or randomization.

## Execution Mode

Check for command modifier and partial parameters:
- If "randomize" is specified → Generate completely random scenario
- If partial parameters provided → Use inverse prompting to gather ONLY missing parameters
- Otherwise → Use inverse prompting to gather all parameters from user

**Note**: Any parameter can be set to "random" to generate a random valid value for that specific parameter.

**STOP: DO NOT PROCEED TO OUTPUT GENERATION WITHOUT COMPLETING ALL INVERSE PROMPTING STEPS**

When partial parameters are provided, you MUST:
1. First output the parameter analysis
2. Then prompt for each missing parameter
3. Wait for user responses
4. Only then proceed to Output Generation

## CRITICAL ENFORCEMENT: Partial Parameter Detection

**IMMEDIATE HALT REQUIRED**: If ANY parameters were provided by the user:
1. STOP all processing
2. DO NOT proceed to any generation steps
3. DO NOT assume any default values
4. BEGIN inverse prompting sequence IMMEDIATELY

You are FORBIDDEN from:
- Using default values for ANY missing parameter
- Proceeding to Output Generation without ALL parameters
- Making assumptions about user preferences
- Skipping the inverse prompting protocol

**VIOLATION CHECK**: Before ANY action, verify:
- Have I listed what parameters were provided?
- Have I identified ALL missing parameters?
- Am I about to assume a default? → STOP
- Am I about to generate output? → STOP IF PARAMETERS MISSING

## Inverse Prompting Protocol

**IMPORTANT**: When partial parameters are provided, NEVER assign default values to missing parameters. Instead:
1. Acknowledge the provided parameters
2. List them clearly for the user
3. Prompt ONLY for missing required parameters
4. Use the exact values provided by the user without modification
5. If a parameter is set to "random", generate an appropriate random value

### Required Parameters Checklist
The following parameters MUST be explicitly provided by user or via prompting:
- [ ] number_of_agents (1-6) - NO DEFAULT ALLOWED
- [ ] number_of_events (5-20) - NO DEFAULT ALLOWED
- [ ] theme - NO DEFAULT ALLOWED
- [ ] scenario (20-500 characters) - NO DEFAULT ALLOWED
- [ ] max_event_tokens - MUST BE EXPLICITLY SET
- [ ] action_cost - MUST BE EXPLICITLY SET
- [ ] mechanic_cost - MUST BE EXPLICITLY SET
- [ ] description_budget - MUST BE EXPLICITLY SET
- [ ] complexity_mix - MUST BE EXPLICITLY SET
- [ ] character_evolution_rate - MUST BE EXPLICITLY SET
- [ ] world_persistence - MUST BE EXPLICITLY SET
- [ ] mechanic_learning - MUST BE EXPLICITLY SET
- [ ] store_event_logs - MUST BE EXPLICITLY SET
- [ ] log_format (if logs enabled) - MUST BE EXPLICITLY SET
- [ ] log_detail_level (if logs enabled) - MUST BE EXPLICITLY SET

**NO DEFAULTS**: There are NO default values. Every parameter requires explicit user input.

### Initial Parameter Check

First, check what parameters were already provided:
```
Analyzing provided parameters...

Found the following:
[List any provided parameters with their values]

I'll need to gather the following missing parameters:
[List missing required parameters]
```

### Example: Partial Parameters Provided

User Input: "Theme: Space Opera, Agents: 4"

CORRECT RESPONSE:
```
Analyzing provided parameters...

Found the following:
- Theme: Space Opera
- Number of Agents: 4

I'll need to gather the following missing parameters:
- Number of events
- Scenario description
- Token management settings
- Complexity distribution
- Evolution settings
- Event logging configuration

Let's start with the number of events:

How many events should the adventure contain? (5-20 or "random")
[... continue with prompting sequence ...]
```

INCORRECT RESPONSE:
```
[Immediately creating scenario file with assumed defaults]
```

### MANDATORY PARAMETER CHECK POINT #1

**STOP HERE**: Before reading ANY further in this prompt:
1. Have you identified provided parameters? If no → Do it now
2. Have you listed missing parameters? If no → Do it now  
3. Are you about to continue without prompting? → STOP

If you have not yet prompted the user for missing parameters, you MUST:
- Stop processing this prompt
- Begin the inverse prompting sequence
- Return here only after ALL parameters are collected

**DO NOT CONTINUE PAST THIS POINT WITH MISSING PARAMETERS**

### Common Mistakes to Avoid

**NEVER**:
- Jump directly to file creation when parameters are missing
- Assume default values for unprovided parameters
- Interpret or expand on user-provided values
- Skip the parameter confirmation step
- Proceed without explicit user input for each missing parameter

### Example: Correct Partial Parameter Handling

User Input: "Theme: Cyberpunk, Agents: 3, Events: 9, Scenario: Elite crew hired to steal experimental..."

REQUIRED RESPONSE:
```
Analyzing provided parameters...

Found the following:
- Theme: Cyberpunk  
- Number of Agents: 4
- Number of Events: 10
- Scenario: Elite crew hired to steal experimental neural implants from Nexus Corp's quantum-encrypted vault. The implants grant superhuman cognition but may have hidden purposes. Double-crosses expected.

I need to gather the following missing parameters:
- Token management settings (max_event_tokens, action_cost, mechanic_cost, description_budget)
- Complexity distribution (low/medium/high percentages)
- Evolution settings (character_evolution_rate, world_persistence, mechanic_learning)
- Event logging configuration (store_event_logs, and if enabled: format and detail level)

Let's start with the token management settings:

Token management parameters are REQUIRED. How would you like to set them?

1. Standard preset: max_event_tokens=2000, action_cost=150, mechanic_cost=200, description_budget=300
2. Compact preset: max_event_tokens=1500, action_cost=100, mechanic_cost=150, description_budget=200
3. Extended preset: max_event_tokens=2500, action_cost=200, mechanic_cost=250, description_budget=400
4. Custom: Specify each value individually
5. Random: Let the system choose from presets

Enter choice (1-5):
```

FORBIDDEN RESPONSE:
```
I'll create a Cyberpunk neural heist scenario with your parameters and use default values for the rest...
[Proceeds to create file]
```

### Parameter Collection Sequence

#### 1. Number of Agents (If not provided)
```
How many characters should participate in this adventure? (1-6 or "random")

This determines the party size. Consider:
- 1-2: Intimate, character-focused narrative
- 3-4: Balanced party dynamics (recommended)
- 5-6: Complex interactions, ensemble cast
- "random": Let the system choose

Enter number (1-6) or "random":
```

If "random": Use weighted distribution (1-2: 20%, 3-4: 60%, 5-6: 20%)

#### 2. Number of Events (If not provided)
```
How many events should the adventure contain? (5-20 or "random")

Each event is a complete scene or encounter. Consider:
- 5-8: Short adventure, single session
- 9-14: Medium adventure, mini-campaign (recommended)
- 15-20: Epic adventure, full campaign
- "random": Let the system choose

Enter number (5-20) or "random":
```

If "random": Use weighted distribution (5-8: 25%, 9-14: 50%, 15-20: 25%)

#### 3. Theme (If not provided)
```
What theme should define the adventure world?

Options:
- Fantasy: Magic, dragons, ancient prophecies
- Sci-Fi: Space exploration, alien encounters, technology
- Horror: Supernatural threats, psychological terror
- Post-Apocalyptic: Survival, rebuilding, resource scarcity
- Steampunk: Victorian technology, airships, clockwork
- Cyberpunk: Hackers, corporations, digital consciousness
- Historical: Real-world periods with adventure elements
- Superhero: Powers, villains, saving the world
- Mystery: Investigation, clues, hidden truths
- "random": Let the system choose

Enter theme or "random":
```

If "random": Select with equal probability from the theme list

#### 4. Scenario (If not provided)
```
What scenario launches the adventure?

[If theme was selected, provide theme-appropriate examples]

Fantasy examples:
- "Ancient tomb discovery with active magical guardians"
- "Dragon's curse spreading through the kingdom"
- "Portal to demon realm opening in peaceful village"
- "Lost heir must reclaim throne from usurper"
- "Magical plague requires quest for cure"

Sci-Fi examples:
- "Distress signal from derelict alien vessel"
- "Colony ship malfunction threatens thousands"
- "First contact goes dangerously wrong"
- "Time loop trapping space station"
- "AI uprising on mining platform"

[Continue with appropriate examples based on theme]

Enter scenario description (20-500 characters) or "random":
```

If "random": Generate appropriate scenario based on selected theme

#### 5. Token Management Settings (If not provided)
```
Token management parameters are REQUIRED. How would you like to set them?

1. Standard preset: max_event_tokens=2000, action_cost=150, mechanic_cost=200, description_budget=300
2. Compact preset: max_event_tokens=1500, action_cost=100, mechanic_cost=150, description_budget=200
3. Extended preset: max_event_tokens=2500, action_cost=200, mechanic_cost=250, description_budget=400
4. Custom: Specify each value individually
5. Random: Let the system choose from presets

Enter choice (1-5):
```

If "random": Select preset 1-3 with equal probability

[If custom selected]
```
Enter specific values for each parameter:
Maximum tokens per event (1000-3000 or "random"): 
Tokens per character action (50-300 or "random"): 
Tokens per mechanic resolution (100-400 or "random"): 
Tokens for scene setup (200-500 or "random"): 
```

#### 6. Complexity Distribution (If not provided)
```
How should event complexity be distributed?

Low complexity: Simple encounters, character moments
Medium complexity: Standard challenges, moderate stakes
High complexity: Boss battles, major plot points

Presets:
1. Steady Build: 60% low, 30% medium, 10% high
2. Balanced: 40% low, 45% medium, 15% high (default)
3. Intense: 20% low, 50% medium, 30% high
4. Custom: Specify your own percentages
5. Random: Let the system choose

Choice (1-5) or "random":
```

If "random": Select preset 1-3 with equal probability

[If custom selected]
```
Enter percentages for each complexity level:
Low % (or "random"): 
Medium % (or "random"): 
High % (or "random"): 

Note: Percentages must sum to 100%. If using "random" for any value, others will be adjusted.
```

#### 7. Evolution Settings (If not provided)
```
How quickly should characters and the world change?

Character Evolution Rate (slow/moderate/rapid/random):
- Slow: Gradual changes, stable personalities
- Moderate: Noticeable growth each 3-4 events (default)
- Rapid: Dramatic changes, volatile development
- Random: Let the system choose

Enter choice:
```

```
World Persistence (low/high/random):
- Low: Events have minimal lasting impact
- High: Consequences carry forward strongly (default)
- Random: Let the system choose

Enter choice:
```

```
Mechanic Learning (true/false/random):
- true: Combat/social systems adapt to patterns (default)
- false: Consistent mechanic resolution
- Random: Let the system choose

Enter choice:
```

#### 8. Event Logging Configuration (If not provided)
```
Would you like to enable detailed event logging? (yes/no/random)

Event logs save complete transcripts of each adventure event, including:
- Full narrative descriptions
- All character actions and dialogue
- Mechanic resolutions and outcomes
- Token usage breakdowns

This is useful for reviewing adventures or sharing stories.

Enter choice (yes/no/random):
```

If "random": 30% chance yes, 70% chance no

[If yes, continue with format and detail options]

```
What format should event logs use? (markdown/yaml/json/random)
- markdown: Rich text with formatting (default)
- yaml: Structured data format
- json: Machine-readable format
- random: Let the system choose

Enter format:
```

```
How detailed should event logs be? (minimal/standard/verbose/random)
- minimal: Key outcomes and state changes only
- standard: Full event transcript with actions (default)  
- verbose: Extended narrative with additional context
- random: Let the system choose

Enter detail level:
```

## FINAL PARAMETER VERIFICATION - DO NOT SKIP

**ABSOLUTE REQUIREMENT**: You MUST verify EVERY parameter:

Parameter Verification Checklist:
- [ ] number_of_agents: _______ (provided/collected)
- [ ] number_of_events: _______ (provided/collected)
- [ ] theme: _______ (provided/collected)
- [ ] scenario: _______ (provided/collected)
- [ ] max_event_tokens: _______ (provided/collected)
- [ ] action_cost: _______ (provided/collected)
- [ ] mechanic_cost: _______ (provided/collected)
- [ ] description_budget: _______ (provided/collected)
- [ ] complexity_mix: _______ (provided/collected)
- [ ] character_evolution_rate: _______ (provided/collected)
- [ ] world_persistence: _______ (provided/collected)
- [ ] mechanic_learning: _______ (provided/collected)
- [ ] store_event_logs: _______ (provided/collected)
- [ ] log_format: _______ (if applicable)
- [ ] log_detail_level: _______ (if applicable)

**ERROR STATE**: If ANY parameter above is not explicitly set:
1. HALT IMMEDIATELY
2. Return to inverse prompting
3. Do not proceed to Output Generation
4. Do not use any default values

Only proceed if EVERY checkbox can be marked with an actual user-provided or user-confirmed value.

## Scenario Naming

After gathering all parameters, generate a descriptive 1-3 term name:
- Format: `[theme]-[key-concept]` or `[theme]-[descriptor]-[concept]`
- Examples: 
  - "cyberpunk-neural-heist"
  - "fantasy-awakened-peasant"
  - "mystery-mansion-murders"
  - "scifi-first-contact"
  - "postapoc-water-wars"

## Random Generation Mode

When "randomize" is specified or when individual parameters are set to "random":

### Random Value Generation Rules

1. **Number of Agents**: Weighted random (1-2: 20%, 3-4: 60%, 5-6: 20%)
2. **Number of Events**: Weighted random (5-8: 25%, 9-14: 50%, 15-20: 25%)
3. **Theme**: Equal probability from preset list
4. **Scenario**: Generate appropriate scenario based on theme using templates
5. **Token Settings**: 
   - 80% use defaults
   - 20% randomize within valid ranges
6. **Complexity**: Equal probability among three presets
7. **Evolution Settings**:
   - Character Evolution: Equal probability (slow/moderate/rapid)
   - World Persistence: 70% high, 30% low
   - Mechanic Learning: 80% enabled, 20% disabled
8. **Event Logging**: 
   - Enable: 30% yes, 70% no
   - Format: 60% markdown, 25% yaml, 15% json
   - Detail: 20% minimal, 60% standard, 20% verbose

## Output Generation

### 1. Save Scenario File

Generate `scenarios/[scenario-name].json`:

```json
{
  "_comments": "[Title based on theme and scenario] - [One-line description]",
  "number_of_agents": "[value - Character description]",
  "number_of_events": "[value - Adventure length description]", 
  "theme": "[value - Theme description]",
  "scenario": "[value - Full scenario description]",
  "max_event_tokens": "[value]",
  "action_cost": "[value]",
  "mechanic_cost": "[value]", 
  "description_budget": "[value]",
  "complexity_mix": {
    "low": "[value - Simple encounters]",
    "medium": "[value - Standard challenges]",
    "high": "[value - Major events]"
  },
  "character_evolution_rate": "[value - How quickly characters change]",
  "world_persistence": "[value - How much consequences carry forward]",
  "mechanic_learning": "[value - Whether mechanics adapt]",
  "store_event_logs": "[value - Whether to save detailed transcripts]",
  "log_format": "[value - Format for log files]",
  "log_detail_level": "[value - Amount of detail in logs]",
  "_scenario_specific": "[Add 2-4 relevant settings based on theme/scenario as additional properties]",
  "generation_mode": "[Guided/Random/Mixed - Mixed if some params were random]",
  "generation_date": "[YYYY-MM-DD]",
  "scenario_author": "Generated",
  "difficulty_rating": "[Based on complexity and settings]"
}
```

### 2. Update scenarios/README.md

Add new entry to the scenarios list:

```markdown
### [Next Number]. **[scenario-name].json**
**Theme:** [Theme]  
**Length:** [X] events ([Short/Medium/Long])  
**Party Size:** [X] characters  
**Complexity:** [Brief description based on distribution]  

[Expanded scenario description, 2-3 sentences]

**Best For:** [Target player preferences based on settings]

---
```

## Validation

Before saving:
1. Verify all required parameters are present
2. Check value ranges are valid
3. Ensure complexity percentages sum to 100%
4. Check for duplicate scenario names in scenarios/ directory
5. Validate scenario description length (20-500 characters)
6. Ensure "random" values have been replaced with actual values

## Completion Message

```
Scenario generated successfully!
Saved to: scenarios/[scenario-name].json
Updated: scenarios/README.md

Adventure Profile:
- Party Size: [X] characters
- Length: [X] events  
- Theme: [theme]
- Scenario: [first 100 chars of scenario]...
- Event Logging: [Enabled/Disabled]
- Generation Mode: [Guided/Random/Mixed]

To use this scenario:
1. Run: Prompt: generate-adventure.md
2. Select: [scenario-name]

Or to use directly:
Prompt: generate-adventure.md
Scenario: scenarios/[scenario-name].json
```
