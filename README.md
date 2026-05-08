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
```

## Workflow 1: Drive to Pinecone Ingestion

**File:** `workflows/01-drive-to-pinecone-ingestion.json`

**Purpose:**

This workflow watches a Google Drive folder for newly uploaded Tesla quarterly earnings PDFs. When a new file is added, the workflow downloads the PDF, extracts the text, splits it into chunks, adds structured metadata, generates embeddings with OpenAI, and stores the vectors in Pinecone.

This workflow represents the ingestion layer of the system.

## Metadata Strategy

Each document chunk is tagged with:

```text
source_file
company
fiscal_year
fiscal_quarter
document_type
```

The `fiscal_year` and `fiscal_quarter` fields are extracted from the file name using n8n JavaScript expressions and regex.

Example filename:

```text
TSLA-Q1-2026-Update.pdf
```

Generated metadata:

```text
source_file: TSLA-Q1-2026-Update.pdf
company: Tesla
fiscal_year: 2026
fiscal_quarter: Q1
document_type: earnings_update
```

## Technologies Used

```text
n8n
Google Drive
OpenAI Embeddings
Pinecone Vector Database
MCP
RAG
Google Sheets
```

## Setup Notes

Before running the workflow, configure your own credentials in n8n:

```text
Google Drive OAuth2 credential
OpenAI credential
Pinecone credential
Google Drive folder ID
Pinecone index and namespace
```

The public workflow JSON uses placeholder values for credentials and folder IDs.

Example placeholders:

```text
YOUR_GOOGLE_DRIVE_CREDENTIAL_ID
YOUR_GOOGLE_DRIVE_FOLDER_ID
YOUR_OPENAI_CREDENTIAL_ID
YOUR_PINECONE_CREDENTIAL_ID
```

## Pinecone Configuration

The workflow is configured to use:

```text
Index: n8ntesla
Namespace: tesla-financials-v1
```

These values can be changed after importing the workflow into n8n.

## Why This Project Matters

This project demonstrates several skills relevant to AI automation and n8n workflow engineering:

```text
Document ingestion pipeline design
RAG architecture
Vector database integration
Metadata extraction
Credential hygiene
Workflow modularity
AI tool orchestration
Production-style workflow separation
```

## Next Steps

Planned additions:

```text
MCP Server workflow exposing the Tesla Financial RAG Tool
Client Assistant workflow using the MCP Client
Google Sheets interaction logging
Screenshots and demo video
Architecture documentation
```

## Repository Structure

```text
ai-orchestration-mcp-rag-n8n/
  README.md
  workflows/
    01-drive-to-pinecone-ingestion.json
  screenshots/
  docs/
```

## Author

Built by Boris Villanueva as part of an AI automation portfolio focused on n8n, MCP, RAG, and workflow orchestration.
