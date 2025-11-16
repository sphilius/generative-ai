# AI Assistant Guide: Generative AI on Google Cloud

**Version:** 1.0.0
**Last Updated:** 2025-11-16
**Maintained By:** Repository Team

This document provides AI assistants (like Claude, GitHub Copilot, etc.) with comprehensive context about this repository's structure, conventions, and workflows to enable effective code assistance, debugging, and development support.

---

## Table of Contents

1. [Repository Overview](#repository-overview)
2. [Codebase Structure](#codebase-structure)
3. [Development Workflows](#development-workflows)
4. [Code Conventions & Standards](#code-conventions--standards)
5. [Common Patterns](#common-patterns)
6. [Testing Strategy](#testing-strategy)
7. [Deployment Patterns](#deployment-patterns)
8. [Troubleshooting Guide](#troubleshooting-guide)
9. [AI Assistant Best Practices](#ai-assistant-best-practices)

---

## Repository Overview

### Purpose
This repository demonstrates **Generative AI capabilities on Google Cloud Platform**, providing:
- 350+ Jupyter notebooks with tutorials and examples
- 40+ production-ready sample applications
- Reference implementations for common AI patterns
- Best practices for deploying generative AI on GCP

### Repository Type
**Educational & Reference Implementation Repository** (not a library or framework)

### Target Users
- Developers building AI applications on Google Cloud
- Data scientists working with foundation models
- ML engineers deploying and fine-tuning models
- Enterprise teams implementing RAG and agent systems

### Key Technologies
- **Primary Language:** Python 3.10+
- **Cloud Platform:** Google Cloud Platform (GCP)
- **AI Platform:** Vertex AI
- **Models:** Gemini, Imagen, Veo, Chirp, Lyria, Open Source Models
- **Frameworks:** LangChain, LangGraph, CrewAI, LlamaIndex, Streamlit, Flask, Angular

---

## Codebase Structure

### Directory Organization

```
generative-ai/
├── gemini/                    # Gemini model examples (LARGEST - 34 subdirs)
│   ├── getting-started/       # Introduction notebooks
│   ├── function-calling/      # Tool use and function calling
│   ├── rag-engine/           # RAG implementations
│   ├── agent-engine/         # Agent development
│   ├── sample-apps/          # Full-stack applications
│   ├── use-cases/            # Industry-specific examples
│   ├── multimodal-live-api/  # Real-time multimodal
│   ├── controlled-generation/ # Structured output
│   ├── context-caching/      # Context caching
│   ├── grounding/            # Grounding with Google Search
│   ├── evaluation/           # Model evaluation
│   ├── tuning/               # Fine-tuning examples
│   └── ...                   # (30+ more subdirectories)
│
├── vision/                    # Imagen & Veo (image/video generation)
│   ├── getting-started/
│   ├── sample-apps/
│   └── use-cases/
│
├── audio/                     # Audio generation (Lyria, Chirp)
│   ├── lyria/                # Music generation
│   └── chirp/                # Speech synthesis
│
├── search/                    # Vertex AI Search
│   ├── retrieval-augmented-generation/
│   ├── custom-embeddings/
│   └── ranking-api/
│
├── embeddings/                # Text/multimodal embeddings
│   ├── vector-search/
│   └── use-cases/
│
├── agents/                    # AI agent frameworks
│   ├── adk/                  # Agent Development Kit
│   ├── agent_engine/
│   └── cloud_run/
│
├── open-models/               # Open source models (Gemma, Llama)
│   ├── fine-tuning/
│   ├── serving/
│   └── evaluation/
│
├── partner-models/            # Third-party models
│   └── claude/               # Anthropic Claude integration
│
├── rag-grounding/            # RAG resource index
├── workshops/                # Training workshops
├── genkit/                   # Firebase Genkit integration
├── setup-env/                # Environment setup guides
├── tools/                    # Evaluation tools
├── .github/                  # CI/CD workflows
├── .cloud-build/             # Cloud Build configs
│
├── README.md                 # Main documentation
├── CONTRIBUTING.md           # Contribution guidelines
├── RESOURCES.md              # Learning resources
├── UPDATES.md                # Repository status report
├── CLAUDE.md                 # This file
├── noxfile.py               # Python automation
├── .ruff.toml               # Python linting config
├── renovate.json            # Dependency updates
└── notebook_template.ipynb  # Template for new notebooks
```

### File Naming Conventions

#### Notebooks
- **Format:** `{action}_{model}_{capability}.ipynb`
- **Examples:**
  - `intro_gemini_2_5_pro.ipynb`
  - `rag_evaluation_gemini.ipynb`
  - `function_calling_intro.ipynb`

#### Python Files
- **Format:** `{purpose}_{module}.py`
- **Examples:**
  - `main.py` - Application entry point
  - `config.py` - Configuration
  - `utils.py` - Utility functions
  - `test_{module}.py` - Unit tests

#### Sample Apps
- **Structure:**
```
sample-apps/{app-name}/
├── README.md              # App documentation
├── Dockerfile             # Container definition
├── docker-compose.yml     # Multi-service (optional)
├── requirements.txt       # Python dependencies
├── backend/               # Backend service
│   ├── main.py
│   ├── requirements.txt
│   └── tests/
├── frontend/              # Frontend (if applicable)
│   ├── package.json
│   └── src/
├── terraform/             # Infrastructure (optional)
└── deploy.sh             # Deployment script (optional)
```

### Important Files to Check First

When working on any task, AI assistants should review these files in order:

1. **`README.md`** - Repository overview and directory guide
2. **`CONTRIBUTING.md`** - Contribution guidelines and code quality requirements
3. **`CLAUDE.md`** (this file) - AI assistant guidelines
4. **Directory-specific README** - Each major directory has its own README
5. **`notebook_template.ipynb`** - Template for creating new notebooks
6. **`.ruff.toml`** - Python code style rules
7. **`noxfile.py`** - Automation and formatting commands

---

## Development Workflows

### Setting Up Development Environment

#### Python Environment
```bash
# Recommended Python version
python3.11 -m venv venv
source venv/bin/activate

# Install development tools
pip install --upgrade nox
```

#### Google Cloud Setup
```bash
# Authenticate
gcloud auth login
gcloud auth application-default login

# Set project
gcloud config set project YOUR_PROJECT_ID

# Enable required APIs
gcloud services enable aiplatform.googleapis.com
```

### Code Formatting Workflow

#### Format Changed Files (Default)
```bash
nox -s format
```
**Behavior:** Formats only files changed from the `main` branch

#### Format All Files
```bash
nox -s format -- --all
```

#### Aggressive Auto-Fixing
```bash
nox -s format -- --unsafe-fixes
```

#### Format Specific Notebook
```bash
# Manual formatting
python3 -m tensorflow_docs.tools.nbfmt notebook.ipynb
```

### Creating New Content

#### New Notebook Workflow
1. **Copy template:**
   ```bash
   cp notebook_template.ipynb gemini/{category}/{your_notebook}.ipynb
   ```

2. **Edit notebook** with required sections:
   - Title and description
   - Objectives
   - Costs (if applicable)
   - Setup and authentication
   - Main content
   - Cleaning up

3. **Format notebook:**
   ```bash
   nox -s format
   ```

4. **Test execution** (recommended before PR)

5. **Commit and push**

#### New Sample App Workflow
1. **Create directory structure:**
   ```bash
   mkdir -p gemini/sample-apps/{app-name}/{backend,frontend}
   ```

2. **Add required files:**
   - `README.md` - App description, setup, deployment
   - `requirements.txt` - Python dependencies
   - `Dockerfile` - Container definition
   - `.gcloudignore` - Files to exclude from deployment

3. **Follow existing patterns** from similar apps

4. **Test locally** before committing

5. **Add deployment documentation**

### Git Workflow

#### Branch Naming
- **Feature:** `feature/{description}`
- **Bug Fix:** `fix/{description}`
- **Documentation:** `docs/{description}`

#### Commit Message Format
```
{type}: {description} (#{issue-number})

Examples:
feat: add notebook for Vector Search 2.0 Public Preview (#2486)
fix: correct auth and bucket creation snippets (#2488)
chore: update Vertex AI SDK version (#2455)
docs: fix typos in various files (#2473)
```

**Types:** feat, fix, chore, docs, refactor, test, ci

#### Pull Request Process
1. Fork repository (external contributors)
2. Create feature branch
3. Make changes
4. Run `nox -s format`
5. Commit with descriptive message
6. Push and create PR to `main`
7. Address linting issues (GitHub Actions will check)
8. Wait for review

---

## Code Conventions & Standards

### Python Style Guide

#### Linting Configuration
**Tool:** Ruff (configured in `.ruff.toml`)
**Style:** Google Python Style Guide

**Key Rules:**
- **Line Length:** 88 characters
- **Python Version:** 3.10+ minimum
- **Import Style:** Absolute imports (no relative)
- **Quotes:** Double quotes for strings
- **Docstrings:** Google format
- **Type Hints:** Encouraged (ANN rules)

#### Docstring Format
```python
def generate_text(prompt: str, model_name: str = "gemini-2.5-pro") -> str:
    """Generates text using Gemini model.

    Args:
        prompt: The input prompt for text generation.
        model_name: Name of the Gemini model to use.

    Returns:
        Generated text response.

    Raises:
        ValueError: If prompt is empty.
    """
    if not prompt:
        raise ValueError("Prompt cannot be empty")
    # Implementation
```

#### Import Organization
```python
# Standard library
import os
import sys
from typing import Any, Optional

# Third-party
import vertexai
from vertexai.generative_models import GenerativeModel

# Local
from utils import load_config
```

#### Common Patterns to Follow

**Vertex AI Initialization:**
```python
import vertexai

PROJECT_ID = "your-project-id"
LOCATION = "us-central1"

vertexai.init(project=PROJECT_ID, location=LOCATION)
```

**Model Invocation:**
```python
from vertexai.generative_models import GenerativeModel

model = GenerativeModel("gemini-2.5-pro")
response = model.generate_content("Your prompt here")
print(response.text)
```

**Error Handling:**
```python
from google.api_core import exceptions

try:
    response = model.generate_content(prompt)
except exceptions.ResourceExhausted as e:
    print(f"Quota exceeded: {e}")
except exceptions.InvalidArgument as e:
    print(f"Invalid argument: {e}")
```

### Notebook Conventions

#### Required Sections
1. **Title and Description** (Markdown cell at top)
2. **Objectives** (What users will learn)
3. **Costs** (If applicable - link to pricing)
4. **Before you begin** (Prerequisites)
5. **Setup** (Installation and authentication)
6. **Main Content** (Tutorial steps)
7. **Cleaning Up** (Resource cleanup)

#### Code Cell Best Practices
- Keep cells focused (one concept per cell)
- Add comments for complex operations
- Use descriptive variable names
- Include expected output in comments

#### Installation Cell Format
```python
# Install required packages
!pip install --upgrade --quiet \
    google-cloud-aiplatform \
    langchain \
    langchain-google-vertexai
```

#### Authentication Cell Format
```python
# Authenticate (Colab only)
from google.colab import auth
auth.authenticate_user()

# Set project
PROJECT_ID = "your-project-id"  # @param {type:"string"}
LOCATION = "us-central1"  # @param {type:"string"}

# Initialize Vertex AI
import vertexai
vertexai.init(project=PROJECT_ID, location=LOCATION)
```

### JavaScript/TypeScript Conventions

#### Framework-Specific
- **Angular:** Follow Angular style guide
- **Next.js:** Use App Router patterns
- **Node.js:** Use ESM imports (not CommonJS)

#### Common Patterns
```typescript
// Firebase integration
import { initializeApp } from 'firebase/app';
import { getAuth } from 'firebase/auth';

// Vertex AI API calls
const response = await fetch(`https://${location}-aiplatform.googleapis.com/...`, {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(request)
});
```

---

## Common Patterns

### RAG (Retrieval Augmented Generation)

#### Basic Pattern
```python
from vertexai.generative_models import GenerativeModel, Part

# 1. Retrieve relevant context
def retrieve_context(query: str) -> list[str]:
    # Vector search or database query
    return ["context1", "context2"]

# 2. Construct prompt with context
def build_rag_prompt(query: str, contexts: list[str]) -> str:
    context_str = "\n".join(contexts)
    return f"""Based on the following context:
{context_str}

Answer the question: {query}
"""

# 3. Generate response
model = GenerativeModel("gemini-2.5-pro")
contexts = retrieve_context("What is RAG?")
prompt = build_rag_prompt("What is RAG?", contexts)
response = model.generate_content(prompt)
```

### Function Calling

#### Pattern
```python
from vertexai.generative_models import (
    FunctionDeclaration,
    GenerativeModel,
    Tool,
)

# Define function
get_weather = FunctionDeclaration(
    name="get_weather",
    description="Get weather for a location",
    parameters={
        "type": "object",
        "properties": {
            "location": {"type": "string", "description": "City name"}
        },
        "required": ["location"]
    }
)

# Create tool
weather_tool = Tool(function_declarations=[get_weather])

# Use with model
model = GenerativeModel("gemini-2.5-pro", tools=[weather_tool])
response = model.generate_content("What's the weather in London?")

# Handle function call
if response.candidates[0].function_calls:
    function_call = response.candidates[0].function_calls[0]
    # Execute function and return result
```

### Agent Pattern

#### Using Agent Engine
```python
from vertexai.preview import reasoning_engines

# Define agent
agent = reasoning_engines.LangchainAgent(
    model="gemini-2.5-pro",
    tools=[...],
    agent_executor_kwargs={"return_intermediate_steps": True}
)

# Deploy agent
deployed_agent = agent.deploy(
    display_name="my-agent",
    enable_monitoring=True
)

# Query agent
response = deployed_agent.query(
    input="Analyze sales data and create report"
)
```

### Multimodal Input

#### Pattern
```python
from vertexai.generative_models import GenerativeModel, Part

model = GenerativeModel("gemini-2.5-pro")

# Image from GCS
image_part = Part.from_uri(
    "gs://bucket/image.jpg",
    mime_type="image/jpeg"
)

# Video from GCS
video_part = Part.from_uri(
    "gs://bucket/video.mp4",
    mime_type="video/mp4"
)

# Combined prompt
response = model.generate_content([
    "Describe what's happening in this image and video:",
    image_part,
    video_part
])
```

### Fine-Tuning

#### Supervised Fine-Tuning Pattern
```python
from vertexai.preview.tuning import sft

# Prepare training data
training_data = "gs://bucket/training_data.jsonl"

# Configure tuning job
sft_job = sft.train(
    source_model="gemini-2.5-flash",
    train_dataset=training_data,
    validation_dataset="gs://bucket/validation_data.jsonl",
    epochs=3,
    learning_rate_multiplier=1.0,
)

# Monitor job
print(f"Job name: {sft_job.name}")
print(f"Job state: {sft_job.state}")

# Use tuned model
tuned_model = sft_job.tuned_model
```

### Deployment Patterns

#### Cloud Run Deployment
```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 main:app
```

```bash
# Deploy
gcloud run deploy my-app \
  --source . \
  --region us-central1 \
  --allow-unauthenticated
```

#### Cloud Function Deployment
```python
# main.py
import functions_framework
from vertexai.generative_models import GenerativeModel

@functions_framework.http
def generate(request):
    model = GenerativeModel("gemini-2.5-flash")
    prompt = request.get_json().get("prompt", "")
    response = model.generate_content(prompt)
    return {"response": response.text}
```

---

## Testing Strategy

### Current State
- **Notebook Testing:** Automated execution via Cloud Build
- **Unit Tests:** Limited (primarily in sample apps)
- **Integration Tests:** Ad-hoc (not standardized)

### Testing Locations
```
gemini/sample-apps/{app}/tests/
gemini/sample-apps/swot-agent/tests/
gemini/sample-apps/llamaindex-rag/backend/tests/
```

### Recommended Testing Patterns

#### Unit Test Pattern
```python
# tests/test_utils.py
import pytest
from utils import build_prompt

def test_build_prompt():
    result = build_prompt("test query", ["context1"])
    assert "test query" in result
    assert "context1" in result

def test_build_prompt_empty():
    with pytest.raises(ValueError):
        build_prompt("", [])
```

#### Notebook Testing
- **Manual:** Execute all cells and verify outputs
- **Automated:** Cloud Build executes notebooks in test environments
- **Validation:** Check for errors, verify key outputs

#### Integration Testing Considerations
- **Cost:** Vertex AI API calls cost money
- **Quotas:** May hit rate limits
- **Nondeterminism:** LLM outputs vary
- **Solution:** Use smaller models, cache results, test logic not outputs

---

## Deployment Patterns

### Infrastructure as Code

#### Terraform Pattern
```hcl
# terraform/main.tf
resource "google_cloud_run_service" "default" {
  name     = "genai-app"
  location = "us-central1"

  template {
    spec {
      containers {
        image = "gcr.io/${var.project_id}/genai-app:latest"
        env {
          name  = "PROJECT_ID"
          value = var.project_id
        }
      }
    }
  }
}
```

### Multi-Service Deployments

#### Docker Compose Pattern
```yaml
# docker-compose.yml
version: '3.8'
services:
  backend:
    build: ./backend
    environment:
      - PROJECT_ID=${PROJECT_ID}
    ports:
      - "8080:8080"

  frontend:
    build: ./frontend
    ports:
      - "4200:4200"
    depends_on:
      - backend
```

### Deployment Scripts

#### Common Pattern
```bash
#!/bin/bash
# deploy.sh

set -e

PROJECT_ID=${1:-$(gcloud config get-value project)}
REGION=${2:-us-central1}

echo "Deploying to project: $PROJECT_ID"

# Build container
gcloud builds submit --tag gcr.io/$PROJECT_ID/app

# Deploy to Cloud Run
gcloud run deploy app \
  --image gcr.io/$PROJECT_ID/app \
  --region $REGION \
  --platform managed \
  --allow-unauthenticated

echo "Deployment complete!"
```

---

## Troubleshooting Guide

### Common Issues and Solutions

#### 1. Authentication Errors

**Error:** `google.auth.exceptions.DefaultCredentialsError`

**Solutions:**
```bash
# Option 1: Application Default Credentials
gcloud auth application-default login

# Option 2: Service Account
export GOOGLE_APPLICATION_CREDENTIALS="/path/to/key.json"

# Option 3: Colab
from google.colab import auth
auth.authenticate_user()
```

#### 2. Quota Exceeded

**Error:** `google.api_core.exceptions.ResourceExhausted: 429 Quota exceeded`

**Solutions:**
- Check quotas: Cloud Console → IAM & Admin → Quotas
- Request quota increase
- Use smaller models (flash instead of pro)
- Implement rate limiting
- Add retry logic with exponential backoff

```python
from google.api_core import retry

@retry.Retry(predicate=retry.if_exception_type(exceptions.ResourceExhausted))
def generate_with_retry(prompt):
    return model.generate_content(prompt)
```

#### 3. Module Not Found

**Error:** `ModuleNotFoundError: No module named 'vertexai'`

**Solutions:**
```bash
# Install missing package
pip install --upgrade google-cloud-aiplatform

# Install all requirements
pip install -r requirements.txt

# Clear cache and reinstall
pip cache purge
pip install --upgrade --force-reinstall google-cloud-aiplatform
```

#### 4. Linting Failures

**Error:** Ruff linting failures in PR

**Solutions:**
```bash
# Run formatter locally
nox -s format

# Check specific file
ruff check path/to/file.py

# Auto-fix issues
ruff check --fix path/to/file.py

# Aggressive fixes
nox -s format -- --unsafe-fixes
```

#### 5. Notebook Execution Errors

**Common Issues:**
- Outdated SDK version
- Missing environment variables
- Incorrect project ID
- API not enabled

**Debugging Steps:**
1. Check Python version: `python --version` (should be 3.10+)
2. Verify SDK version: `pip show google-cloud-aiplatform`
3. Confirm project setup: `gcloud config list`
4. Enable required APIs:
   ```bash
   gcloud services enable aiplatform.googleapis.com
   ```

#### 6. Sample App Deployment Failures

**Common Issues:**
- Missing environment variables
- Insufficient permissions
- Resource naming conflicts
- Region availability

**Debugging:**
```bash
# Check logs
gcloud run services logs read SERVICE_NAME --region REGION

# Describe service
gcloud run services describe SERVICE_NAME --region REGION

# Check IAM permissions
gcloud projects get-iam-policy PROJECT_ID
```

---

## AI Assistant Best Practices

### When Helping Users

#### 1. Understand Context First
- Check which directory user is working in
- Review relevant README files
- Identify which model/API is being used
- Check for existing similar examples

#### 2. Follow Repository Conventions
- Use correct naming conventions
- Match existing code style
- Include proper docstrings
- Add necessary comments

#### 3. Provide Complete Solutions
- Don't just show code snippets
- Include necessary imports
- Add error handling
- Suggest testing approach

#### 4. Consider Costs
- Warn about expensive operations
- Suggest cost-effective alternatives
- Recommend cleanup procedures
- Note quota requirements

#### 5. Recommend Best Practices
- Security (don't hardcode credentials)
- Error handling (graceful failures)
- Resource cleanup (avoid orphaned resources)
- Logging (for debugging)

### Code Generation Guidelines

#### Always Include:
```python
# 1. Proper imports
import vertexai
from vertexai.generative_models import GenerativeModel

# 2. Configuration
PROJECT_ID = "your-project-id"  # Update this
LOCATION = "us-central1"

# 3. Initialization
vertexai.init(project=PROJECT_ID, location=LOCATION)

# 4. Error handling
try:
    # Main logic
    model = GenerativeModel("gemini-2.5-pro")
    response = model.generate_content(prompt)
except Exception as e:
    print(f"Error: {e}")
    # Handle appropriately

# 5. Resource cleanup (if applicable)
# Close connections, delete temporary resources
```

#### Security Checklist:
- ✅ Never hardcode API keys or credentials
- ✅ Use environment variables or Secret Manager
- ✅ Validate user inputs
- ✅ Sanitize outputs
- ✅ Follow principle of least privilege
- ✅ Enable audit logging for production

### Documentation Standards

#### When Creating Examples:
1. **Purpose:** Start with what the example demonstrates
2. **Prerequisites:** List required setup
3. **Step-by-Step:** Break down complex operations
4. **Explanation:** Explain why, not just what
5. **Variations:** Show alternative approaches
6. **Gotchas:** Highlight common mistakes
7. **Resources:** Link to relevant documentation

#### Example Structure:
```markdown
# Example: RAG with BigQuery

## Purpose
Demonstrates how to implement RAG using BigQuery as the data source.

## Prerequisites
- Google Cloud project with billing enabled
- BigQuery dataset with sample data
- Vertex AI API enabled

## Setup
\```python
# Installation
!pip install google-cloud-aiplatform google-cloud-bigquery
\```

## Implementation

### Step 1: Connect to BigQuery
\```python
from google.cloud import bigquery
client = bigquery.Client(project=PROJECT_ID)
\```

[More steps...]

## Common Issues
- **Quota errors:** Reduce batch size
- **Authentication:** Ensure ADC is configured

## Next Steps
- Try with your own dataset
- Implement caching for better performance
- Add error handling for production
```

### Debugging Support

#### Systematic Approach:
1. **Understand the Error**
   - What's the error message?
   - When does it occur?
   - What's the expected behavior?

2. **Check Basics**
   - Is authentication configured?
   - Are APIs enabled?
   - Is the SDK version compatible?

3. **Review Configuration**
   - Correct project ID?
   - Right region?
   - Valid resource names?

4. **Examine Code**
   - Recent changes?
   - Missing dependencies?
   - Syntax errors?

5. **Test Incrementally**
   - Simplify to minimal example
   - Add logging
   - Test each component

6. **Consult Documentation**
   - Check CLAUDE.md (this file)
   - Review relevant README
   - Search for similar examples

### Recommending Examples

When users ask "how do I...", recommend existing examples:

**User Query → Example Path Mapping:**

| User Wants To... | Recommend |
|-----------------|-----------|
| Get started with Gemini | `gemini/getting-started/intro_gemini_2_5_pro.ipynb` |
| Implement RAG | `gemini/rag-engine/` or `search/retrieval-augmented-generation/` |
| Build an agent | `gemini/agent-engine/` or `agents/adk/` |
| Use function calling | `gemini/function-calling/` |
| Generate images | `vision/getting-started/` |
| Fine-tune a model | `gemini/tuning/` or `open-models/fine-tuning/` |
| Deploy to Cloud Run | Look for `Dockerfile` in relevant sample apps |
| Evaluate model performance | `gemini/evaluation/` or `tools/llmevalkit/` |

### Performance Optimization

#### Recommendations:
1. **Model Selection**
   - Use Flash for faster/cheaper responses
   - Use Pro for complex reasoning
   - Consider context window size

2. **Caching**
   - Use context caching for repeated contexts
   - Cache embeddings for large documents
   - Store expensive API responses

3. **Batching**
   - Batch API calls when possible
   - Use async for parallel operations
   - Implement request queuing

4. **Cost Optimization**
   - Monitor token usage
   - Implement prompt compression
   - Use smaller models when appropriate
   - Clean up unused resources

---

## Quick Reference

### Essential Commands

```bash
# Format code
nox -s format

# Format all files
nox -s format -- --all

# Aggressive auto-fix
nox -s format -- --unsafe-fixes

# Deploy Cloud Run app
gcloud run deploy APP_NAME --source . --region us-central1

# Enable Vertex AI API
gcloud services enable aiplatform.googleapis.com

# Set project
gcloud config set project PROJECT_ID

# Authenticate
gcloud auth application-default login
```

### File Paths Cheat Sheet

```
README.md                              → Main documentation
CONTRIBUTING.md                        → Contribution guide
CLAUDE.md                             → AI assistant guide (this file)
UPDATES.md                            → Repository status report
notebook_template.ipynb               → Template for notebooks
noxfile.py                            → Automation scripts
.ruff.toml                            → Linting configuration
.github/workflows/                    → CI/CD workflows
gemini/getting-started/               → Gemini introduction
gemini/sample-apps/                   → Full applications
vision/getting-started/               → Image/video generation
search/retrieval-augmented-generation/ → RAG examples
agents/adk/                           → Agent Development Kit
```

### API Version References

**Current Model Versions (as of 2025-11-16):**
- Gemini 2.5 Pro: `gemini-2.5-pro`
- Gemini 2.5 Flash: `gemini-2.5-flash`
- Gemini 1.5 Pro: `gemini-1.5-pro`
- Imagen 4: `imagen-4.0-generate-preview`
- Imagen 3: `imagen-3.0-generate-001`

**Recommended SDK Versions:**
- `google-cloud-aiplatform >= 1.40.0`
- Python: `3.10+`
- Vertex AI API version: `v1` (stable) or `v1beta1` (preview features)

### Common Environment Variables

```bash
# Required
export PROJECT_ID="your-project-id"
export LOCATION="us-central1"

# Optional but recommended
export GOOGLE_APPLICATION_CREDENTIALS="/path/to/key.json"
export VERTEX_AI_LOCATION="us-central1"
```

### Links to Key Documentation

- [Vertex AI Documentation](https://cloud.google.com/vertex-ai/docs)
- [Gemini API Reference](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/gemini)
- [Google Cloud SDK](https://cloud.google.com/sdk/docs)
- [Repository Issues](https://github.com/GoogleCloudPlatform/generative-ai/issues)
- [Repository README](README.md)
- [Contribution Guide](CONTRIBUTING.md)

---

## Maintenance

### Keeping This Document Updated

**When to Update:**
- New major features added to repository
- Structural changes to directory organization
- Changes to development workflows
- New code conventions adopted
- Common issues discovered

**Update Process:**
1. Edit CLAUDE.md
2. Update "Last Updated" date at top
3. Increment version number if major changes
4. Commit with message: `docs: update CLAUDE.md`
5. Consider updating UPDATES.md if significant changes

**Version History:**
- v1.0.0 (2025-11-16): Initial creation

---

## Feedback

### For Users
If you find this guide helpful or have suggestions:
- Open an issue: [GitHub Issues](https://github.com/GoogleCloudPlatform/generative-ai/issues)
- Tag with `documentation` label

### For AI Assistants
If you (AI assistant) encounter:
- Missing information you need frequently
- Patterns not documented here
- Outdated information
- Suggest updates in your responses to users

---

**Remember:** This is a living document. As the repository evolves, this guide should evolve with it. The goal is to enable AI assistants to provide accurate, helpful, and contextually appropriate support to developers working with Google Cloud's generative AI platform.
