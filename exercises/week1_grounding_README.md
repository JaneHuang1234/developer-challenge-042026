# Week 1: Grounding with SAP Generative AI Hub

## Overview

This exercise introduces the orchestration service of SAP's Generative AI Hub and demonstrates how to implement Retrieval-Augmented Generation (RAG) using the document grounding capability.

The orchestration service lets you use all available models with the same codebase. A deployment comes automatically with your AI Core instance, and you can access all available models by changing the model name parameter. You can also use grounding, prompt templating, data masking, and content filtering capabilities.

## What You'll Achieve

By working through this exercise, you'll learn how to:

- **Connect to the Orchestration Service**: Access SAP's Generative AI Hub orchestration service, which provides a unified interface to multiple LLM models through a single deployment
- **Configure Document Grounding**: Set up the document grounding service to retrieve relevant context from a vector database before generating responses
- **Implement RAG Pattern**: Build a complete RAG workflow that combines document retrieval with LLM generation to provide contextually accurate answers
- **Use Prompt Templates**: Create structured prompts that incorporate both user queries and grounded context from your knowledge base

The exercise demonstrates a practical implementation where the LLM can answer questions about the German NGO "die Tafel" and the German basic income support by retrieving relevant information from a pre-configured vector database, showcasing how grounding enhances response accuracy with domain-specific knowledge.

## Prerequisites

- Access to SAP AI Core instance
- Python environment (Jupyter Notebook)
- Cloud SDK for AI package (`sap-ai-sdk-gen`)

## Key Components

### 1. LLM Configuration

The exercise uses the `gemini-2.5-flash` model with temperature set to 0.0 for consistent, deterministic responses.

### 2. Prompt Template

A structured template that includes:

- **System Message**: Defines the AI's role as a helpful assistant for the German citizen center
- **User Message**: Combines user queries with grounded context from the vector database

### 3. Document Grounding Setup

- **Data Repository ID**: Pre-configured vector database containing documents about German social services
- **Search Filters**: Configured to retrieve up to 15 relevant chunks from the vector database
- **Data Repository Type**: Vector-based retrieval for semantic search

### 4. Orchestration Configuration

Combines the LLM, template, and grounding module to create a unified workflow that:

1. Receives user queries
2. Retrieves relevant context from the vector database
3. Constructs prompts with grounded information
4. Generates accurate, context-aware responses

## Implementation Steps

1. **Install Dependencies**: Install the Cloud SDK for AI package
2. **Import Required Packages**: Load orchestration models and services
3. **Configure LLM and Template**: Set up the model and prompt structure
4. **Create Grounding Configuration**: Define document filters and grounding parameters
5. **Build Orchestration Config**: Combine all components into a single configuration
6. **Stream Responses**: Execute queries and receive streamed responses

## Testing Your Implementation

Try asking questions such as:

- "What is die Tafel in Germany?"
- Questions about German basic income support (Grundsicherung)
- Other queries related to German social services

The system will retrieve relevant context from the vector database and provide accurate, grounded responses.
