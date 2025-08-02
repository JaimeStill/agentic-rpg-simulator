# Simulate Adventure: First Contact Crisis

Continue or start the adventure simulation from the current state.

## Instructions
1. **Character Subagent Setup**: Convert character profiles to runtime subagents
   - Run: `Prompt: prompts/system/convert-character-to-subagent.md`
   - For each character in ../characters/
   - Deploy to .claude/agents/runtime/scifi-first-contact-20250801/
2. **Check Event State**: Check for existing event states in ../events/
3. **Initialize or Continue**: If no states exist, initialize Event 1; if states exist, continue from latest
4. **Process Event**: Execute event according to engine rules with character subagent participation
5. **Character Evolution**: Extract character growth from subagent responses
   - Run: `Prompt: prompts/system/extract-character-evolution.md`
   - Update character profiles in ../characters/
6. **Save State**: Save new state to ../events/event-[X]-state.yml
7. **Create Transcript**: Create full event transcript in ../logs/event-[X].md (logging enabled)

## Adventure Context
Theme: Sci-Fi
Scenario: First Contact Crisis - During routine deep space survey, the crew encounters an alien vessel. A translation error during first contact is interpreted as a declaration of war. Now both species mobilize fleets while the crew races to prevent catastrophe and uncover who benefits from conflict.
Current Event: [determined from state]

## Output Format
Each event should include:
- Event title and token budget
- Event setup with stakes
- Character actions phase (invoke character subagents by name for authentic responses)
- Mechanic resolution phase
- Evolution phase (character and world changes)
- Character growth extraction (run evolution extraction on subagent responses)
- Event summary
- Save compressed state (events/) and full transcript (logs/)

## Character Subagent Integration
During character action phases:
1. **Invoke by Name**: Call character subagents directly (e.g., "character-elena-vasquez")
2. **Authentic Responses**: Subagents will respond in character with appropriate actions
3. **Track Evolution**: Monitor character responses for growth, relationship changes, goal shifts
4. **Extract Changes**: Use evolution extraction to capture character development
5. **Update Profiles**: Apply extracted evolution to persistent YAML character profiles

## Logging Configuration
- Format: Markdown (.md)
- Detail Level: Standard (complete event transcript with character actions and mechanics)
- Location: ../logs/event-[X].md