# Week 2: Building AI Agents with CrewAI and LiteLLM

## Overview

This exercise introduces AI agent development by combining CrewAI (an agent framework), LiteLLM (a unified LLM interface), and SAP's Generative AI Hub as the LLM provider to create intelligent, task-oriented agents.

Welcome to week 2 of the April Developer Challenge on AI! Last week you learned how to build a RAG use case with the grounding service and the orchestration service. This week you'll build an AI agent using LiteLLM, CrewAI, and Generative AI Hub.

## What You'll Achieve

By working through this exercise, you'll learn how to:

- **Build Your First AI Agent**: Create an intelligent agent with a specific role, goal, and backstory using the CrewAI framework
- **Define Agent Tasks**: Structure concrete objectives and expected outputs that guide agent behavior
- **Integrate Multiple Technologies**: Connect CrewAI with SAP Generative AI Hub models through LiteLLM's unified API
- **Process Complex Queries**: Enable agents to analyze user input, make decisions, and provide structured recommendations

The exercise implements a Hamburg Social Welfare Case Manager agent that can process citizen inquiries, assess eligibility for welfare programs, and generate personalized support plans. This demonstrates how AI agents can be designed to handle domain-specific scenarios requiring structured analysis and decision-making capabilities.

## Key Technologies

### LiteLLM

LiteLLM is a library that provides a unified, provider-agnostic API for calling large language models (LLMs) and handling common tasks (completion, chat, streaming, multimodal inputs). It standardizes request/response handling and includes utilities that speed up integration with agent frameworks. Essentially, it's a gateway between LLM providers and AI Agent frameworks.

This means you can use your Generative AI Hub credentials to build state-of-the-art AI Agents with any models available through GenAI Hub and any AI Agent frameworks compatible with LiteLLM. You can use LLMs hosted or managed by SAP (Mistral, Llama, Nvidia) and models from various partners including Gemini, Amazon Bedrock (Anthropic), and Azure OpenAI.

### CrewAI

CrewAI is a third-party open-source Python library. As the name suggests, you can use it to build a crew of agents that have a set of tools available to accomplish certain tasks. CrewAI uses tasks to bridge the gap between high-level goals and concrete agent actions, assigning specific objectives and expected outputs. For now, your agent will only respond to incoming queries.

## Implementation Components

### 1. Agent Configuration

The Hamburg Social Welfare Case Manager agent is configured with:

- **Role**: Hamburg Social Welfare Case Manager
- **Goal**: Process and manage social welfare applications, matching citizens with appropriate services
- **Backstory**: Experienced case manager with deep knowledge of Hamburg's social services
- **LLM**: Uses `sap/gpt-4o` from Generative AI Hub
- **Verbose Mode**: Enabled for detailed execution tracking

### 2. Task Definition

Tasks in CrewAI define:

- **Description**: Specific instructions for processing user inquiries
- **Expected Output**: Structured assessments with eligibility determination and support plans
- **Agent Assignment**: Links the task to the welfare agent

### 3. Interactive Workflow

The system includes:

- User input prompt for welfare inquiries
- Dynamic task creation based on user questions
- Crew execution with verbose output
- Formatted assessment report generation

## Environment Setup

The notebook handles environment configuration in two ways:

1. **Trial Environment**: Reads from `config.json` file with AI Core credentials
2. **Local Development**: Uses `.env` file with environment variables

Required environment variables:

- `AICORE_AUTH_URL`
- `AICORE_CLIENT_ID`
- `AICORE_CLIENT_SECRET`
- `AICORE_BASE_URL`
- `LITELLM_PROVIDER` (set to "sap")
- `AICORE_RESOURCE_GROUP`

## Testing Your Agent

Try asking various social welfare questions to test the agent's capabilities in:

1. Analyzing citizen circumstances and needs
2. Determining eligibility for welfare programs
3. Recommending local services and resources
4. Creating personalized support plans

## Additional Resources

- [Example Repo](https://sap-contributions.github.io/litellm-agentic-examples/_notebooks/examples/crewai_litellm_lib.html)
- [Blog Post - Build AI Agents with CrewAI](https://community.sap.com/t5/artificial-intelligence-blogs-posts/i-built-an-ai-agent-with-litellm-crewai-and-sap-rpt-1-here-s-what-actually/ba-p/14315663)
- [CodeJam on code-based agents](https://github.com/SAP-samples/codejam-code-based-agents/tree/main)
