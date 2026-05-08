# AI Orchestration System using MCP, RAG, and n8n

This project demonstrates an AI orchestration system built with n8n, MCP, Pinecone, OpenAI embeddings, Google Drive, and structured logging.

The goal is to show how an AI assistant can use a clean multi-workflow architecture to ingest documents, expose retrieval tools through MCP, answer user questions with source-grounded responses, and log interactions for observability.

## Project Status

This repository is being built in stages.

Current workflow included:

1. `01-drive-to-pinecone-ingestion.json`

Coming next:

2. `02-mcp-server-tools.json`
3. `03-client-assistant.json`

## Architecture Overview

The final system is designed as three separate workflows:

```text
Google Drive PDF Upload
        ↓
PDF Download and Text Extraction
        ↓
Chunking and Metadata Tagging
        ↓
OpenAI Embeddings
        ↓
Pinecone Vector Store
        ↓
MCP Server Tool
        ↓
Client Assistant
        ↓
Structured Answer and Interaction Logging
