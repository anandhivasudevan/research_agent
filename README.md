 Research Agent — AI-Powered Autonomous Research Assistant
An intelligent research agent built with LangGraph ReAct architecture, powered by Meta LLaMA 3.2 on IBM Watsonx AI, and deployed on IBM Cloud. The agent autonomously searches the web, retrieves academic information, summarizes findings, and generates structured research reports — all through a conversational interface.

Built as the capstone project for the AICTE Internship with IBM SkillsBuild × Edunet Foundation (July–August 2025).


Features

ReAct Agent Architecture — uses LangGraph's create_react_agent for autonomous reasoning and tool use
Multi-Source Search — integrates GoogleSearch, DuckDuckGo, Wikipedia, and WebCrawler tools
Research Summarization — understands natural language research questions and retrieves relevant information
Report Generation — drafts structured research summaries and suggests hypotheses
Streaming Responses — real-time token-by-token streaming via generate_stream()
Conversation Memory — multi-turn memory with LangGraph's MemorySaver
IBM Cloud Deployment — deployed as a production service on IBM Watsonx AI (IBM Cloud US South)


Tech Stack
LayerTechnologyLLMMeta LLaMA 3.2 (11B Vision Instruct)Agent FrameworkLangGraph (ReAct)LLM IntegrationLangChain IBM / ChatWatsonxToolsIBM Watsonx AI Toolkit (GoogleSearch, DuckDuckGo, Wikipedia, WebCrawler)DeploymentIBM Watsonx AI — IBM Cloud (us-south)LanguagePython (Jupyter Notebook)

Architecture
User Query
    │
    ▼
ReAct Agent (LangGraph)
    │
    ├──► GoogleSearch Tool
    ├──► DuckDuckGo Tool
    ├──► Wikipedia Tool
    ├──► WebCrawler Tool
    │
    ▼
LLaMA 3.2 (IBM Watsonx)
    │
    ▼
Structured Research Response (streamed)
The agent follows the Reasoning + Acting (ReAct) loop:

Receives a research question
Reasons about which tool to use
Acts by calling the appropriate search tool
Observes the result
Repeats until it has enough information
Returns a comprehensive, formatted response


🚀 Getting Started
Prerequisites
bashpip install langchain-ibm ibm-watsonx-ai langgraph langchain-core
Configuration

Clone the repo:

bashgit clone https://github.com/anandhivasudevan/research_agent.git
cd research_agent

Set up your IBM Watsonx credentials. Create a .env file based on .env.example:

IBM_API_KEY=your_ibm_api_key_here
IBM_SPACE_ID=your_watsonx_space_id_here
IBM_SERVICE_URL=https://us-south.ml.cloud.ibm.com

Open RESEARCH AGENT/Research_Agent.ipynb in Jupyter and run the cells.


⚠️ Note: API credentials have been removed from the notebook for security. You will need your own IBM Watsonx API key and Space ID to run this project. Sign up for a free IBM Cloud account at cloud.ibm.com.

 
How It Works
1. Agent Initialization
The agent is initialized with a ChatWatsonx model connected to IBM Cloud, along with a set of search and web tools from the IBM Watsonx AI Toolkit.
2. Tool Calling
When the user asks a research question, the ReAct agent decides which tool to call — it may search Google, query DuckDuckGo, look up Wikipedia, or crawl a specific webpage depending on the query.
3. Response Generation
The agent synthesizes information from multiple sources and returns a well-structured response. It supports both standard (generate) and streaming (generate_stream) response modes for real-time output.
4. Memory
Conversation history is maintained using LangGraph's MemorySaver, allowing the agent to handle follow-up questions within the same session.

Key Implementation Details

Custom Tool Wrapper — create_utility_agent_tool() wraps IBM Watsonx Toolkit tools into LangChain StructuredTool objects with proper schema validation
Streaming Architecture — generate_stream() handles three event types: messages (content chunks), updates > agent (tool calls), and updates > tools (tool results)
Token Usage Tracking — final stream chunk includes prompt_tokens, completion_tokens, and total_tokens metadata


About This Project
This project was developed as the final capstone during a 4-week AICTE-approved AI/ML internship with Edunet Foundation in collaboration with IBM SkillsBuild (July–August 2025). It was built and deployed on IBM Cloud using IBM Watsonx AI services.

Author
Anandhi Vasudevan
AI & ML Engineer | B.Tech AI & DS, CK College of Engineering and Technology


License
This project is open source and available under the MIT License.
