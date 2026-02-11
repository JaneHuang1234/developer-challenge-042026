# Coding Challenge - The Orchestration Workflow in Generative AI Hub on SAP AI Core

For this month's coding challenge on the SAP Community, you will have the opportunity to learn more about the Orchestration Workflow available on Generative AI Hub with SAP AI Core.
You will learn how to work with the APIs of the SAP Cloud SDK for AI to create an orchestration workflow including document grounding. You will also work on building a code-based agent to consume the grounded document information.

The coding challenge will span over the next four weeks where you will be working on 4 separate challenges, one for every week. At the end of each week you need to upload the results of the given week's challenge. This can be a screenshot or a configuration file but no worries, each week's challenge will exactly tell you what to do.

But first, let's set the stage.

## Setting the stage

This year's coding challenges are all about voluntary activities. The United Nations has designated 2026 as the International Year of Volunteers and we want you to think about what such an initiative could be. For this month's coding challenge, think about how you could utilize the Orchestration Workflow to support volunteer initiatives.

Imagine you are working on a project for which you should ground and orchestrate contextual information to a Large Language Model (LLM) in order to support a voluntary organization, group or individuals. Here are some example use cases you can get inspired by:

1. Disaster Relief Coordinator Assistant
   Ground emergency response procedures, local shelter locations, and volunteer skill databases. The orchestration workflow could:
   - Match volunteers with specific disaster relief needs based on their skills
   - Provide real-time guidance on emergency protocols
   - Generate personalized volunteer briefings based on current situation reports

2. Community Food Bank Navigator
   Ground food bank inventory, dietary restrictions databases, and distribution schedules. Use cases:
   - Help volunteers quickly answer client questions about available food items
   - Generate culturally appropriate meal suggestions based on current inventory
   - Create multilingual information sheets for diverse communities

3. Environmental Conservation Knowledge Base
   Ground scientific reports, species identification guides, and local ecosystem data. Applications:
   - Assist volunteer park rangers with species identification queries
   - Generate educational content for school visits based on seasonal wildlife activity
   - Create site-specific conservation action plans for volunteer groups

4. Senior Care Companion Support
   Ground medical guidelines, activity recommendations, and local senior resources. Benefits:
   - Help volunteers provide accurate information about medication schedules
   - Suggest appropriate activities based on mobility levels and interests
   - Generate conversation starters tailored to individual senior backgrounds

5. Refugee Integration Helper
   Ground immigration procedures, local services directories, and language learning resources:
   - Answer common questions about housing, healthcare, and employment in multiple languages
   - Generate personalized integration roadmaps based on individual circumstances
   - Create cultural orientation materials specific to the local community

## The Solution Diagram

For this challenge you are using different systems to achieve an automated grounding process and you will set up an orchestration workflow on Generative AI Hub.

![code_challenge_sd](./S3_Bucket_Orchestration_AICore.png)

### SAP BTP Architecture for Grounding and Orchestration Workflow

This architecture diagram illustrates the complete system setup for implementing a RAG (Retrieval Augmented Generation) solution using SAP BTP (Business Technology Platform) services integrated with partner foundation models.
The data, in this case, is stored within an S3 Bucket on AWS (Amazon Web Services) managed through the Document Store service on BTP. As vector database, this solution uses the SAP HANA Cloud Vector Engine.

#### Main Components:

**SAP BTP Platform**
The entire solution runs on SAP Business Technology Platform on AWS:

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

- **Azure OpenAI Services**: Provides the LLM and embedding models via HTTPS connection
- Additional partner models indicated by "..." (extensible architecture)

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

![code_challenge_sd](./S3_Bucket_Orchestration_AICore_sequence_diagram.png)

### Grounding Document & Vectorization Process on SAP BTP with AWS

This sequence diagram illustrates the complete workflow for setting up a document grounding pipeline and orchestration workflow using SAP AI Core on SAP BTP (running on AWS infrastructure).

#### 1: Credentials & Upload

The process begins with the user creating an instance of the SAP BTP Object Store service in Cloud Foundry, which provisions an S3 bucket on AWS. The user receives service credentials and uses Bruno (an API client) to upload grounding documents directly to the S3 bucket. These documents will serve as the knowledge base for the RAG (Retrieval Augmented Generation) system.

#### 2: Pipeline Setup

Next, the user configures the infrastructure through SAP AI Launchpad by creating a Resource Group. Using Bruno, they create a generic secret in SAP AI Core (storing credentials for external services like Azure OpenAI) and then create a grounding pipeline. AI Core returns a pipeline ID that will be used to execute the grounding process.

#### 3: Grounding & Vectorization

When triggered, SAP AI Core activates the Grounding Service, which fetches the documents from S3. The service chunks the documents into smaller segments and preprocesses them for embedding. These chunks are then sent to an Embedding Model (such as Azure OpenAI's text-embedding model), which converts them into vector representations. The resulting embeddings are stored in SAP HANA Cloud's Vector Engine, creating a searchable vector database.

#### 4: Orchestration & Querying

Finally, the user creates an orchestration workflow in SAP AI Launchpad and configures it to use the grounding pipeline. When a query is submitted, the Orchestrator performs a cosine similarity search in HANA Cloud to retrieve the most relevant document chunks. These chunks are then passed as context to a Foundation Model (LLM) like Azure OpenAI GPT-4, which generates a contextual response. The orchestrated answer is returned to the user, combining the grounded knowledge with the LLM's generative capabilities.

This architecture demonstrates a complete RAG implementation using SAP's AI services, enabling volunteers or coordinators to query domain-specific knowledge with accurate, contextually grounded responses.

## The Challenge

Now that you have a better understanding of the technology stack used and the architecture, let's talk about the challenge.

You will work through the challenge using Jupiter Notebooks in Business Application Studio. Here you can comfortably use a Python environment and a pre-defined environment to work on the challenges.

The challenge is structured as follows:

**Week 1:**

- Understand and work on the orchestration workflow
- Understand and implement document grounding
- Ground a document & test the orchestration workflow

**Week 2:**

- Build a code-based agent with LiteLLM, CrewAI and generative AI Hub

**Week 3:**

- Combine the code-based agent you built with the orchestration workflow from week 1
- Have the agent use the grounding service as tool

**Week 4:**

- Utilize SAP's RPT-1 model from a code-based to understand and populate tabular data structures
