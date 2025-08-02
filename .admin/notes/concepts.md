# Concepts

Captures ideas that prove particularly insightful or compelling.

## Transient Runtime Agents vs. Persistent System Agents

Subagents can be organized in `.claude/agents` or `~/.claude/agents` in subdirectories.

Given this distinction, we can support the notion of transient runtime agents: agents that are initialized into the subagent system at startup, operate for the duration of the session, and are removed when the session ends.

These subagents can be stored in a `runtime/` sub-directory that facilitates easy startup and cleanup.

Persistent system agents are those that have a strictly defined profile that is rarely updated and are always available.

  ### Subagent Context Persistence

  The more I think about it, the more you may be right to keep the persistent 
  character profiles in a non-markdown format. This way, whenever this platform 
  evolves, the state persistence format is already portable and easily integrated 
  into a persistent storage mechanism (i.e. - SQLite).

● You make an excellent point about data portability and future platform evolution.
   Let me revise the approach:

  Hybrid Format Strategy:
  - Persistent Storage: Keep adventures/[name]/characters/[name].yml in YAML format
   for portability and database integration
  - Runtime Subagents: Generate .claude/agents/runtime/character-[name].md in
  markdown subagent format for active use

  State Synchronization Flow:
  1. Adventure Start: Convert YAML profiles → Generate markdown subagents in
  .claude/agents/runtime/
  2. Event Processing: Invoke character subagents directly for authentic behavior
  3. Event End: Extract character evolution from subagent responses → Update YAML
  profiles

  This provides:
  - Data Portability: YAML format ready for database storage, API integration, or
  platform migration
  - Subagent Functionality: Native Claude Code subagent support during runtime
  - Clean Separation: Persistent data layer independent from runtime execution
  layer

  Would you like me to proceed with this hybrid approach? I can:
  1. Keep the existing YAML character schema
  2. Create a conversion system that generates subagents from YAML profiles
  3. Build state extraction to capture subagent evolution back to YAML format

  This maintains all the benefits of both approaches while future-proofing the
  persistent data layer.

## System Prompts

Should these system prompts be embedded in a prompts/system/ subdirectory ?

● Yes, that's an excellent organizational idea. These are system/utility prompts
  rather than user-facing adventure prompts. Let me reorganize them:

● Bash(mkdir -p /home/jaime/research/agentic-rpg-simulator/prompts/system)
  ⎿  (No content)

● Bash(mv /home/jaime/research/agentic-rpg-simulator/prompts/convert-character-to-s
      ubagent.md /home/jaime/research/agentic-rpg-simulator/prompts/system/ && mv
      /home/ja…)
  ⎿  (No content)

● This creates a cleaner organization:

  prompts/
  ├── generate-adventure.md        # User-facing adventure creation
  ├── generate-scenario.md         # User-facing scenario creation
  └── system/                      # System/utility prompts
      ├── convert-character-to-subagent.md
      └── extract-character-evolution.md

  The prompts/system/ directory will contain all the internal system prompts used
  for:
  - Character management and conversion
  - State synchronization
  - Evolution tracking
  - Other utility functions

  While the main prompts/ directory contains user-facing prompts for creating and
  managing adventures.