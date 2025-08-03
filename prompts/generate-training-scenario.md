# Generate Training Scenario

Create RPG adventure scenarios optimized for extracting training insights and operational lessons. While played as narrative adventures, these scenarios embed decision points, team dynamics, and consequences that mirror real-world training objectives.

## Execution Modes

This prompt supports two distinct execution modes:

### Mode 1: Conditions Provided
When executed with conditions:
```
Prompt: prompts/generate-training-scenario.md
Conditions: [description of training objectives and constraints]
```

Parse the provided conditions flexibly and generate a scenario that naturally embeds the training value. DO NOT require strict parameter formats - interpret creatively.

### Mode 2: Inverse Prompting
When executed without conditions:
```
Prompt: prompts/generate-training-scenario.md
```

Engage in conversational parameter gathering using the training conditions schema as a flexible guide. DO NOT require all parameters - only gather what the user wants to specify.

## Execution Flow

### Step 1: Determine Mode
Check if conditions were provided:
- If YES → Proceed to Condition Analysis (Step 2A)
- If NO → Proceed to Inverse Prompting (Step 2B)

### Step 2A: Condition Analysis (When Conditions Provided)

1. **Parse Training Intent**: Extract key training objectives from the natural language description
2. **Identify Constraints**: Note any specific requirements or limitations mentioned
3. **Infer Missing Elements**: Use reasonable defaults for unspecified aspects
4. **Map to RPG Elements**: Translate training concepts to adventure mechanics

Example condition parsing:
```
Conditions: "Humanitarian crisis response with limited resources and time pressure. 
Team must balance immediate needs against long-term stability."

Extracted:
- Primary objective: Crisis response decision-making
- Constraints: Resource scarcity, time pressure
- Key tension: Short-term vs long-term thinking
- Suggested mechanics: Resource management, timed events, consequence tracking
```

### Step 2B: Inverse Prompting (When No Conditions Provided)

Begin conversational gathering using `schemas/training-conditions.json` as a GUIDE ONLY:

```
I'll help you create a training-oriented adventure scenario. Let's start by 
understanding what kind of training objectives you want to explore.

What's the primary skill or competency you'd like to develop through this scenario?

For example:
- Leadership under pressure
- Resource allocation in crisis
- Team coordination during emergencies
- Ethical decision-making
- Strategic planning with incomplete information

You can describe this in your own words:
```

**IMPORTANT**: 
- Use open-ended questions
- Accept partial responses
- Build on what the user provides
- Don't require all schema fields
- Encourage natural language descriptions

Continue gathering only until you have enough to create a meaningful scenario:

```
[After primary objective]
What kind of operational context interests you?

- Humanitarian mission
- Peacekeeping operation
- Disaster response
- Security situation
- Or describe your own:
```

```
[If relevant to their objectives]
Should the scenario include any specific challenges or constraints?

- Time pressure
- Resource limitations
- Unclear information
- Competing priorities
- Environmental hazards
- Or describe your own:
```

### Step 3: Training-to-RPG Mapping

Translate training concepts to RPG adventure elements:

#### Operational Domains → Themes
- Humanitarian Operations → "Relief Mission Crisis"
- Peacekeeping → "Neutral Zone Tensions"
- Disaster Response → "Natural Catastrophe"
- Crisis Management → "Escalating Emergency"
- Security Operations → "Protection Detail"

#### Training Objectives → Game Mechanics
- Decision-making → Multiple branching paths with consequences
- Resource management → Limited action tokens, supply tracking
- Team coordination → Multi-character actions requiring cooperation
- Leadership → Character influence and morale systems
- Communication → Information sharing mechanics
- Adaptability → Dynamic event generation

#### Constraints → Scenario Parameters
- Time pressure → Reduced event count, escalating complexity
- Resource scarcity → Lower token budgets, limited supplies
- Information fog → Partial state reveals, intelligence gathering
- Ethical dilemmas → Competing success criteria

### Step 4: Scenario Generation

Generate a complete `scenario.json` with training-optimized parameters:

1. **Set Core Parameters**:
   - `number_of_agents`: Based on team roles needed (usually 3-5 for training)
   - `number_of_events`: Shorter for focused training (7-12 typical)
   - `theme`: Operational domain translated to narrative theme
   - `scenario`: Rich description embedding training objectives

2. **Optimize Token Economy**:
   - Adjust budgets to create decision pressure
   - Balance action costs to force prioritization
   - Set complexity mix to match escalation needs

3. **Configure Evolution**:
   - Higher evolution rate for leadership/adaptation focus
   - World persistence to show consequence chains
   - Mechanic learning for realistic opponent adaptation

4. **Enable Logging**: 
   - Always set `store_event_logs: true` for after-action review
   - Use `markdown` format for readable debriefs
   - Set `verbose` detail for training analysis

5. **Add Training Metadata**:
   ```json
   "_training_metadata": {
     "primary_objectives": ["extracted from conditions"],
     "embedded_decision_points": ["key choices"],
     "assessment_opportunities": ["evaluation moments"],
     "debrief_topics": ["discussion points"]
   }
   ```

### Step 5: Output Generation

Save the scenario and provide usage instructions:

```
Training scenario generated successfully!
Saved to: scenarios/[scenario-name].json

Training Profile:
- Primary Objective: [main training goal]
- Operational Context: [domain/theme]
- Team Size: [X] participants
- Duration: [X] events (approximately X decision points)
- Key Challenges: [embedded constraints]

Embedded Training Elements:
- [Decision point 1]: [What it trains]
- [Decision point 2]: [What it trains]
- [Crisis event]: [Adaptability assessment]

To run this training scenario:
1. Execute: Prompt: prompts/generate-adventure.md
2. Select: scenarios/[scenario-name].json
3. Run adventure: Prompt: adventures/[name]/prompts/simulate-adventure.md
4. Review logs: adventures/[name]/logs/event-[X].md

After-Action Review Topics:
- [Suggested debrief point 1]
- [Suggested debrief point 2]
- [Key learning extraction]
```

## Examples

### Example 1: Specific Conditions Provided
```
Conditions: "Medical emergency response in remote area. Limited supplies, 
communication blackout, local population suspicious of outsiders. Team must 
establish trust while managing triage decisions."

Generated Scenario Focus:
- Theme: "Remote Medical Crisis"
- Primary mechanics: Resource management, social influence, time pressure
- Key tensions: Trust-building vs urgency, individual vs collective care
```

### Example 2: Inverse Prompting Result
```
User responses during conversation:
- Primary objective: "Team coordination under stress"
- Context: "Natural disaster aftermath"
- Constraints: "Conflicting priorities from different agencies"

Generated Scenario Focus:
- Theme: "Multi-Agency Disaster Response"  
- Primary mechanics: Communication channels, priority negotiation
- Key tensions: Agency mandates vs ground truth, coordination vs autonomy
```

## Design Principles

1. **Flexibility First**: Accept natural language conditions without rigid structure
2. **Training Value**: Every event should offer learning opportunities
3. **Realistic Pressures**: Use game mechanics to simulate operational constraints
4. **Observable Behaviors**: Create situations that reveal competencies
5. **Meaningful Consequences**: Ensure decisions have traceable impacts

## Validation Checklist

Before finalizing the scenario:
- [ ] Does it address the stated training objectives?
- [ ] Are decision points clear and meaningful?
- [ ] Will the constraints create appropriate pressure?
- [ ] Can performance be assessed through gameplay?
- [ ] Are there natural debrief opportunities?

Remember: The goal is not to create a training simulation, but rather an engaging adventure that happens to generate training-relevant insights through its narrative structure and decision points.