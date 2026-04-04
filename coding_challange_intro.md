# AI Developer Challenge April 2026 - build AI Agents with Generative AI Hub

For this month's coding challenge on the SAP Community, you will have the opportunity to learn more about the Orchestration Workflow available on Generative AI Hub with SAP AI Core. You will also work on building your first code-based agents with CrewAI and LiteLLM.

**What you'll learn:** Build production-ready AI solutions that combine Retrieval-Augmented Generation (RAG) with intelligent agents. You will learn how to work with the APIs of the SAP Cloud SDK for AI to create an orchestration workflow including document grounding, and build code-based agents that leverage grounded document information to provide accurate, context-aware responses.

The coding challenge will span over the next four weeks where you will be working on 4 separate challenges, one for each week. At the end of each week you need to upload the results of the given week's challenge. This can be a screenshot or a configuration file, but no worries, each week's challenge will exactly tell you what to do.

But first, let's set the stage.

## Setting the stage

The United Nations has designated 2026 as the International Year of Volunteers and we want you to think about what such an initiative could be.

**Why this matters:** Volunteer organizations often struggle with information accessibility - experienced knowledge is scattered across documents, reports, and guides. By combining AI orchestration with document grounding, you can create intelligent assistants that make this knowledge instantly accessible to volunteers in the field, enabling them to make better decisions and have greater impact.

For this month's coding challenge, you'll build a system that could support volunteer initiatives by grounding and orchestrating contextual information to a Large Language Model (LLM). Here is the use case for this challenge:

**Social Services in Germany**

For this month's code challenge, you will build an intelligent solution for social wellfare service recipients to fetch information about the "Grundsicherung", a social service for unemployed citizens in Germany. On top of that the service should help social wellfare service recipients to find information about food banks in Germany, these food banks are provided through an organization called "Tafel Deutschland".

## The Solution Diagram

For this challenge you are using different systems to achieve an automated grounding process and you will set up an orchestration workflow on Generative AI Hub.

![code_challenge_sd](./S3_Bucket_Orchestration_AICore.png)

## SAP BTP Architecture for Grounding and Orchestration Workflow

This architecture diagram illustrates the complete system setup for implementing a RAG (Retrieval Augmented Generation) solution using SAP BTP (Business Technology Platform) services integrated with partner foundation models.
The data, in this case, is stored within an S3 Bucket on AWS (Amazon Web Services) managed through the Document Store service on BTP. As vector database, this solution uses the SAP HANA Cloud Vector Engine.

### Main Components:

**SAP BTP Platform**
The entire solution runs on SAP Business Technology Platform:

1. **Generative AI Hub** - The AI service layer containing:
   - **SAP AI Launchpad**: User interface for managing AI scenarios and deployments
   - **SAP AI Core**: The core AI orchestration engine containing:
     - **Orchestration Workflow**: Coordinates the entire RAG process by querying the LLM and triggering grounding
     - **Grounding Service**: Handles document fetching, chunking, and vectorization
     - **Foundation Model Access**: Provides connectivity to external LLMs via HTTPS

2. **SAP BTP, Cloud Foundry runtime** - Contains:
   - **S3 Bucket (AWS) Document Store**: Cloud storage for grounding documents that the AI Engineer uploads

#### External Components:

**Partner Foundation Models**

- **Foundation Model Providers**: Provides LLM and embedding models via HTTPS connection (e.g., Gemini, Azure OpenAI, Amazon Bedrock)
- Extensible architecture supporting multiple model providers

**AI Engineer with Bruno**

- The human operator who uploads documents to the S3 bucket using Bruno (API client tool)
- The human operator who manages secrets in SAP AI Core using Bruno

### Data Flow:

1. **Upload Flow** (Purple arrow): AI Engineer uploads documents via Bruno to the S3 bucket
2. **Vectorization Flow** (Orange arrow): Grounding Service processes documents and stores embeddings in HANA Cloud Vector Engine
3. **Grounding Flow** (Blue arrow): Fetches grounding documents from storage
4. **Similarity Search Flow** (Green arrow): Orchestration Workflow queries HANA Cloud's Vector Engine for relevant context

**SAP HANA Cloud (Vector Engine)**
The vector database that stores document embeddings and performs cosine similarity searches to retrieve relevant context for user queries.

This architecture enables a complete RAG implementation where documents are grounded (vectorized and stored), and user queries are enriched with relevant context before being sent to foundation models for response generation.

## Understand what is happening

To fully understand the single steps that need to be taken, you can use the following sequence diagram.

![code_challenge_sd](<./Grounding%20Document%20&%20Vectorization%20(SAP%20BTP%20on%20AWS).png>)

### Grounding Document & Vectorization Process on SAP BTP with AWS

This sequence diagram illustrates the complete workflow for setting up a document grounding pipeline and orchestration workflow using SAP AI Core on SAP BTP (running on AWS infrastructure).

#### 1: Credentials & Upload

The process begins with the user creating an instance of the SAP BTP Object Store service in Cloud Foundry, which provisions an S3 bucket on AWS. The user receives service credentials and uses Bruno (an API client) to upload grounding documents directly to the S3 bucket. These documents will serve as the knowledge base for the RAG (Retrieval Augmented Generation) system.

#### 2: Pipeline Setup

Next, the user configures the infrastructure through SAP AI Launchpad by creating a Resource Group. Using Bruno, they create a generic secret in SAP AI Core (storing credentials for external services like partner foundation model providers) and then create a grounding pipeline. AI Core returns a pipeline ID that will be used to execute the grounding process.

#### 3: Grounding & Vectorization

When triggered, SAP AI Core activates the Grounding Service, which fetches the documents from S3. The service chunks the documents into smaller segments and preprocesses them for embedding. These chunks are then sent to an Embedding Model (from partner providers like Gemini, Azure OpenAI, or Amazon Bedrock), which converts them into vector representations. The resulting embeddings are stored in SAP HANA Cloud's Vector Engine, creating a searchable vector database.

#### 4: Orchestration & Querying

Finally, the user creates an orchestration workflow in SAP AI Launchpad and configures it to use the grounding pipeline. When a query is submitted, the Orchestrator performs a cosine similarity search in HANA Cloud to retrieve the most relevant document chunks. These chunks are then passed as context to a Foundation Model (LLM) such as Gemini or GPT-4, which generates a contextual response. The orchestrated answer is returned to the user, combining the grounded knowledge with the LLM's generative capabilities.

This architecture demonstrates a complete RAG implementation using SAP's AI services, enabling volunteers or coordinators to query domain-specific knowledge with accurate, contextually grounded responses.

## The Challenge

Now that you have a better understanding of the technology stack used and the architecture, let's talk about the challenge.

**TL;DR:** Over four weeks, you'll progress from basic document grounding to building intelligent agents that can reason with domain-specific knowledge, all using Jupyter Notebooks with pre-configured infrastructure.

### Prerequisites

To successfully complete this challenge, you should have:

- Basic Python programming experience
- Familiarity with Jupyter Notebooks
- Understanding of REST APIs (helpful but not required)
- Interest in AI/ML concepts (no deep expertise needed)

### Environment Setup

You will work through the challenge using Jupyter Notebooks in Business Application Studio. Here you can comfortably use a Python environment and a pre-defined environment to work on the challenges.

You don't have to take care of the infrastructure setup. We will provide you with access to a fully functioning system to work through the Jupyter Notebooks.

### Weekly Structure

The challenge is structured as follows:

**Week 1: Grounding with SAP Generative AI Hub**

What you'll learn:

- **Connect to the Orchestration Service**: Access SAP's Generative AI Hub orchestration service, which provides a unified interface to multiple LLM models through a single deployment
- **Configure Document Grounding**: Set up the document grounding service to retrieve relevant context from a vector database before generating responses
- **Implement RAG Pattern**: Build a complete RAG workflow that combines document retrieval with LLM generation to provide contextually accurate answers
- **Use Prompt Templates**: Create structured prompts that incorporate both user queries and grounded context from your knowledge base

**Week 2: Building AI Agents with CrewAI and LiteLLM**

What you'll learn:

- **Build Your First AI Agent**: Create an intelligent agent with a specific role, goal, and backstory using the CrewAI framework
- **Define Agent Tasks**: Structure concrete objectives and expected outputs that guide agent behavior
- **Integrate Multiple Technologies**: Connect CrewAI with SAP Generative AI Hub models through LiteLLM's unified API
- **Process Complex Queries**: Enable agents to analyze user input, make decisions, and provide structured recommendations

**Week 3: AI Agents with Grounding Tools**

What you'll learn:

- **Create Custom Agent Tools**: Build a custom tool that wraps the document grounding service, making it accessible to your AI agent
- **Enable Tool-Based Reasoning**: Allow agents to decide when and how to use tools based on user queries
- **Integrate RAG with Agents**: Combine retrieval-augmented generation with agentic workflows for more accurate, knowledge-grounded responses
- **Build End-to-End Solutions**: Create a complete system where agents autonomously retrieve relevant information before making decisions

**Week 4: Structured Data Extraction with AI**

What you'll learn:

- Utilize SAP's RPT-1 model from a code-based agent to understand and populate tabular data structures
- Extract structured information from unstructured documents
- Automatically fill forms and templates using AI-driven data extraction

### Submission Requirements

At the end of each week, you'll need to submit evidence of your completed challenge:

- Screenshots of successful executions
- Configuration files or code snippets as specified in each week's exercise
- Brief description of any challenges you encountered and how you solved them

Detailed submission instructions will be provided in each week's Jupyter Notebook.
