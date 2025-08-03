# Simulate Adventure: Operation Underground Extraction

Execute the complete adventure simulation workflow automatically.

## Adventure Context
**Theme:** Special Operations Hostage Rescue  
**Scenario:** Elite special forces team DELTA-7 must infiltrate cartel-controlled underground tunnel networks near Juarez to rescue multiple groups of hostages held in fortified prison cells. Intelligence indicates a narrow window before the hostages are moved deeper into Mexico. The labyrinthine tunnels are rigged with alarms, the cartel has superior numbers, and any mistake could trigger an international incident. Success requires precise coordination, resource management, and split-second tactical decisions.

## Automated Execution Workflow

I will now execute the complete adventure simulation process:

### Phase 1: Character Subagent Setup
Converting character profiles to runtime subagents for authentic character behavior during events.

**Converting Character Profiles:**
- Reading JSON character profiles from ../characters/
- Generating runtime subagents in .claude/agents/runtime/operation-underground-20250803/
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
- Creating detailed event transcript in ../logs/event-[X].md
- Preparing next event setup for adventure continuation

## Execution Begins Now

I am now executing this complete workflow automatically. The adventure will process the next event with full character subagent participation, evolution tracking, and state persistence.