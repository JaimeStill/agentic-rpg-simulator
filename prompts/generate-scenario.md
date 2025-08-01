# Generate Parameters

Create a new parameters.yml file for an RPG adventure through guided configuration or randomization.

## Execution Mode

Check for command modifier:
- If "randomize" is specified → Generate completely random parameters
- Otherwise → Use inverse prompting to gather parameters from user

## Inverse Prompting Protocol

For each parameter, provide:
1. Parameter name and description
2. Valid ranges or options
3. Examples to inspire choices
4. Default recommendation

### Parameter Collection Sequence

#### 1. Number of Agents (Required)
```
How many characters should participate in this adventure? (1-6)

This determines the party size. Consider:
- 1-2: Intimate, character-focused narrative
- 3-4: Balanced party dynamics (recommended)
- 5-6: Complex interactions, ensemble cast

Default: 3
```

#### 2. Number of Events (Required)
```
How many events should the adventure contain? (5-20)

Each event is a complete scene or encounter. Consider:
- 5-8: Short adventure, single session
- 9-14: Medium adventure, mini-campaign (recommended)
- 15-20: Epic adventure, full campaign

Default: 12
```

#### 3. Theme (Required)
```
What theme should define the adventure world?

Examples:
- Fantasy: Magic, dragons, ancient prophecies
- Sci-Fi: Space exploration, alien encounters, technology
- Horror: Supernatural threats, psychological terror
- Post-Apocalyptic: Survival, rebuilding, resource scarcity
- Steampunk: Victorian technology, airships, clockwork
- Cyberpunk: Hackers, corporations, digital consciousness
- Historical: Real-world periods with adventure elements
- Superhero: Powers, villains, saving the world
- Mystery: Investigation, clues, hidden truths
- Random: Let the system surprise you!

Enter theme or "Random":
```

#### 4. Scenario (Required)
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

Enter scenario description or "Random":
```

#### 5. Context Management Settings
```
Would you like to customize token management? (yes/no)

These are advanced settings that control adventure pacing:
- max_event_tokens: Maximum tokens per event (default: 2000)
- action_cost: Tokens per character action (default: 150)
- mechanic_cost: Tokens per mechanic resolution (default: 200)
- description_budget: Tokens for scene setup (default: 300)

Default: no (use standard settings)
```

#### 6. Complexity Distribution
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

Choice (1-4):
```

#### 7. Evolution Settings
```
How quickly should characters and the world change?

Character Evolution Rate:
- Slow: Gradual changes, stable personalities
- Moderate: Noticeable growth each 3-4 events (default)
- Rapid: Dramatic changes, volatile development

World Persistence:
- Low: Events have minimal lasting impact
- High: Consequences carry forward strongly (default)

Mechanic Learning:
- Enabled: Combat/social systems adapt to patterns (default)
- Disabled: Consistent mechanic resolution

Enter preferences or press Enter for defaults:
```

## Random Generation Mode

When "randomize" is specified:

1. **Number of Agents**: Weighted random (1-2: 20%, 3-4: 60%, 5-6: 20%)
2. **Number of Events**: Weighted random (5-8: 25%, 9-14: 50%, 15-20: 25%)
3. **Theme**: Equal probability from preset list
4. **Scenario**: Generate appropriate scenario based on theme using templates
5. **Token Settings**: Use defaults
6. **Complexity**: Use balanced distribution
7. **Evolution**: Use moderate/high/enabled defaults

## Output Format

Generate `parameters.yml` with:
```yaml
# Lightweight RPG Adventure Parameters
# Generated: [timestamp]
# Mode: [Guided/Random]

# Core Parameters
number_of_agents: [value] # [Description of choice]
number_of_events: [value] # [Description of choice]
theme: "[value]" # [Description or inspiration]
scenario: "[value]" # Full scenario description

# Context Management
max_event_tokens: [value]
action_cost: [value]
mechanic_cost: [value]
description_budget: [value]

# Event Complexity Distribution
complexity_mix:
  low: [value]% # Simple encounters
  medium: [value]% # Standard challenges
  high: [value]% # Major events

# State Evolution Settings
character_evolution_rate: "[value]" # How quickly characters change
world_persistence: "[value]" # How much world state carries forward
mechanic_learning: [value] # Whether mechanics adapt

# Generation Metadata
generation_mode: "[Guided/Random]"
generation_date: "[timestamp]"
```

## Validation

Before saving:
1. Verify all required parameters are present
2. Check value ranges are valid
3. Ensure percentages sum to 100%
4. Confirm file will overwrite if exists (with user permission)

## Completion Message

```
Scenario generated successfully!
Saved to: [output location]

Adventure Profile:
- Party Size: [X] characters
- Length: [X] events
- Theme: [theme]
- Scenario: [first 100 chars of scenario]...

To generate your adventure, run:
Prompt: generate-adventure.md
```