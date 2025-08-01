# Plans

These are ideas that I want to flesh out at a later point.

## Human Interaction

Extend the engine to support human involvement. It should be extended in a way that preserves the ability for the engine to run autonomously based on the parameters configuration.

## Mechanics MCP Server

Engine mechanics that are deteriministic and have set behaviors should be implemented with MCP tools rather than subagent processing. This way, we optimize token consumption and processing time. Write the mechanics MCP server in Go.

## Derived Scenarios

There should be a prompt that allows a scenario to be spawned from an existing scenario as:
- a side adventure
- a backstory
- the next arc once the scenario concludes