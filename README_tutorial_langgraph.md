# LangGraph Application on Vertex AI Agent Engine

## Overview

This tutorial demonstrates how to build, deploy, and test a LangGraph application using Agent Engine in Vertex AI. LangGraph is a library for building stateful, multi-actor applications with LLMs, used to create agent and multi-agent workflows. The tutorial shows how to combine LangGraph's workflow orchestration with the scalability of Vertex AI.

## What You'll Learn

- Define custom tools for AI applications
- Set up routing logic for conversation flow control
- Build a LangGraph application with Gemini integration
- Test applications locally before deployment
- Deploy to Vertex AI Agent Engine for scalable execution
- Test deployed applications remotely
- Clean up cloud resources properly

## Key Features

- **Custom Application Template**: Uses Agent Engine's customized template approach
- **LangGraph Integration**: Leverages LangGraph for workflow orchestration
- **Gemini 2.0 Flash**: Utilizes Google's latest language model
- **Tool Integration**: Demonstrates custom function integration as tools
- **Production Deployment**: Scalable deployment on Google Cloud infrastructure

## Prerequisites

- Google Cloud Project with Vertex AI API enabled
- Python environment with required packages
- Basic understanding of LangGraph and AI agents
- Familiarity with Google Cloud services

## Architecture Components

### Core Libraries
- **LangGraph**: Workflow orchestration and state management
- **LangChain**: Core messaging and tool integration
- **Vertex AI SDK**: Google Cloud AI platform integration
- **ChatVertexAI**: Gemini model interface

### Application Structure
1. **Tools Definition**: Custom Python functions that serve as agent capabilities
2. **Router Logic**: Controls conversation flow and tool selection
3. **LangGraph Application**: Orchestrates the entire workflow
4. **Agent Engine Deployment**: Managed cloud deployment

## Getting Started

### 1. Environment Setup
```bash
pip install --upgrade "google-cloud-aiplatform[agent_engines,langchain]" \
    cloudpickle==3.0.0 \
    "pydantic==2.11.2" \
    langgraph \
    httpx
```

### 2. Configure Google Cloud
- Set PROJECT_ID and LOCATION
- Configure staging bucket
- Initialize Vertex AI SDK

### 3. Define Custom Tools
The tutorial includes a sample product details tool:
```python
def get_product_details(product_name: str):
    """Gathers basic details about a product."""
    # Returns product information for various items
```

### 4. Implement Router Logic
```python
def router(state: list[BaseMessage]) -> Literal["get_product_details", "__end__"]:
    """Controls conversation flow based on tool calls"""
```

### 5. Build LangGraph Application
The `SimpleLangGraphApp` class demonstrates:
- Model initialization with tool binding
- Graph construction with nodes and edges
- Conversation flow management
- Query processing

## Application Workflow

1. **User Input**: Application receives user message
2. **Model Processing**: Gemini model processes input with available tools
3. **Tool Selection**: Router determines appropriate tool to call
4. **Tool Execution**: Selected tool executes and returns results
5. **Response Generation**: Final response generated and returned

## Local Testing

Before deployment, the tutorial demonstrates local testing:
```python
agent = SimpleLangGraphApp(project=PROJECT_ID, location=LOCATION)
agent.set_up()
response = agent.query(message="Get product details for shoes")
```

## Deployment to Agent Engine

Deploy to Vertex AI with required dependencies:
```python
remote_agent = agent_engines.create(
    SimpleLangGraphApp(project=PROJECT_ID, location=LOCATION),
    requirements=[
        "google-cloud-aiplatform[agent_engines,langchain]",
        "cloudpickle==3.0.0",
        "pydantic==2.11.2",
        "langgraph",
        "httpx",
    ],
    display_name="Agent Engine with LangGraph",
    description="Sample custom application using LangGraph"
)
```

## Remote Testing

After deployment, test the remote agent:
```python
response = remote_agent.query(message="Get product details for shoes")
```

## Sample Interactions

The application handles various queries:
- **Product Information**: "Get product details for shoes" → Returns product description
- **Multiple Products**: Supports queries for smartphones, coffee, headphones, speakers
- **Out of Scope**: "Tell me about the weather" → Politely declines with explanation

## Key Benefits

1. **Scalability**: Agent Engine provides managed, scalable infrastructure
2. **Flexibility**: Custom application template supports any framework
3. **Integration**: Seamless integration with Google Cloud services
4. **Testing**: Local testing capabilities before deployment
5. **Monitoring**: Built-in logging and monitoring through Google Cloud Console

## Advanced Features

- **Multi-Agent Workflows**: Can be extended for complex multi-agent scenarios
- **State Management**: LangGraph provides sophisticated state handling
- **Custom Logic**: Router can implement complex decision-making logic
- **Tool Chaining**: Support for sequential tool calls
- **Error Handling**: Graceful handling of unsupported requests

## Use Cases

- Product information systems
- Customer support automation
- Knowledge base querying
- Multi-step workflow automation
- Interactive AI assistants

## File Structure

The notebook provides a complete implementation example:
1. Environment setup and dependencies
2. Tool and router definitions
3. LangGraph application implementation
4. Local testing procedures
5. Deployment configuration
6. Remote testing validation
7. Resource cleanup

This tutorial serves as a foundation for building sophisticated AI applications that require stateful, multi-step interactions with custom business logic integration.