# Intelligent Operations Platform: Core Architecture Concepts

## Deterministic vs. Non-Deterministic Processing

Modern systems require two fundamentally different types of processing capabilities.

**Deterministic Processing** produces predictable, repeatable results from given inputs:
- Mathematical calculations
- Database operations
- State transitions
- Protocol implementations
- Resource allocations

**Non-Deterministic Processing** handles tasks requiring interpretation, creativity, or judgment:
- Natural language understanding
- Pattern recognition in unstructured data
- Strategic decision making
- Creative content generation
- Contextual analysis

These processing types require different approaches to implementation, testing, and deployment. Deterministic processes can be validated through traditional testing methods. Non-deterministic processes require statistical evaluation and continuous monitoring of output quality.

**Critical Design Principle**: Agentic processes consume tokens and computational resources at significant cost. Reserve non-deterministic processing exclusively for tasks that genuinely require intelligence, creativity, or judgment. Implement all predictable behaviors using traditional programming constructs and expose them to agents as MCP tools. This separation dramatically reduces operational costs while improving system reliability and performance.

### Communication Protocols

**Deterministic Systems** use structured protocols:
- **MCP (Model Context Protocol)**: Tool-based interactions with defined schemas
- **gRPC**: High-performance binary protocol for service-to-service communication
- **HTTP/REST**: Standard web APIs for broad compatibility

**Non-Deterministic Systems** use flexible protocols:
- **Agent-to-Agent (A2A)**: Structured message passing between intelligent agents
- **Prompt Chains**: Sequenced operations with context preservation
- **Event Streams**: Asynchronous communication for reactive processing

The separation of these concerns enables appropriate tooling, monitoring, and optimization strategies for each type of processing.

## Architecture Overview

The platform uses goroutine-based sessions to handle three distinct interaction patterns.

### Session Types

**Command Sessions** execute single operations and return results:
```go
type CommandSession struct {
    ID       string
    Request  chan AgentRequest
    Response chan AgentResponse
    Done     chan struct{}
}
```

**Interactive Sessions** maintain stateful connections for ongoing interactions:
```go
type InteractiveSession struct {
    ID          string
    UserID      string
    Input       chan UserInput
    Output      chan AgentOutput
    Control     chan ControlMessage
    State       *SessionState
    LastActive  time.Time
}
```

**Daemon Sessions** run continuously, responding to events and performing scheduled tasks:
```go
type DaemonSession struct {
    ID            string
    Name          string
    Events        chan Event
    Actions       chan Action
    Status        chan StatusUpdate
    Config        *DaemonConfig
    Checkpoints   *CheckpointStore
}
```

### Communication Patterns

Each session type runs in isolated goroutines, communicating through channels:

```go
type MainAgent struct {
    // Incoming channels
    Requests     chan ProcessingRequest
    Events       chan SystemEvent
    
    // Outgoing channels  
    Deterministic   chan DeterministicTask
    NonDeterministic chan IntelligentTask
    
    // Control channels
    Metrics      chan MetricUpdate
    Errors       chan ErrorReport
    Shutdown     chan struct{}
}
```

Task routing leverages appropriate protocols:

```go
func (a *MainAgent) routeTask(task Task) {
    switch task.Type {
    case Deterministic:
        // Route to MCP tools, gRPC services, or HTTP APIs
        a.Deterministic <- task
        
    case NonDeterministic:
        // Route to A2A protocol or intelligent agents
        a.NonDeterministic <- task
    }
}
```

This architecture provides:
- Fault isolation between sessions
- Natural concurrency boundaries
- Clear communication contracts
- Resource management per session type
- Protocol-appropriate routing

## Everything as Code, Binary, and Container

Each platform component exists in three forms to support different deployment scenarios.

### Package Form

Components as importable Go libraries enable direct integration:

```go
import "github.com/org/platform/components/statemanager"

sm := statemanager.New(config)
state, err := sm.Load(eventID)
```

### Binary Form

Standalone executables provide CLI tools and services:

```bash
# CLI usage
$ platform-state-manager get --event-id=12345

# Service mode
$ platform-state-manager serve --port=8080 --storage=postgres
```

### Container Form

Docker images enable cloud-native deployments:

```yaml
services:
  state-manager:
    image: platform/state-manager:v1.0
    ports:
      - "8080:8080"
    environment:
      - STORAGE_BACKEND=postgresql
      - STORAGE_URI=postgresql://db:5432/platform
```

This three-form approach provides:
- Maximum deployment flexibility
- Consistent interfaces across forms
- Progressive adoption paths
- Standard operational patterns

## Provider Abstraction

The platform abstracts external service providers through common interfaces.

### Intelligence Providers

All AI/ML providers implement a unified interface:

```go
type IntelligenceProvider interface {
    Complete(context.Context, CompletionRequest) (CompletionResponse, error)
    Embed(context.Context, EmbeddingRequest) (EmbeddingResponse, error)
    Analyze(context.Context, AnalysisRequest) (AnalysisResponse, error)
}
```

### Storage Providers

Storage systems share common operations:

```go
type StorageProvider interface {
    Save(context.Context, key string, data []byte) error
    Load(context.Context, key string) ([]byte, error)
    Delete(context.Context, key string) error
    List(context.Context, prefix string) ([]string, error)
}
```

### Monitoring Providers

Observability systems use standard interfaces:

```go
type MonitoringProvider interface {
    RecordMetric(context.Context, Metric) error
    StartSpan(context.Context, string) Span
    Log(context.Context, LogEntry) error
}
```

### Configuration Example

Providers are configured declaratively:

```yaml
providers:
  intelligence:
    primary:
      type: openai
      config:
        model: gpt-4
        temperature: 0.7
    fallback:
      type: anthropic
      config:
        model: claude-3
        
  storage:
    primary:
      type: s3
      config:
        bucket: platform-data
        region: us-east-1
        
  monitoring:
    metrics:
      type: prometheus
      config:
        endpoint: http://prometheus:9090
```

This abstraction approach enables:
- Provider switching without code changes
- Multi-provider strategies (primary/fallback)
- Provider-specific optimizations
- Consistent interfaces across provider types

## Agent Lifecycle Management

The platform distinguishes between agents that exist for a single session and those that provide system-wide capabilities.

### Agent Types

**Transient Runtime Agents** are initialized at session start and removed at session end:
```
.claude/agents/runtime/
\u251c\u2500\u2500 character-elena-vasquez.md
\u251c\u2500\u2500 narrative-director.md
\u2514\u2500\u2500 combat-resolver.md
```

**Persistent System Agents** provide always-available capabilities:
```
.claude/agents/
\u251c\u2500\u2500 code-analyzer/
\u251c\u2500\u2500 documentation-writer/
\u2514\u2500\u2500 test-generator/
```

### Hybrid Format Strategy

Agents use different formats for different purposes:

**Persistent Storage Format** (YAML/JSON):
```yaml
# adventures/first-contact/characters/captain-vasquez.yml
id: captain-elena-vasquez
core_identity:
  - Diplomatic military leader
  - Puts crew safety first
current_status:
  health: Healthy
  location: Bridge
evolution_log:
  - event: 1
    change: "Gained confidence in diplomatic leadership"
  - event: 2
    change: "Developed trust in alien communication"
```

**Runtime Agent Format** (Markdown):
```markdown
# Captain Elena Vasquez

You are Captain Elena Vasquez, commanding the Earth Survey Vessel Meridian.

## Core Identity
- Diplomatic military leader who puts crew safety first
- Decisive under pressure with 15 years military experience

## Current Status
- Health: Healthy
- Location: Bridge, coordinating first contact protocols

## Recent Evolution
- Event 1: Gained confidence in diplomatic leadership
- Event 2: Developed trust in alien communication

## Response Guidelines
Maintain military bearing while embracing diplomatic opportunities. 
Balance crew safety with mission objectives.
```

The conversion process preserves all persistent data while adding runtime-specific context and behavioral guidelines.

### State Synchronization

The platform manages bidirectional state flow:

```go
type AgentLifecycle interface {
    // Session start: Load persistent \u2192 Create runtime
    InitializeRuntime(ctx context.Context, persistentPath string) error
    
    // Session active: Track runtime changes
    CaptureEvolution(ctx context.Context, agentID string) Evolution
    
    // Session end: Extract changes \u2192 Update persistent
    SyncToPersistent(ctx context.Context, evolution Evolution) error
    
    // Cleanup: Remove runtime agents
    CleanupRuntime(ctx context.Context, sessionID string) error
}
```

This lifecycle approach provides:
- Efficient resource usage (agents only exist when needed)
- Clean session isolation
- Evolution tracking across sessions
- Data portability between formats

## System Organization Patterns

The platform uses directory conventions to separate concerns and establish clear boundaries.

### Directory Structure

```
project/
\u251c\u2500\u2500 prompts/                    # User-facing interfaces
\u2502   \u251c\u2500\u2500 generate-report.md
\u2502   \u2514\u2500\u2500 analyze-data.md
\u251c\u2500\u2500 prompts/system/            # Internal system operations
\u2502   \u251c\u2500\u2500 convert-format.md
\u2502   \u251c\u2500\u2500 extract-metadata.md
\u2502   \u2514\u2500\u2500 validate-schema.md
\u2514\u2500\u2500 .claude/agents/            # Agent definitions
    \u251c\u2500\u2500 runtime/               # Transient session agents
    \u2502   \u251c\u2500\u2500 character-elena.md
    \u2502   \u2514\u2500\u2500 narrative-director.md
    \u251c\u2500\u2500 code-analyzer/         # Persistent system agent
    \u251c\u2500\u2500 test-generator/        # Persistent system agent
    \u2514\u2500\u2500 doc-writer/           # Persistent system agent
```

### Runtime Agent Management

The `.claude/agents/runtime/` directory provides automatic lifecycle management:

```bash
# Session start: Initialize runtime agents
$ ls .claude/agents/runtime/
character-vasquez.md
character-chen.md
scenario-controller.md

# Session end: Cleanup
$ rm -rf .claude/agents/runtime/*
```

This enables dynamic agent loading per session while keeping system agents always available.

### Separation of Interfaces

**User-Facing Prompts** define external interactions:
- Clear documentation
- Stable interfaces
- Usage examples
- Input validation

**System Prompts** handle internal operations:
- Format conversions
- State extraction
- Utility functions
- Integration logic

### Convention Benefits

This organization pattern enables:
- Clear architectural boundaries
- Discoverability of capabilities
- Separation of public/private interfaces
- Consistent project structure

### Integration Example

```go
type SystemPrompts struct {
    basePath string
}

func (sp *SystemPrompts) Load(name string) (*Prompt, error) {
    // System prompts always in system/ subdirectory
    path := filepath.Join(sp.basePath, "prompts", "system", name+".md")
    return LoadPrompt(path)
}

func (sp *SystemPrompts) ConvertCharacter(char Character) (*Agent, error) {
    prompt := sp.Load("convert-character-to-agent")
    return prompt.Execute(char)
}
```

These patterns establish consistent conventions that scale across projects and teams while maintaining clear separation between user interfaces and system internals.

## Cloud Provider Integration

Enterprise deployments often require processing isolation and data sovereignty controls that cloud provider LLM services enable.

### Processing Isolation

Cloud providers offer abstraction layers that keep data within organizational boundaries:

```go
type CloudLLMProvider interface {
    // Standard provider interface with cloud-specific implementation
    IntelligenceProvider
    
    // Cloud-specific configuration
    ConfigureEndpoint(vpcEndpoint string) error
    SetDataRegion(region string) error
    EnablePrivateLink(enabled bool) error
}
```

### Provider Examples

**AWS Bedrock Integration**:
```yaml
providers:
  bedrock:
    type: aws-bedrock
    config:
      region: us-east-1
      model_id: anthropic.claude-3-opus
      vpc_endpoint: vpce-xxxxxx
      data_residency: us-only
```

**GCP Vertex AI Integration**:
```yaml
providers:
  vertex:
    type: gcp-vertex
    config:
      project: my-project
      location: us-central1
      model: claude-3-opus@001
      private_endpoint: true
```

### Benefits

This approach provides:
- Data processing within organizational cloud boundaries
- Compliance with data residency requirements
- Network isolation through VPC endpoints
- Unified billing and governance
- Audit trails within existing cloud infrastructure

## References

### AI Documentation
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Subagents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Model Context Protocol](https://modelcontextprotocol.io/overview)
- [Agent2Agent](https://github.com/a2aproject/A2A)

### Cloud Documentation
- [Cloud Integration](https://docs.anthropic.com/en/docs/claude-code/third-party-integrations)
- [AWS Bedrock](https://docs.aws.amazon.com/bedrock/)
- [GCP Vertex AI](https://cloud.google.com/vertex-ai/docs)

### Go
- [Go Language](https://go.dev/doc)
- [Effective Go - Concurrency](https://go.dev/doc/effective_go#concurrency)
- [Go By Example](https://gobyexample.com)

### Protocol Documentation
- [gRPC Documentation](https://grpc.io/docs/)
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [WebSocket Protocol RFC 6455](https://datatracker.ietf.org/doc/html/rfc6455)

### Container and Orchestration
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Open Container Initiative](https://opencontainers.org/release-notices/overview/)

### Observability Standards
- [OpenTelemetry Documentation](https://opentelemetry.io/docs/)
- [Prometheus Documentation](https://prometheus.io/docs/)