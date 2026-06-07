# Research Agent

An intelligent, autonomous research assistant built with LangGraph ReAct architecture, powered by Meta LLaMA 3.2 on IBM Watsonx AI, and deployed on IBM Cloud. The agent searches the web, retrieves academic information, synthesizes findings from multiple sources, and generates structured research reports — all through a conversational interface with streaming support.

Built as the capstone project for the AICTE Internship with IBM SkillsBuild x Edunet Foundation (July–August 2025).

---

## Features

- **ReAct Agent Architecture** — autonomous reasoning and tool selection via LangGraph's `create_react_agent`
- **Multi-Source Search** — integrates GoogleSearch, DuckDuckGo, Wikipedia, and WebCrawler tools from the IBM Watsonx AI Toolkit
- **Research Summarization** — understands natural language questions and retrieves structured, relevant information
- **Report Generation** — drafts organized research summaries and suggests hypotheses
- **Streaming Responses** — real-time token-by-token output via `generate_stream()`
- **Conversation Memory** — multi-turn session memory using LangGraph's `MemorySaver`
- **IBM Cloud Deployment** — runs as a production service on IBM Watsonx AI (US South)

---

## Project Structure

```
research_agent/
├── RESEARCH AGENT/
│   └── Research_Agent.ipynb    # Main notebook — agent setup, tools, streaming, and demos
└── README.md
```

---

## Tech Stack

| Layer             | Technology                                          |
|-------------------|-----------------------------------------------------|
| LLM               | Meta LLaMA 3.2 (11B Vision Instruct)                |
| Agent Framework   | LangGraph (ReAct)                                   |
| LLM Integration   | LangChain IBM / ChatWatsonx                         |
| Tools             | IBM Watsonx AI Toolkit (GoogleSearch, DuckDuckGo, Wikipedia, WebCrawler) |
| Deployment        | IBM Watsonx AI — IBM Cloud (us-south)               |
| Language          | Python (Jupyter Notebook)                           |

---

## Architecture

```
User Query
    |
    v
ReAct Agent (LangGraph)
    |
    |---> GoogleSearch Tool
    |---> DuckDuckGo Tool
    |---> Wikipedia Tool
    |---> WebCrawler Tool
    |
    v
LLaMA 3.2 via IBM Watsonx AI
    |
    v
Structured Research Response (streamed)
```

The agent follows the Reasoning + Acting (ReAct) loop:

1. Receives a research question
2. Reasons about which tool is most appropriate
3. Acts by calling the selected search or crawl tool
4. Observes the result
5. Repeats until sufficient information is gathered
6. Returns a comprehensive, formatted response

---

## Getting Started

### Prerequisites

- Python 3.8+
- An IBM Cloud account with Watsonx AI access
- A Watsonx AI Space ID and API Key

### Installation

```bash
pip install langchain-ibm ibm-watsonx-ai langgraph langchain-core
```

### Configuration

Clone the repository:

```bash
git clone https://github.com/anandhivasudevan/research_agent.git
cd research_agent
```

Set your IBM Watsonx credentials as environment variables or in a `.env` file:

```env
IBM_API_KEY=your_ibm_api_key_here
IBM_SPACE_ID=your_watsonx_space_id_here
IBM_SERVICE_URL=https://us-south.ml.cloud.ibm.com
```

Open the notebook and run the cells:

```bash
jupyter notebook "RESEARCH AGENT/Research_Agent.ipynb"
```

> Note: API credentials have been removed from the notebook for security. You will need your own IBM Watsonx API key and Space ID. A free IBM Cloud account can be created at [cloud.ibm.com](https://cloud.ibm.com).

---

## How It Works

### 1. Agent Initialization

The agent is initialized with a `ChatWatsonx` model connected to IBM Cloud, together with a set of search and web tools from the IBM Watsonx AI Toolkit. Tools are wrapped using a custom `create_utility_agent_tool()` function that converts them into LangChain `StructuredTool` objects with proper schema validation.

### 2. Tool Calling

When a research question is submitted, the ReAct agent decides which tool to invoke — it may query Google, search DuckDuckGo, look up Wikipedia, or crawl a specific URL depending on the nature of the query. This decision is made autonomously at each reasoning step.

### 3. Response Generation

The agent synthesizes information gathered from multiple tool calls and returns a well-structured response. Both standard (`generate`) and streaming (`generate_stream`) response modes are supported.

### 4. Streaming

`generate_stream()` handles three event types during output:

| Event Type              | Description                          |
|-------------------------|--------------------------------------|
| `messages`              | Content chunks streamed token by token |
| `updates > agent`       | Tool call decisions made by the agent  |
| `updates > tools`       | Results returned from tool calls       |

The final stream chunk includes token usage metadata: `prompt_tokens`, `completion_tokens`, and `total_tokens`.

### 5. Memory

Conversation history is maintained using LangGraph's `MemorySaver`, enabling the agent to handle follow-up questions within the same session without losing context.

---

## Key Implementation Details

- **Custom Tool Wrapper** — `create_utility_agent_tool()` bridges IBM Watsonx Toolkit tools to LangChain's `StructuredTool` interface, ensuring correct schema validation and argument handling.
- **Streaming Architecture** — `generate_stream()` processes event stream chunks and routes them by type for real-time display of reasoning, tool calls, and final answers.
- **Token Tracking** — usage metadata is extracted from the final stream chunk for cost and performance monitoring.

---

## About This Project

This project was developed as the final capstone during a 4-week AICTE-approved AI/ML internship with Edunet Foundation in collaboration with IBM SkillsBuild (July–August 2025). It was built and deployed on IBM Cloud using IBM Watsonx AI services.

---


## License

This project is open source and available under the MIT License.

---
