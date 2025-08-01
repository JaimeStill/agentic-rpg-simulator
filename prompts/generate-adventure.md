# Generate Adventure

Initialize a new RPG adventure by creating all necessary artifacts and directory structure.

## Execution Instructions

1. **Load Scenario**: Determine scenario source:
   - If scenario file explicitly specified, load that file
   - If scenario data provided with prompt, use that data
   - Otherwise, list available scenarios from `scenarios/` directory:
     ```
     Available scenarios:
     1. cyberpunk-neural-heist
     2. fantasy-awakened-peasant
     3. mystery-mansion-murders
     4. postapoc-water-wars
     5. scifi-first-contact
     6. superhero-reality-crisis
     7. custom (create new scenario)
     ```
   - If user selects "custom", invoke `generate-scenario.md`
   - Validate all required scenario elements are present

2. **Create Adventure Directory**: Generate a unique adventure name based on theme and scenario
   - Format: `[theme]-[descriptor]-[timestamp]` (e.g., `fantasy-tomb-20250801`)
   - Create directory structure:
     ```
     [adventure-name]/
     ├── characters/
     ├── events/
     ├── logs/ (only if store_event_logs: true in scenario)
     ├── prompts/
     └── scenario.yml (copy of scenario configuration)
     ```

3. **Generate Character Profiles**: Based on `number_of_agents` from scenario
   - Create character profiles in `[adventure]/characters/`
   - Each character should have:
     - Unique name fitting the theme
     - Core identity traits
     - Starting equipment/abilities
     - Initial relationships with other characters
     - Personal goals aligned with scenario

4. **Create Adventure-Specific Prompts**: Generate the following in `[adventure]/prompts/`:
   
   ### simulate-adventure.md
   ```markdown
   # Simulate Adventure: [Adventure Name]
   
   Continue or start the adventure simulation from the current state.
   
   ## Instructions
   1. Check for existing event states in ../events/
   2. If no states exist, initialize Event 1
   3. If states exist, continue from the latest event
   4. Process the event according to engine rules
   5. Save the new state to ../events/event-[X]-state.yml
   6. Create full event transcript in ../logs/event-[X].[format] (if store_event_logs enabled)
   
   ## Adventure Context
   Theme: [theme]
   Scenario: [scenario]
   Current Event: [determined from state]
   
   ## Output Format
   Each event should include:
   - Event title and token budget
   - Event setup with stakes
   - Character actions phase (150 tokens per character)
   - Mechanic resolution phase
   - Evolution phase (character and world changes)
   - Event summary
   - Save compressed state (events/) and full transcript (logs/) if logging enabled
   ```
   
   ### summarize-adventure.md
   ```markdown
   # Summarize Adventure: [Adventure Name]
   
   Provide a concise summary of the adventure's progress.
   
   ## Instructions
   1. Read all event states in ../events/
   2. Extract key story beats and character developments
   3. Present a chronological summary
   4. Include current status of all characters
   5. Highlight major achievements and setbacks
   ```
   
   ### narrate-adventure.md
   ```markdown
   # Narrate Adventure: [Adventure Name]
   
   Transform the adventure events into a compelling narrative.
   
   ## Instructions
   1. Read all event states in ../events/
   2. Expand compressed states into rich prose
   3. Add sensory details and emotional depth
   4. Maintain consistent voice and tone
   5. Create chapter breaks at major story beats
   ```

5. **Initialize First State**: Create `event-0-state.yml` representing pre-adventure state
   ```yaml
   event_number: 0
   world_state:
     location: [Starting location based on scenario]
     active_elements: [Initial hooks and opportunities]
     resources: [Starting equipment and allies]
   
   character_states: [Generated from character profiles]
   
   action_log: []
   
   next_event_setup:
     trigger: [What starts the adventure]
     stakes: [Initial stakes from scenario]
     complexity: low
   ```

6. **Generate README**: Create `[adventure]/README.md` with:
   - Adventure name and creation date
   - Theme and scenario description
   - Character roster with brief descriptions
   - Quick start instructions
   - Current status (initialized)

## Output Format

After successful generation:
```
Adventure "[name]" initialized successfully!

Location: ./[adventure-name]/
Characters: [List character names]
Theme: [theme]
Scenario: [scenario]

To begin the adventure, run:
Prompt: [adventure-name]/prompts/simulate-adventure.md
```

## Error Handling

- If scenario configuration is invalid, provide specific error messages
- If directory already exists, append a unique suffix
- Validate all files were created successfully before confirming completion