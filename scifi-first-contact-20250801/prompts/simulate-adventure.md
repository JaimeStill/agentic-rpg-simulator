# Simulate Adventure: First Contact Crisis

Continue or start the adventure simulation from the current state.

## Instructions
1. Check for existing event states in ../events/
2. If no states exist, initialize Event 1
3. If states exist, continue from the latest event
4. Process the event according to engine rules
5. Save the new state to ../events/event-[X]-state.yml
6. Create full event transcript in ../logs/event-[X].md (logging enabled in scenario config)

## Adventure Context
Theme: Sci-Fi
Scenario: First Contact Crisis - During routine deep space survey, the crew encounters an alien vessel. A translation error during first contact is interpreted as a declaration of war. Now both species mobilize fleets while the crew races to prevent catastrophe and uncover who benefits from conflict.
Current Event: [determined from state]

## Output Format
Each event should include:
- Event title and token budget
- Event setup with stakes
- Character actions phase (150 tokens per character)
- Mechanic resolution phase
- Evolution phase (character and world changes)
- Event summary
- Save compressed state (events/) and full transcript (logs/)

## Logging Configuration
- Format: Markdown (.md)
- Detail Level: Standard (complete event transcript with character actions and mechanics)
- Location: ../logs/event-[X].md