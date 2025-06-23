# Deploy ADK Agent to Vertex AI Agent Engine

## Overview

This tutorial demonstrates how to deploy an Agent Development Kit (ADK) agent to Vertex AI Agent Engine. The ADK provides a simplified framework for building AI agents with custom tools and deploying them to Google Cloud's managed infrastructure for scalable execution.

## What You'll Learn

- Create AI agents using Google's Agent Development Kit (ADK)
- Define custom tools for specific functionalities
- Deploy agents to Vertex AI Agent Engine
- Test deployed agents remotely
- Manage agent lifecycle and resources

## Key Components

### Agent Development Kit (ADK)
- **Simplified Framework**: Streamlined approach to agent creation
- **Built-in Tools Support**: Easy integration of custom Python functions
- **Gemini Integration**: Uses Gemini 2.0 Flash model by default
- **Deployment Ready**: Designed for seamless cloud deployment

### Sample Agent Features
- **Weather Information**: Get current weather reports for cities
- **Time Services**: Retrieve current time in different timezones
- **Error Handling**: Graceful handling of unsupported locations
- **Structured Responses**: Consistent response format with status and results

## Prerequisites

- Google Cloud Project with Vertex AI API enabled
- Agent Development Kit package installed
- Basic Python programming knowledge
- Understanding of AI agent concepts

## Getting Started

### 1. Installation
```bash
pip install google-cloud-aiplatform[adk,agent_engines]
```

### 2. Environment Configuration
```python
import os
PROJECT_ID = "your-project-id"
LOCATION = "us-central1"
STAGING_BUCKET = "gs://your-staging-bucket"

os.environ["GOOGLE_CLOUD_PROJECT"] = PROJECT_ID
os.environ["GOOGLE_CLOUD_LOCATION"] = LOCATION
os.environ["GOOGLE_GENAI_USE_VERTEXAI"] = "TRUE"
```

### 3. Initialize Vertex AI
```python
import vertexai
vertexai.init(
    project=PROJECT_ID,
    location=LOCATION,
    staging_bucket=STAGING_BUCKET,
)
```

## Agent Implementation

### Define Custom Tools

The tutorial includes two example tools:

#### Weather Tool
```python
def get_weather(city: str) -> dict:
    """Retrieves the current weather report for a specified city."""
    if city.lower() == "new york":
        return {
            "status": "success",
            "report": "The weather in New York is sunny with a temperature of 25°C (77°F)."
        }
    else:
        return {
            "status": "error",
            "error_message": f"Weather information for '{city}' is not available."
        }
```

#### Time Tool
```python
def get_current_time(city: str) -> dict:
    """Returns the current time in a specified city."""
    if city.lower() == "new york":
        # Returns formatted time with timezone information
    else:
        return {
            "status": "error",
            "error_message": f"Sorry, I don't have timezone information for {city}."
        }
```

### Create Agent

```python
from google.adk.agents import Agent

root_agent = Agent(
    name="weather_time_agent",
    model="gemini-2.0-flash",
    description="Agent to answer questions about the time and weather in a city.",
    instruction="You are a helpful agent who can answer user questions about the time and weather in a city.",
    tools=[get_weather, get_current_time],
)
```

## Deployment Process

### Deploy to Agent Engine

```python
from vertexai import agent_engines

remote_app = agent_engines.create(
    agent_engine=root_agent,
    requirements=[
        "google-cloud-aiplatform[adk,agent_engines]"   
    ]
)
```

The deployment process includes:
1. **Package Preparation**: Automatically packages agent code and dependencies
2. **Container Creation**: Builds deployment container with required libraries
3. **Resource Provisioning**: Allocates cloud resources for agent execution
4. **Service Registration**: Makes agent available through Agent Engine API

## Agent Capabilities

### Supported Queries
- **Weather Information**: "What's the weather in New York?"
- **Time Queries**: "What time is it in New York?"
- **Combined Requests**: Can handle multiple information requests

### Response Format
All responses follow a consistent structure:
```python
{
    "status": "success" | "error",
    "report": "response content",  # for successful requests
    "error_message": "error details"  # for failed requests
}
```

## Key Features

1. **Simplified Development**: ADK abstracts complex agent setup
2. **Automatic Deployment**: Streamlined deployment to cloud infrastructure
3. **Scalable Execution**: Managed scaling based on demand
4. **Integrated Monitoring**: Built-in logging and monitoring capabilities
5. **Error Handling**: Robust error handling and reporting

## Use Cases

- **Information Services**: Weather, time, and location-based services
- **Customer Support**: Automated query handling with specific tools
- **API Integration**: Wrapper agents for external service integration
- **Specialized Assistants**: Domain-specific AI assistants

## Best Practices

1. **Tool Design**: Create focused, single-purpose tools
2. **Error Handling**: Implement comprehensive error responses
3. **Input Validation**: Validate and sanitize tool inputs
4. **Response Consistency**: Use consistent response formats
5. **Documentation**: Clear tool descriptions for better model understanding

## Limitations and Considerations

- **Geographic Scope**: Sample tools limited to specific cities
- **Static Data**: Example uses hardcoded responses
- **Timezone Handling**: Limited timezone support in example
- **Scalability**: Consider tool complexity for production deployment

## Extension Opportunities

The basic framework can be extended with:
- **Real API Integration**: Connect to actual weather and time services
- **Database Integration**: Store and retrieve dynamic information
- **Multi-language Support**: Internationalization capabilities
- **Advanced Error Handling**: More sophisticated error recovery
- **Caching**: Implement response caching for better performance

## File Structure

The notebook demonstrates:
1. Environment setup and configuration
2. Tool definition and implementation
3. Agent creation with ADK
4. Deployment to Agent Engine
5. Testing and validation procedures

This tutorial provides a foundation for building production-ready AI agents using Google's Agent Development Kit and Vertex AI infrastructure.