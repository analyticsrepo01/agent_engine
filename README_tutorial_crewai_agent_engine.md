# CrewAI Agent Evaluation on Vertex AI Agent Engine

## Overview

This tutorial demonstrates how to evaluate a CrewAI agent with customized template on Vertex AI Agent Engine using Vertex AI Gen AI Evaluation. The tutorial covers building, deploying, and comprehensively evaluating AI agents to ensure reliable and effective performance.

## What You'll Learn

- Build and deploy an agent using CrewAI on Vertex AI Agent Engine
- Prepare Agent Evaluation datasets
- Perform single tool usage evaluation
- Conduct trajectory evaluation (tool sequence analysis)
- Evaluate response quality and coherence
- Create custom evaluation metrics

## Prerequisites

- Google Cloud Project with Vertex AI API enabled
- Python environment with required packages
- Basic understanding of AI agents and evaluation concepts

## Key Components

### Agent Architecture
- **CrewAI Framework**: Used to build the agent application
- **Custom Tools**: Product details and pricing functions
- **Gemini Model**: vertex_ai/gemini-2.0-flash for LLM capabilities
- **Agent Engine**: Vertex AI's managed service for agent deployment

### Evaluation Types

1. **Single Tool Usage Evaluation**
   - Validates if agent selects correct tools for given tasks
   - Uses `TrajectorySingleToolUse` metric

2. **Trajectory Evaluation**
   - Analyzes tool sequence choices and order
   - Metrics include:
     - `trajectory_exact_match`: Identical trajectories
     - `trajectory_in_order_match`: Reference actions present in order
     - `trajectory_any_order_match`: All reference actions present
     - `trajectory_precision`: Proportion of predicted actions in reference
     - `trajectory_recall`: Proportion of reference actions in predicted

3. **Response Evaluation**
   - Evaluates final agent responses
   - Metrics include safety, coherence, and custom criteria

4. **Custom Metrics**
   - Response follows trajectory logic
   - Custom prompt templates for specialized evaluation

## Getting Started

### 1. Environment Setup
```bash
pip install --upgrade "google-cloud-aiplatform[agent_engines,evaluation]" \
    "crewai" "crewai-tools" \
    "cloudpickle==3.0.0" \
    "pydantic>=2.10" \
    "requests" "crewai_tools"
```

### 2. Configure Google Cloud
- Set up PROJECT_ID and LOCATION
- Initialize Vertex AI SDK
- Create storage bucket for staging

### 3. Define Tools
The tutorial includes sample tools for product information:
- `get_product_details()`: Retrieves product descriptions
- `get_product_price()`: Gets product pricing information

### 4. Build CrewAI Application
Create a custom application class that:
- Initializes agents with specific roles and tools
- Defines tasks for product research
- Implements query processing logic

### 5. Deploy to Agent Engine
Deploy the local agent to Vertex AI Agent Engine for scalable execution.

### 6. Evaluation Process
Create evaluation datasets with:
- User prompts
- Reference trajectories (expected tool sequences)
- Ground truth responses (optional)

Run evaluations using `EvalTask` with various metrics to assess agent performance.

## Evaluation Dataset Structure

```python
eval_data = {
    "prompt": ["Get price for smartphone", ...],
    "reference_trajectory": [
        [{"tool_name": "get_product_price", "tool_input": {"product_name": "smartphone"}}],
        ...
    ]
}
```

## Key Features

- **Comprehensive Evaluation**: Multiple evaluation types covering tool selection, trajectory analysis, and response quality
- **Custom Metrics**: Ability to define domain-specific evaluation criteria
- **Bring-Your-Own-Dataset**: Support for pre-generated responses and trajectories
- **Visualization**: Built-in plotting and reporting capabilities
- **Production Ready**: Scalable deployment on Vertex AI infrastructure

## Use Cases

- Customer support agents
- Product recommendation systems
- Multi-step workflow automation
- Decision-making applications requiring tool orchestration

## File Structure

The notebook is organized into clear sections:
1. Environment setup and authentication
2. Agent building and local testing
3. Deployment to Agent Engine
4. Evaluation dataset preparation
5. Various evaluation methodologies
6. Results visualization and analysis
7. Cleanup procedures

This tutorial provides a complete framework for building, deploying, and evaluating CrewAI agents in production environments using Google Cloud's Vertex AI platform.