# Week 3: AI Agents with Grounding Tools

Welcome to week 3 of April's Developer Challenge on AI! This week you will combine what you learned in weeks 1 and 2 to build a more powerful AI agent that uses the grounding service as a tool.

## What You'll Build

In this exercise, you'll enhance the Hamburg Social Welfare Case Manager agent from Week 2 by equipping it with a **custom grounding tool**. This allows the agent to:

- Query the vector database on demand for specific information
- Retrieve Hamburg-specific social services documentation
- Make decisions based on up-to-date, grounded knowledge
- Provide more accurate and verifiable responses

## The Power of Tool-Equipped Agents

Unlike Week 2 where the agent relied solely on its base model knowledge, your Week 3 agent will:

- **Autonomously decide** when to retrieve external information
- **Access real documentation** instead of relying on training data
- **Provide traceable answers** backed by actual source documents
- **Stay current** with information from the knowledge base

This is where AI agents truly shine - combining reasoning capabilities with the ability to access and utilize external knowledge sources!

## What You'll Achieve

By working through this exercise, you'll learn how to:

- **Create Custom Agent Tools**: Build a custom tool that wraps the document grounding service, making it accessible to your AI agent
- **Enable Tool-Based Reasoning**: Allow agents to decide when and how to use tools based on user queries
- **Integrate RAG with Agents**: Combine retrieval-augmented generation with agentic workflows for more accurate, knowledge-grounded responses
- **Build End-to-End Solutions**: Create a complete system where agents autonomously retrieve relevant information before making decisions

The exercise extends the Hamburg Social Welfare Case Manager agent by giving it access to a grounding tool. The agent can now query Hamburg's social services knowledge base to retrieve specific program details, eligibility criteria, and local resources before generating assessments and recommendations. This demonstrates how tool-equipped agents can provide more accurate, up-to-date, and contextually relevant responses compared to agents relying solely on their base model knowledge.

## Prerequisites

- Completion of Week 1 (Grounding) and Week 2 (Agents)
- Python environment (Jupyter Notebook)
- Access to SAP AI Core instance
- Cloud SDK for AI package (`sap-ai-sdk-gen`)

## Key Components

### 1. Custom Grounding Tool

The exercise introduces the `@tool` decorator from CrewAI to create a custom tool that wraps the document grounding service:

```python
@tool("call_grounding_service")
def call_grounding_service(user_question: str) -> str:
    """Retrieve relevant information from the knowledge base"""
```

This tool:

- Accepts user questions as input
- Uses the RetrievalAPIClient from Cloud SDK for AI
- Configures search filters to query the vector database
- Returns relevant document chunks (configured for max 2 chunks)
- Provides grounded information to the agent

### 2. Retrieval Configuration

The grounding tool is configured with:

- **Data Repository ID**: Same vector database from Week 1
- **Data Repository Type**: Vector-based semantic search
- **Search Configuration**: Maximum chunk count (configurable)
- **Filter Settings**: Target specific data repositories

### 3. Enhanced Agent

The Hamburg Social Welfare Case Manager agent is now equipped with:

- **Tools Array**: Includes the `call_grounding_service` tool
- **Updated Goal**: Explicitly instructs the agent to use the grounding service
- **Autonomous Decision Making**: Agent decides when to call the tool based on user queries

### 4. Integration Architecture

The system combines:

1. **CrewAI Framework**: Manages agent behavior and task execution
2. **Foundation Model Access**: Access to SAP Generative AI Hub models
3. **Cloud SDK Retrieval API**: Connects to the vector database
4. **Vector Database**: Contains Hamburg social services knowledge

## How It Works

When a user asks a question:

1. The agent receives the inquiry
2. The agent decides if it needs external knowledge
3. If needed, the agent calls `call_grounding_service` with the user's question
4. The tool queries the vector database and retrieves relevant chunks
5. The agent uses the grounded information to formulate its response
6. A comprehensive, knowledge-grounded assessment is generated

## Benefits Over Week 2

Compared to the Week 2 agent that relied solely on model knowledge:

- **More Accurate**: Responses are grounded in actual documentation
- **Up-to-Date**: Information comes from current knowledge base
- **Verifiable**: Answers can be traced back to source documents
- **Context-Aware**: Retrieves Hamburg-specific information
- **Autonomous**: Agent decides when to use the tool
