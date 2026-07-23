<img src="img/SAPCloudALM.png" width="10%">

# Building SAP Cloud ALM Extensions with AI 
**Target Audience**: SAP Cloud ALM Customers  
**Purpose**: Learn how to create AI-powered extensions (skills, agents, MCP servers) using SAP Cloud ALM APIs


---

## Table of Contents

1. [Overview](#overview)
   - [What You Can Build](#what-you-can-build)
   - [Key Use Cases](#key-use-cases)

2. [Understanding AI: Tools, Models, and Concepts](#understanding-ai-tools-models-and-concepts)
   - [The AI Landscape: Available Tools](#the-ai-landscape-available-tools)
     - [Claude (by Anthropic)](#claude-by-anthropic)
     - [GPT-4 / ChatGPT (by OpenAI)](#gpt-4--chatgpt-by-openai)
     - [Cline (VS Code Extension)](#cline-vs-code-extension)
   - [Model Selection Guide](#model-selection-guide)
   - [Core AI Concepts: Skills, Agents, and MCP Servers](#core-ai-concepts-skills-agents-and-mcp-servers)
     - [What Are Skills?](#what-are-skills)
     - [What Are Agents?](#what-are-agents)
     - [What Are MCP Servers?](#what-are-mcp-servers)
     - [Skills vs Agents vs MCP Servers: Quick Comparison](#skills-vs-agents-vs-mcp-servers-quick-comparison)
   - [The "Vibe Coding" Approach](#the-vibe-coding-approach)

3. [Implementation Paths](#implementation-paths)
   - [Path 1: Direct API Integration (Simplest)](#path-1-direct-api-integration-simplest)
   - [Path 2: AI with Tool Calling (Recommended)](#path-2-ai-with-tool-calling-recommended)
   - [Path 3: Build MCP Server (Advanced)](#path-3-build-mcp-server-advanced)
   - [Path 4: Agent Definition Files (Declarative)](#path-4-agent-definition-files-declarative)

4. [Choosing the Right Path](#choosing-the-right-path)

5. [Key SAP Cloud ALM APIs](#key-sap-cloud-alm-apis)
   - [Task Management API (CALM_TKM)](#task-management-api-calm_tkm)
   - [Project Management API (CALM_PJM)](#project-management-api-calm_pjm)

6. [Best Practices](#best-practices)
   - [Authentication & Security](#1-authentication--security)
   - [Error Handling](#2-error-handling)
   - [AI Prompt Design](#3-ai-prompt-design)

7. [Resources](#resources)
   - [Documentation](#documentation)
   - [Reference Implementations](#reference-implementations)

8. [Next Steps](#next-steps)

---

## Overview

This guide shows you how to extend SAP Cloud ALM with AI capabilities by building custom skills, agents, and MCP (Model Context Protocol) servers that integrate with SAP Cloud ALM APIs.
<img src="img/SCALM.png" width="70%">

### What You Can Build

- **Custom Skills**: Specialized AI assistants that handle specific SAP Cloud ALM workflows
- **AI Agents**: Autonomous agents that can orchestrate complex multi-step tasks
- **MCP Servers**: Tool servers that expose SAP Cloud ALM APIs to AI models
- **Conversational Interfaces**: Natural language interfaces to your SAP Cloud ALM data

### Key Use Cases

1. **Task Automation**: "Create tasks for all open requirements in project X"
2. **Intelligent Querying**: "Show me all critical defects assigned to my team"
3. **Workflow Orchestration**: "Generate test cases from requirements and assign to testers"
4. **Analytics & Insights**: "Summarize project health across all active implementations"

---

## Understanding AI: Tools, Models, and Concepts

### The AI Landscape: Available Tools

When building AI-powered extensions, you have multiple AI models and development tools to choose from. It's important to understand the difference between:

- **AI Models** - The underlying language models (Claude, GPT-4, etc.) that power the intelligence
- **Development Tools** - IDEs and extensions that help you build with AI (Cline, Cursor, GitHub Copilot, etc.)

---

## **AI Models** (The Intelligence) 🧠

These are the underlying language models you'll use in your applications:

### **Claude (by Anthropic)** <img src="img/claude-icon-logo.png" width="30">

**What Is Claude:**
Claude is a family of AI language models accessed via API or web interface. This is the "brain" that powers your AI application.

**Access Methods:**
- **Claude API** - Direct API integration (api.anthropic.com)
- **Claude.ai** - Web interface for testing and prototyping
- **AWS Bedrock** - Claude hosted on AWS infrastructure

**Models Available:**
- **Claude Opus 4.8**<sup>[[2]](#references)</sup> - Most capable model for the most complex reasoning and analysis tasks
- **Claude Sonnet 4.6**<sup>[[2]](#references)</sup> - Excellent balance of capability and speed, ideal for most production workloads including complex reasoning and multi-step orchestration
- **Claude Sonnet 4.5**<sup>[[2]](#references)</sup> - Balanced performance and cost
- **Claude Haiku 4.5**<sup>[[2]](#references)</sup> - Fast, cost-effective model for simple, repetitive tasks

**Best For:** 
- Building MCP servers with tool calling
- Complex code generation and refactoring
- Multi-step workflow orchestration
- Precise instruction following

---

### **GPT-4 / ChatGPT (by OpenAI)** <img src="img/openAI-logo.png" width="30">

**What Is GPT-4:**
OpenAI's language model, accessed via API or ChatGPT interface<sup>[[4]](#references)</sup>.

**Access Methods:**
- **OpenAI API** - Direct API integration<sup>[[4]](#references)</sup>
- **ChatGPT Plus** - Web interface with GPT-4 access
- **Azure OpenAI Service** - Enterprise hosting on Azure<sup>[[5]](#references)</sup>

**Models Available:**
- **GPT-4o**<sup>[[4]](#references)</sup> - Multimodal model with strong reasoning capabilities
- **GPT-4o mini** - Faster, more economical variant for everyday tasks
- **o1** - Advanced reasoning model for complex problem-solving

**Best For:**
- General automation and scripting
- Conversational interfaces and chatbots
- Quick prototyping and brainstorming
- Content generation

---

### **Other AI Models**

- **Gemini (by Google)** - Google's multimodal AI, good for mixed text/image workflows
- **LLaMA (by Meta)** - Open-source models you can self-host
- **Mistral** - European AI provider with strong code capabilities
- **Amazon Bedrock** - Access to multiple models (Claude, Llama, etc.) via AWS

---

## **Development Tools** (Where You Build) ⚒️

These tools help you build, test, and iterate on your AI-powered applications:

### **Cline (VS Code Extension)** <img src="img/Cline-logo.png" width="30">

**What Is Cline:** 
Cline (formerly Claude Dev) is an **IDE extension** that brings AI capabilities directly into Visual Studio Code<sup>[[8]](#references)</sup>. 
It's a **tool** that **uses** Claude (or other models) to help you code.

**What Cline Does:**
- Read and write files in your project
- Execute terminal commands
- Run tests and check output
- Create/modify/delete files based on your requests
- Iterate on code based on test failures<sup>[[8]](#references)</sup>

**Best For:**
- **Vibe coding** - Build features by describing them in natural language
- In-IDE code assistance
- Refactoring and code review
- Learning and prototyping
- **Building MCP servers** through conversation



---

### **Cursor** <img src="img/Cursor-logo.png" width="30">

**What Is Cursor:**
An AI-first code editor (fork of VS Code) with native AI integration<sup>[[9]](#references)</sup>.

**Key Features:**
- AI chat built into the editor
- Multi-file editing with AI
- Codebase-aware suggestions
- Uses GPT-4, Claude, or other models<sup>[[9]](#references)</sup>
- Autonomous task execution ("agentic development")<sup>[[9]](#references)</sup>

**Best For:**
- Teams wanting an AI-native editor
- Multi-file refactoring
- Conversational coding experience
- Enterprise adoption (trusted by Fortune 500 companies)<sup>[[9]](#references)</sup>


---

### **GitHub Copilot** <img src="img/Github-logo.png" width="30">

**What Is Copilot:**
AI pair programmer integrated into multiple IDEs (VS Code, JetBrains, Neovim)<sup>[[10]](#references)</sup>.

**Key Features:**
- Line-by-line code suggestions
- Autocomplete powered by AI
- Chat interface for questions
- Code agents for autonomous task execution<sup>[[10]](#references)</sup>
- Multi-platform support (IDE, CLI, Mobile)<sup>[[10]](#references)</sup>

**Best For:**
- Real-time code completion
- Boilerplate generation
- Quick function implementations




## **Which Tool Should You Use?**

### **Recommended Stack for This Guide:**

> **Note**: These recommendations are based on general patterns for SAP Cloud ALM API integrations and may vary based on your specific requirements, budget, and compliance needs. Always evaluate models for your particular use case.

**For Development:**
- **IDE Tool**: Cline/Claude (VS Code) or Cursor
- **AI Model**: Claude Sonnet 4.6 (excellent tool calling capabilities<sup>[[1]](#references)</sup>, large context window<sup>[[2]](#references)</sup>)

**For Production:**
- **AI Model**: Claude Sonnet 4.6 or Claude Haiku 4.5 via API (depending on complexity)
- **Deployment**: Your choice of cloud platform
- **Optional**: MCP server for tool centralization

---

### Model Selection Guide

| Use Case | Recommended Model | Why |
|----------|------------------|-----|
| **Complex SAP Cloud ALM workflows** | Claude Sonnet 4.6<sup>[[2]](#references)</sup> | Strong tool use capabilities<sup>[[1]](#references)</sup>, multi-step reasoning, large context window |
| **Production task automation** | Claude Sonnet 4.6<sup>[[2]](#references)</sup> | Best balance of intelligence and speed |
| **High-volume simple queries** | Claude Haiku 4.5<sup>[[2]](#references)</sup> | Fast and cost-effective |
| **Most complex reasoning tasks** | Claude Opus 4.8<sup>[[2]](#references)</sup> | Highest capability for complex reasoning |
| **Prototyping & learning** | GPT-4o via ChatGPT or API / Claude via Cline | Quick iteration, broad community resources |
| **Enterprise compliance** | Azure OpenAI (GPT-4o) | Security, SLAs, data residency guarantees |
| **Interactive development** | Cline + Claude | IDE integration, context awareness |

---

### References

<a name="references"></a>

**Claude (Anthropic)**:
1. **[Anthropic Tool Use Documentation](https://docs.anthropic.com/en/docs/build-with-claude/tool-use)** - Official guide on Claude's tool calling capabilities
2. **[Anthropic Models Overview](https://docs.anthropic.com/en/docs/about-claude/models)** - Official model specifications, capabilities, and pricing
3. **[Anthropic Pricing](https://www.anthropic.com/pricing)** - Current API pricing and plans

**GPT / OpenAI**:

4. **[OpenAI Platform Documentation](https://platform.openai.com/docs)** - Official OpenAI API and model documentation
5. **[Azure OpenAI Service](https://azure.microsoft.com/en-us/products/ai-services/openai-service)** - Microsoft Azure's OpenAI hosting
6. **[OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)** - Guide on function calling with GPT models
7. **[OpenAI Pricing](https://openai.com/api/pricing)** - Current API pricing for GPT models

**Development Tools**:

8. **[Cline GitHub Repository](https://github.com/cline/cline)** - Official Cline (Claude Dev) VS Code extension source and documentation
9. **[Cursor IDE](https://www.cursor.com)** - Official Cursor AI-powered code editor website
10. **[GitHub Copilot](https://github.com/features/copilot)** - Official GitHub Copilot features and pricing

**Additional Resources**:
- [Claude API Documentation](https://docs.anthropic.com) - Complete API reference
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io) - MCP specification
- [SAP Cloud ALM API Hub](https://hub.sap.com) - SAP API documentation

---

### Core AI Concepts: Skills, Agents, and MCP Servers

Understanding these three concepts is key to building AI-powered SAP Cloud ALM extensions:

#### **What Are Skills? ⚒️**
**Definition:** A skill is a packaged set of instructions and capabilities that an AI model loads on demand, defined in a markdown file. It provides behavior templates and procedures for a specific domain or task area.

**Think of it as:** A specialist's handbook (e.g., "Task Manager Procedures", "Requirement Analysis Guidelines") that the AI consults when needed

**Key Point:** Skills are **passive templates** — they define HOW to behave, but don't act autonomously. They must be invoked by an agent or application.

**Structure:**
```markdown
---
name: task-skill
description: Manages SAP Cloud ALM tasks
tools:
  - List-Tasks
  - Create-Task
---

# System Instructions
You are a task management specialist...
```

**Key Characteristics:**
- **Procedures (SKILL.md)** - defined in markdown files as instructions and workflows
- **Reusability** - same skill can be used by multiple applications and contexts
- **Token-efficient** - loaded only when needed, doesn't bloat main context
- **Specialization** - focused on one area (tasks, projects, requirements)

**Example Skills:**
- `project-task-skill` - Creates and manages tasks
- `requirement-skill` - Handles requirement creation and approval workflows
- `defect-triage-skill` - Analyzes and prioritizes defects

**When to Create a Skill:**
- You have a recurring workflow (e.g., "weekly task summaries")
- You want consistent behavior across multiple users/apps
- You need version-controlled AI behavior

---

#### **What Are Agents? 🤖**
**Definition:** An autonomous AI entity that can plan, execute multi-step tasks, use tools, and make decisions to achieve a goal.

**Think of it as:** A self-directed worker who can break down complex requests and execute them independently

**Difference from Skills:**
- **Skills** = behavior templates (passive, need to be invoked)
- **Agents** = active executors (can run autonomously, make decisions)

**Key Characteristics:**
- **Reasoning** - can plan and execute without constant human input
- **Planning** - breaks complex tasks into sub-tasks
- **Agentic Loop** - calls APIs and functions to get things done
- **Delegation** - can delegate subtasks to other agents or skills

**Example Agent Workflows:**
```
User: "Prepare project X for release"

Agent thinks:
1. List all open tasks → [finds 15 tasks]
2. Check which are critical → [identifies 3 blockers]
3. Assign tasks to team members → [assigns based on workload]
4. Create release checklist → [generates QA checklist]
5. Send summary to project lead → [formats report]
```

**When to Use an Agent:**
- Complex, multi-step workflows
- Tasks requiring decision-making ("which tasks are critical?")
- Workflows that vary based on context
- Long-running background processes

---

#### **What Are MCP Servers? 🌐**
**Definition:** Model Context Protocol (MCP) servers are standardized tool servers that expose APIs as callable functions for AI models.

**Think of it as:** A toolbox that AI models can reach into to interact with external systems

**Architecture:**
```
┌─────────────┐
│  AI Model   │  "Create a task in project X"
└──────┬──────┘
       │
       ├─ calls tool: Create-Task
       │
┌──────▼──────────┐
│   MCP Server    │  ← Your custom tool server
│  - List Tasks   │
│  - Create Task  │
│  - Update Task  │
└──────┬──────────┘
       │
┌──────▼──────────────┐
│  SAP Cloud ALM API  │
└─────────────────────┘
```

**Key Characteristics:**
- **Interoperability** - follows standardized MCP specification for cross-platform compatibility
- **Connectivity** - bridges AI models with external systems
- **Database, APIs, filesystems (Integrations)** - connects to diverse data sources and services
- **Reliability** - provides stable, type-safe tool interfaces with JSON Schema validation

**What an MCP Server Provides:**
1. **Tools** - callable functions (e.g., `Create-Task`)
2. **Resources** - data sources (e.g., project configurations)
3. **Prompts** - reusable prompt templates

**When to Build an MCP Server:**
- You have 5+ APIs to expose
- Multiple AI applications need the same tools
- You want centralized governance (logging, auth, rate limiting)
- Enterprise deployment with multiple teams

---

### Skills vs Agents vs MCP Servers: Quick Comparison

| Aspect | Skills | Agents | MCP Servers |
|--------|--------|--------|-------------|
| **What** | Behavior template | Autonomous executor | API tool server |
| **Purpose** | Define HOW to act | DO the work | Provide TOOLS |
| **Autonomy** | None (invoked) | High (self-directed) | None (serves tools) |
| **Complexity** | Low | High | Medium |
| **Example** | "Task management skill definition" | "Agent that runs weekly project reviews" | "Server exposing 20 CALM API tools" |
| **Created by** | Markdown file | Code + AI orchestration | Server application (any language) |

**How They Work Together:**
```
Agent uses a Skill's behavior + MCP Server's tools

Example:
┌─────────────────────────────┐
│  Project Review Agent       │  ← Autonomous executor
│  (uses project-task-skill)  │  ← Follows skill's behavior
│  (calls MCP server tools)   │  ← Uses tools to access APIs
└─────────────────────────────┘
          │
          ├─→ List-Projects
          ├─→ List-Tasks
          └─→ Create-Report
          ↓
    ┌─────────────────┐
    │   MCP Server    │
    │  (CALM Tools)   │
    └─────────────────┘
```

---

### The "Vibe Coding" Approach

**What Is Vibe Coding?**
Building software by describing what you want in natural language, and letting AI generate the code, configuration, and infrastructure.

**How It Works:**
```
You: "Create an MCP server that exposes SAP Cloud ALM task APIs with OAuth authentication"

AI (Cline/Claude):
1. Generates server boilerplate
2. Adds OAuth token handling
3. Defines MCP tool schemas
4. Implements API client
5. Adds error handling
6. Writes tests

You: "Add caching for the list tasks endpoint"

AI: [adds caching logic, updates tests]
```

**Benefits:**
- **Fast prototyping** - go from idea to working code in minutes
- **Lower barrier** - less need for deep framework knowledge
- **Iterative** - refine through conversation
- **Learning tool** - understand patterns by seeing generated code

**Best Practices for Vibe Coding:**
1. **Be specific** - "Add OAuth2 client credentials flow with token caching"
2. **Iterate incrementally** - build feature by feature
3. **Review generated code** - understand what was created
4. **Test as you go** - verify each feature works before moving on

**Perfect For:**
- Building MCP servers from scratch
- Configuring AI skills and agents
- Integrating SAP Cloud ALM APIs
- Prototyping new workflows

---

## Implementation Paths

Choose the approach that fits your needs:

### Path 1: Direct API Integration (Simplest)
**Best for**: Simple automation scripts, single-purpose tools

Make direct REST API calls from your code:
```python
# Example: List tasks using SAP Cloud ALM API
import requests

response = requests.get(
    'https://your-tenant.eu10.alm.cloud.sap/api/calm-tasks/v1/tasks',
    headers={
        'Authorization': f'Bearer {access_token}',
        'Content-Type': 'application/json'
    }
)
tasks = response.json()
```

**Pros**: Simple, no additional infrastructure  
**Cons**: No AI tool-calling integration, manual API handling

---

### Path 2: AI with Tool Calling (Recommended)
**Best for**: Conversational interfaces, natural language automation

Integrate AI models (Claude, GPT, etc.) with tool/function calling to let AI interact with SAP Cloud ALM APIs.

**Architecture**:
```
User: "Create a task for login bug"
         ↓
AI Model: Analyzes request → Decides to call create_calm_task tool
         ↓
Your App: Executes the tool the AI chose → Returns result
         ↓
AI Model: Receives result → Formulates human-readable response
         ↓
User: "I've created task TASK-123 'Fix login bug'"
```

**Example Tools Definition** (for Claude):
```python
tools = [
    {
        "name": "list_calm_tasks",
        "description": "List tasks from SAP Cloud ALM with optional filters",
        "input_schema": {
            "type": "object",
            "properties": {
                "projectId": {"type": "string", "description": "Filter by project GUID"},
                "status": {"type": "string", "enum": ["OPEN", "IN_PROGRESS", "COMPLETED"]},
                "assignedTo": {"type": "string", "description": "Filter by assignee user ID"}
            }
        }
    },
    {
        "name": "create_calm_task",
        "description": "Create a new task in SAP Cloud ALM",
        "input_schema": {
            "type": "object",
            "properties": {
                "title": {"type": "string", "description": "Task title"},
                "description": {"type": "string", "description": "Task description"},
                "projectId": {"type": "string", "description": "Project GUID"},
                "priority": {"type": "string", "enum": ["LOW", "MEDIUM", "HIGH"]}
            },
            "required": ["title", "projectId"]
        }
    }
]

# Your app executes the tools that AI chooses to call
def execute_tool(tool_name, tool_input):
    # AI decided which tool to use - your app just executes it
    if tool_name == 'list_calm_tasks':
        return calm_client.list_tasks(**tool_input)
    elif tool_name == 'create_calm_task':
        return calm_client.create_task(**tool_input)
```

**User Experience**:
```
User: "Create a task for fixing the login bug in project Alpha with high priority"
AI: [calls create_calm_task tool]
AI: "I've created task TASK-123 'Fix login bug' in project Alpha with high priority."
```

**Pros**: Natural language interface, intelligent workflow handling  
**Cons**: Requires AI model integration

---

### Path 3: Build MCP Server (Advanced)
**Best for**: Exposing multiple APIs as AI-callable tools, complex integrations

Build a Model Context Protocol server that wraps SAP Cloud ALM APIs as tools.

**Benefits**:
- AI models can discover and call your tools automatically
- Type-safe tool definitions with JSON Schema
- Reusable across multiple AI applications
- Built-in error handling and validation

**Example MCP Tool Definition**:
```typescript
{
  name: "CALM_TKM-List-Tasks",
  description: "List tasks in SAP Cloud ALM with optional filters",
  inputSchema: {
    type: "object",
    properties: {
      projectId: { type: "string", description: "Filter by project GUID" },
      status: { type: "string", enum: ["OPEN", "IN_PROGRESS", "COMPLETED"] },
      assignedTo: { type: "string", description: "Filter by assignee" }
    }
  }
}
```

---

### Path 4: Agent Definition Files (Declarative)
**Best for**: Reusable agent definitions, version-controlled behavior, framework-based deployment

Define your agent's behavior in a markdown file with YAML frontmatter. **The agent definition describes behavior; tools can come from Path 1 (direct API), Path 2 (inline), or Path 3 (MCP server).**

**Agent Definition Structure**:
```markdown
---
name: calm-task-assistant
version: 1.0.0
description: Manages SAP Cloud ALM tasks and projects with natural language
modelName: claude-sonnet-4.6
tools:
  - create_calm_task
  - list_calm_tasks
  - update_calm_task
  - list_calm_projects
  - get_calm_project

---

# CALM Task Assistant

You are a specialized assistant for managing tasks in SAP Cloud ALM.

## Capabilities
- Create and manage tasks with smart defaults
- Query tasks with natural language filters
- Link tasks to projects and requirements
- Assign tasks to team members

## Guidelines
1. Always verify project exists before creating tasks
2. Use clear, descriptive task titles
3. Set appropriate priorities based on urgency indicators in user requests
4. Ask for clarification if project context is missing

## Example Interactions

**User**: "Create a high priority task for fixing the login bug in Project Alpha"
**Action**: 
1. Search for project named "Alpha" using list_calm_projects
2. Create task using create_calm_task with priority=HIGH
3. Confirm task creation with task ID

**User**: "Show me all open tasks assigned to me"
**Action**: Use list_calm_tasks with status=OPEN and current user's ID
```

**How Tools Are Resolved**:

The agent definition references tools by name (e.g., `create_calm_task`, `list_calm_tasks`). The actual tool implementation can come from:
- **Path 1**: Direct API calls in your code
- **Path 2**: Inline tool definitions passed to the AI model
- **Path 3**: MCP server exposing the tools

Your application loads the agent definition and connects it to whichever tool source you've chosen.

**Benefits**:
- **Declarative**: Describe behavior, not implementation
- **Version Controlled**: Agent definitions are text files
- **Easy Iteration**: Change markdown, no code changes needed
- **Reusable**: Share agent definitions across teams
- **Tool-Agnostic**: Works with any tool source (API, inline, or MCP)

**Requirements**:
- Tools must be available via one of the three paths
- Needs a framework/loader to execute the agent definition
- Compatible with Claude Code, Anthropic Agent SDK, or custom loaders

**Pros**: Clean separation of behavior and infrastructure, easy to version and share  
**Cons**: Requires framework support or custom loader implementation

---

## Choosing the Right Path

| Path | Complexity | Best For | Tools | Reusability |
|------|-----------|----------|-------|-------------|
| **Path 1: Direct API** | 🟢 Simple | Quick scripts, automation | N/A | Single use |
| **Path 2: AI + Tools** | 🟡 Medium | Conversational apps | Inline code | Single app |
| **Path 3: MCP Server** | 🔴 Complex | Enterprise, multiple apps | Separate service | High |
| **Path 4: Agent Files** | 🟡 Medium | Framework-based, reusable agents | Via MCP or Path 2 | High |

## Key SAP Cloud ALM APIs

> **Note on API Coverage**  
> This guide focuses on **Task Management (TKM)** and **Project Management (PJM)** APIs. SAP Cloud ALM offers additional APIs for features, requirements, quality gates, process management, and more. The patterns and approaches demonstrated here apply to all SAP Cloud ALM APIs.

### Task Management API (CALM_TKM)

**API Documentation**: [CALM_TKM on SAP API Hub](https://hub.sap.com/api/CALM_TKM/resource/Tasks)  
**Base URL**: `https://{your-tenant}.{region}.alm.cloud.sap/api/calm-tasks/v1`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/tasks` | GET | List tasks with filters |
| `/tasks` | POST | Create a new task |
| `/tasks/{id}` | GET | Get task by UUID |
| `/tasks/{id}` | PATCH | Update task |
| `/tasks/{id}` | DELETE | Delete task |
| `/tasks/{id}/subTasks` | GET | Get all child tasks (sub-tasks and checklist items) |

### Project Management API (CALM_PJM)

**API Documentation**: [CALM_PJM on SAP API Hub](https://hub.sap.com/api/CALM_PJM/resource/Projects)  
**Base URL**: `https://{your-tenant}.{region}.alm.cloud.sap/api/calm-projects/v1`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/projects` | GET | List all projects |
| `/projects` | POST | Create a project |
| `/projects/{id}` | GET | Get a single project by ID |
| `/projects/{id}` | PATCH | Update a project |


---

## Best Practices

### 1. Authentication & Security
- **Never hardcode credentials** - use environment variables or secure vaults
- **Token caching** - cache access tokens to reduce authentication calls
- **Scope minimization** - request only the API scopes you need
- **Rate limiting** - respect API rate limits 

### 2. Error Handling
- Handle authentication failures (401) by refreshing tokens
- Implement exponential backoff for rate limits (429 errors)
- Validate API responses before processing
- Provide clear error messages to users

### 3. AI Prompt Design
- **Be specific** - provide clear tool descriptions
- **Add examples** - include example inputs/outputs in tool descriptions
- **Validate inputs** - use JSON Schema to validate tool inputs
- **Handle ambiguity** - train the AI to ask clarifying questions

---

## Resources

### Documentation
- [SAP Cloud ALM API Hub](https://hub.sap.com) - API documentation
- [Claude API Documentation](https://docs.anthropic.com) - AI model integration
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io) - MCP specification

### Reference Implementations
- [Workshop: Build Your SAP Cloud ALM MCP Server](./WORKSHOP_MCP_EXERCISE.md) - Complete MCP server implementation with step-by-step guide


---

## Next Steps

1. **[Workshop: Build Your SAP Cloud ALM MCP Server](./WORKSHOP_MCP_EXERCISE.md)** - Hands-on guide to building a complete MCP server with AI (vibe coding approach)
2. **Start Experimenting** - Choose a path (1-4) based on your needs and begin prototyping
3. **Join the Community** - Share your implementations and learn from others on SAP forums

---

