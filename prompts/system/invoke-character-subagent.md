# Invoke Character Subagent

Execute character actions during adventure events through authentic subagent invocation.

## Execution Instructions

1. **Prepare Character Context**: Set up the specific situation and stakes for the character
2. **Invoke Character Subagent**: Use Task tool to call the character's dedicated subagent
3. **Capture Authentic Response**: Receive and process the character's authentic response
4. **Return Character Action**: Provide the response for integration into event mechanics

## Usage Protocol

This prompt is called during adventure event processing to get authentic character responses. It should be invoked once per character during the character action phase of each event.

### Input Parameters
- **Character Name**: The specific character to invoke (e.g., "Kavitha Subramanian")
- **Character Subagent ID**: The subagent identifier (e.g., "character-kavitha-subramanian")
- **Event Context**: Current event situation, stakes, and environment
- **Character Situation**: Specific circumstances affecting this character
- **Available Actions**: What the character can potentially do in this situation
- **Token Budget**: Allocated tokens for this character's response

## Subagent Invocation Process

### Step 1: Context Preparation
Prepare the complete context for the character subagent:
```
Character: [Character Name]
Situation: [Specific character situation]
Event Context: [Current event circumstances]
Stakes: [What's at risk for this character]
Available Actions: [Potential responses the character can take]
Token Allocation: [Character's portion of event token budget]
```

### Step 2: Subagent Invocation
Use the Task tool to invoke the character subagent with the prepared context:
```
Task: [character-subagent-id]
Description: "Character action response during adventure event"
Prompt: "You are [Character Name] in the following situation: [context]

Current circumstances: [event context]
Your specific situation: [character situation]  
What's at stake: [stakes for character]

Respond as this character would, considering your personality, goals, relationships, and current state. Choose your action and explain your reasoning. Stay true to your character while advancing the story."
```

### Step 3: Response Processing
Capture the authentic character response from the subagent and format it for event integration:

**Response Structure:**
- **Character Action**: What the character decides to do
- **Character Reasoning**: Why they chose this action (internal motivation)
- **Character Dialogue**: Any spoken words or communication
- **Character Evolution Indicators**: Signs of character growth or change
- **Relationship Dynamics**: How this affects relationships with other characters

### Step 4: Integration Output
Return the formatted character response for integration into the event processing:

```yaml
character_name: "[Character Name]"
character_action: "[Character's chosen action]"
character_reasoning: "[Internal motivation and decision process]"
character_dialogue: "[Any spoken words or communication]"
evolution_indicators:
  - "[Signs of character growth or change]"
relationship_effects:
  - character: "[Other Character Name]"
    effect: "[How this action affects the relationship]"
token_usage: "[Tokens used by this character response]"
```

## Error Handling

### Subagent Not Found
If the character subagent doesn't exist in `.claude/agents/runtime/[adventure-name]/`:
1. Extract adventure name from character file path or current working directory
2. Check if the character profile exists in `../characters/`
3. If profile exists, convert it to runtime subagent using `convert-character-to-subagent.md`
4. Retry subagent invocation
5. If conversion fails, provide fallback character response based on JSON profile

**Adventure Name Extraction**: Determine adventure name from character file paths like `adventures/[adventure-name]/characters/character-[name-slug].json` or from current adventure context.

### Subagent Response Issues
If subagent provides inconsistent or problematic response:
1. Validate response against character's core identity
2. Check for evolution triggers that might explain behavior changes
3. If response is out of character, request clarification from subagent
4. Document any concerns for evolution processing

### Token Budget Overrun
If character response exceeds allocated token budget:
1. Request more concise response from subagent
2. Preserve core character action and reasoning
3. Truncate less essential elements if necessary
4. Report token usage for event budget management

## Integration Notes

This prompt is designed to be called multiple times during an event - once for each character. The responses should be collected and integrated into the event's character action phase before proceeding to mechanic resolution.

Character responses can influence:
- Event outcome mechanics
- Character evolution tracking
- Relationship dynamics
- World state changes
- Next event setup

The authentic character responses from subagents are essential for maintaining character consistency and enabling meaningful character development throughout the adventure.