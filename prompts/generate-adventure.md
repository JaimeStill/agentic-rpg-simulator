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
     adventures/[adventure-name]/
     ├── characters/
     ├── events/
     ├── logs/ (only if store_event_logs: true in scenario)
     ├── prompts/
     └── scenario.json (copy of scenario configuration)
     ```

## CRITICAL: File Path Requirements

**IMPORTANT**: ALL files created during adventure generation MUST be placed within the adventure directory structure. NEVER create files at the project root or any other location.

### Correct File Paths (ALWAYS USE FULL PATHS):
- Character profiles: `adventures/[adventure-name]/characters/character-[name-slug].json`
- Event states: `adventures/[adventure-name]/events/event-[X]-state.json`
- Prompts: `adventures/[adventure-name]/prompts/[prompt-name].md`
- Logs: `adventures/[adventure-name]/logs/event-[X].md`
- Scenario copy: `adventures/[adventure-name]/scenario.json`

### Common Mistakes to AVOID:
- ❌ Creating files at root: `character-john-doe.json`
- ❌ Using relative paths: `characters/character-john-doe.json`
- ❌ Forgetting adventure name: `adventures/characters/character-john-doe.json`
- ✅ CORRECT: `adventures/fantasy-quest-20250801/characters/character-john-doe.json`

### When Using Task Tool:
- ALWAYS provide complete file paths in your prompt
- EXPLICITLY state the full directory path for file creation
- VERIFY file locations after Task completion
- Consider using direct Write tool for critical file placement

3. **Generate Character Profiles**: Based on `number_of_agents` from scenario
   - Create character profiles in `adventures/[adventure]/characters/`
   - **File Naming Convention**: `character-[name-slug].json` where name-slug is derived from character's full name
   - **Character ID Generation**: Character ID should match filename (e.g., `character-elena-vasquez`)
   - Each character should have:
     - Unique name fitting the theme (avoid common names like Maya, Chen, Elena, Marcus)
     - Core identity traits
     - Starting equipment/abilities
     - Initial relationships with other characters
     - Personal goals aligned with scenario
   - **Name Slug Rules**:
     - Convert full name to lowercase with hyphens
     - Remove titles/prefixes unless part of identity (Captain → skip, Dr. → skip)
     - Example: "Captain Elena Vasquez" → slug: "elena-vasquez" → file: "character-elena-vasquez.json"

4. **Create Adventure-Specific Prompts**: Generate the following in `adventures/[adventure]/prompts/`:
   
   ### simulate-adventure.md
   ```markdown
   # Simulate Adventure: [Adventure Name]
   
   Execute the complete adventure simulation workflow automatically.
   
   ## Adventure Context
   **Theme:** [theme]  
   **Scenario:** [scenario]
   
   ## Automated Execution Workflow
   
   I will now execute the complete adventure simulation process:
   
   ### Phase 1: Character Subagent Setup
   Converting character profiles to runtime subagents for authentic character behavior during events.
   
   **Converting Character Profiles:**
   - Reading JSON character profiles from ../characters/
   - Generating runtime subagents in .claude/agents/runtime/[adventure-name]/
   - Characters will be available for invocation during event processing
   
   ### Phase 2: Event State Detection and Initialization
   Checking current adventure state and determining next event to process.
   
   **Event State Analysis:**
   - Scanning ../events/ directory for existing event states
   - Determining current event number and adventure progress
   - Loading latest world state and character conditions
   - Initializing next event based on current state
   
   ### Phase 3: Event Processing with Character Subagent Participation
   Executing the next adventure event with authentic character responses through dedicated subagents.
   
   **Event Structure:**
   - **Event Setup**: Describe situation, stakes, and context within token budget
   - **Character Actions**: Invoke each character subagent to get authentic responses to the situation
   - **Mechanic Resolution**: Process character actions through appropriate game mechanics
   - **World Impact**: Determine consequences and changes to adventure state
   
   **Character Subagent Invocation Protocol:**
   During character action phases, I will use the Task tool to invoke each character subagent by name.
   Each subagent will respond authentically based on their personality, goals, and current situation.
   
   ### Phase 4: Character Evolution Processing
   Automatically extracting character growth from subagent responses and updating persistent profiles.
   
   **Evolution Extraction Process:**
   - Analyzing subagent responses for character development indicators
   - Identifying relationship changes, goal evolution, and tactical adaptations
   - Extracting specific character growth elements
   - Updating persistent JSON character profiles in ../characters/
   - Refreshing runtime subagents with evolved character state
   
   ### Phase 5: State Persistence and Logging
   Saving complete adventure state and creating detailed event transcript.
   
   **State Management:**
   - Saving updated event state to ../events/event-[X]-state.json
   - Creating detailed event transcript in ../logs/event-[X].[format]
   - Preparing next event setup for adventure continuation
   
   ## Execution Begins Now
   
   I am now executing this complete workflow automatically. The adventure will process the next event with full character subagent participation, evolution tracking, and state persistence.
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

5. **Initialize First State**: Create `event-0-state.json` representing pre-adventure state
   ```json
   {
     "event_number": 0,
     "world_state": {
       "location": "[Starting location based on scenario]",
       "active_elements": ["Initial hooks and opportunities"],
       "resources": ["Starting equipment and allies"]
     },
     "character_states": "[Generated from character profiles]",
     "action_log": [],
     "next_event_setup": {
       "trigger": "[What starts the adventure]",
       "stakes": "[Initial stakes from scenario]",
       "complexity": "low"
     }
   }
   ```

6. **Generate README**: Create `adventures/[adventure]/README.md` with:
   - Adventure name and creation date
   - Theme and scenario description
   - Character roster with brief descriptions
   - Quick start instructions
   - Current status (initialized)

## Output Format

After successful generation:
```
Adventure "[name]" initialized successfully!

Location: ./adventures/[adventure-name]/
Characters: [List character names]
Theme: [theme]
Scenario: [scenario]

To begin the adventure, run:
Prompt: adventures/[adventure-name]/prompts/simulate-adventure.md
```

## Error Handling

- If scenario configuration is invalid, provide specific error messages
- If directory already exists, append a unique suffix
- Validate all files were created successfully before confirming completion