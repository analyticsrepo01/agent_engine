# Agent Engine Tutorials and Examples

This repository contains comprehensive tutorials and examples for building, deploying, and evaluating AI agents using Google Cloud's Vertex AI Agent Engine. The tutorials cover multiple frameworks and approaches for creating sophisticated AI applications.

## Overview

Vertex AI Agent Engine is a managed service that helps you build and deploy agent frameworks at scale. This repository demonstrates three different approaches to agent development:

1. **CrewAI with Evaluation** - Building and comprehensively evaluating CrewAI agents
2. **LangGraph Integration** - Creating stateful, multi-actor applications with workflow orchestration
3. **Agent Development Kit (ADK)** - Simplified agent creation and deployment

## Repository Contents

### 📓 Tutorials

| Notebook | Framework | Description | README |
|----------|-----------|-------------|---------|
| `tutorial_crewai_agent_engine.ipynb` | CrewAI | Agent evaluation with Vertex AI Gen AI Evaluation | [README](README_tutorial_crewai_agent_engine.md) |
| `tutorial_langgraph.ipynb` | LangGraph | Building stateful multi-actor applications | [README](README_tutorial_langgraph.md) |
| `Deploy_ADK_agent.ipynb` | ADK | Simplified agent development and deployment | [README](README_Deploy_ADK_agent.md) |

## Tutorial Summaries

### 1. CrewAI Agent Evaluation Tutorial

**Focus**: Comprehensive agent evaluation and testing methodologies

**Key Features**:
- Build agents using CrewAI framework
- Deploy to Vertex AI Agent Engine with custom templates
- Comprehensive evaluation using Vertex AI Gen AI Evaluation
- Multiple evaluation types: single tool usage, trajectory analysis, response quality
- Custom evaluation metrics and visualization

**What You'll Learn**:
- Agent building with CrewAI and Gemini models
- Evaluation dataset preparation and structure
- Single tool usage evaluation techniques
- Trajectory evaluation (tool sequence analysis)
- Response quality assessment
- Custom metric development
- Bring-your-own-dataset scenarios

**Use Cases**: Customer support agents, product recommendation systems, multi-step workflow automation

### 2. LangGraph Application Tutorial

**Focus**: Stateful, multi-actor applications with workflow orchestration

**Key Features**:
- LangGraph for complex workflow management
- Custom tool definition and integration
- Conversation flow control with routers
- Local testing before deployment
- Scalable cloud deployment

**What You'll Learn**:
- LangGraph application architecture
- Custom tool development
- Router logic implementation
- Message graph construction
- State management in conversations
- Production deployment strategies

**Use Cases**: Interactive AI assistants, multi-step automation, knowledge base querying, complex decision workflows

### 3. ADK Agent Deployment Tutorial

**Focus**: Simplified agent development with Google's Agent Development Kit

**Key Features**:
- Streamlined agent creation process
- Built-in tool integration
- Automatic deployment capabilities
- Structured response handling
- Error management

**What You'll Learn**:
- ADK framework basics
- Quick agent setup and configuration
- Custom tool implementation
- Deployment to Agent Engine
- Testing and validation procedures

**Use Cases**: Information services, customer support automation, API integration wrappers, specialized assistants

## Common Prerequisites

- **Google Cloud Project** with Vertex AI API enabled
- **Python Environment** with required packages
- **Basic Understanding** of AI agents and Google Cloud services
- **Familiarity** with Python programming

## Getting Started

### 1. Environment Setup

Choose the appropriate installation based on your tutorial:

**For CrewAI Tutorial**:
```bash
pip install --upgrade "google-cloud-aiplatform[agent_engines,evaluation]" \
    "crewai" "crewai-tools" "cloudpickle==3.0.0" "pydantic>=2.10"
```

**For LangGraph Tutorial**:
```bash
pip install --upgrade "google-cloud-aiplatform[agent_engines,langchain]" \
    "cloudpickle==3.0.0" "pydantic==2.11.2" "langgraph" "httpx"
```

**For ADK Tutorial**:
```bash
pip install google-cloud-aiplatform[adk,agent_engines]
```

### 2. Configure Google Cloud

```python
PROJECT_ID = "your-project-id"
LOCATION = "us-central1"
STAGING_BUCKET = "gs://your-staging-bucket"

import vertexai
vertexai.init(project=PROJECT_ID, location=LOCATION, staging_bucket=STAGING_BUCKET)
```

### 3. Choose Your Tutorial

Select the tutorial that best fits your needs:
- **New to agent evaluation?** Start with the CrewAI tutorial
- **Need complex workflows?** Try the LangGraph tutorial  
- **Want quick deployment?** Use the ADK tutorial

## Key Concepts

### Agent Engine Features
- **Managed Infrastructure**: Scalable, serverless agent deployment
- **Multiple Frameworks**: Support for CrewAI, LangGraph, ADK, and custom templates
- **Built-in Monitoring**: Logging and observability through Google Cloud Console
- **Auto-scaling**: Automatic resource scaling based on demand

### Evaluation Methodologies
- **Single Tool Evaluation**: Validate correct tool selection
- **Trajectory Analysis**: Assess tool sequence and order
- **Response Quality**: Evaluate output coherence and safety
- **Custom Metrics**: Domain-specific evaluation criteria

### Deployment Options
- **Local Testing**: Validate functionality before deployment
- **Custom Templates**: Support for any Python-based framework
- **Dependency Management**: Automatic handling of requirements and packages
- **Resource Management**: Built-in lifecycle management

## Architecture Patterns

### Tool-Based Agents
All tutorials demonstrate tool-based agent patterns:
- **Custom Functions**: Python functions as agent capabilities
- **Structured Responses**: Consistent response formats
- **Error Handling**: Graceful failure management
- **Tool Chaining**: Sequential tool execution

### Deployment Patterns
- **Local Development**: Test and iterate locally
- **Cloud Deployment**: Deploy to managed infrastructure
- **Remote Testing**: Validate cloud-deployed agents
- **Resource Cleanup**: Proper resource management

## Advanced Features

### Evaluation and Monitoring
- **Real-time Evaluation**: Online performance monitoring
- **Batch Evaluation**: Large-scale dataset evaluation
- **Custom Metrics**: Domain-specific evaluation criteria
- **Visualization**: Built-in plotting and reporting

### Scalability and Performance
- **Auto-scaling**: Demand-based resource allocation
- **Caching**: Response caching for improved performance
- **Load Balancing**: Distributed request handling
- **Monitoring**: Comprehensive observability

## Best Practices

1. **Development Workflow**:
   - Start with local testing
   - Use appropriate evaluation methods
   - Deploy incrementally
   - Monitor performance continuously

2. **Tool Design**:
   - Create focused, single-purpose tools
   - Implement comprehensive error handling
   - Use consistent response formats
   - Document tool capabilities clearly

3. **Evaluation Strategy**:
   - Prepare diverse evaluation datasets
   - Use multiple evaluation metrics
   - Implement custom metrics for domain-specific needs
   - Visualize results for better insights

4. **Production Deployment**:
   - Test thoroughly before deployment
   - Monitor resource usage
   - Implement proper error handling
   - Plan for scaling requirements

## Contributing

When contributing to this repository:
1. Follow the established tutorial structure
2. Include comprehensive documentation
3. Provide working code examples
4. Test all examples thoroughly
5. Update relevant README files

## Support and Resources

- **Documentation**: [Vertex AI Agent Engine Docs](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
- **Samples**: [Official Google Cloud Samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples)
- **Community**: [Google Cloud Community](https://cloud.google.com/community)

## License

This project follows the Apache 2.0 License as indicated in the notebook headers.

---

*These tutorials provide a comprehensive foundation for building production-ready AI agents using Google Cloud's Vertex AI platform. Each approach offers different advantages depending on your specific use case and requirements.*