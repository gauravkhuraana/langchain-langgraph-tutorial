# Tutorial 4: Agents in LangChain

Welcome to the fourth tutorial in our LangChain and LangGraph series! In this tutorial, we'll explore the concept of Agents in LangChain, which are autonomous entities capable of using tools and making decisions to accomplish tasks.

## What you'll learn

1. Understanding the agent architecture, and how the agent-building API evolved: `initialize_agent()`/`AgentExecutor` (now in `langchain-classic`) → `langgraph.prebuilt.create_react_agent` (now deprecated) → `create_agent()` from the `langchain` package (current)
2. Building agents with `create_agent()`:
   - Zero-shot tool-using agent
   - Conversational agent with a system prompt
   - Plan-and-execute style agent
3. Creating custom tools with `@tool` and `langchain_core.tools.Tool`
4. Implementing a multi-tool agent for task solving

## Prerequisites

- Completion of Tutorials 1-3
- Familiarity with Python and Jupyter Notebooks
- A Groq API key (sign up at https://console.groq.com)

## Getting Started

### 1. Ensure Virtual Environment is Activated

#### For Linux/macOS:
```bash
cd langchain-langgraph-tutorial
source .venv/bin/activate
cd Tutorial04
```

#### For Windows:
```cmd
cd langchain-langgraph-tutorial
.\.venv\Scripts\activate
cd Tutorial04
```

### 2. Launch Jupyter Notebook
```bash
jupyter notebook Tutorial_4_Agents_in_LangChain.ipynb
```

## What's Included

- `Tutorial_4_Agents_in_LangChain.ipynb`: Main tutorial notebook

### Key Topics

#### `create_agent()` basics
- `model` + `tools` — the minimum needed to build an agent
- `system_prompt` — customising agent behaviour
- How the ReAct loop (reason → act → observe) runs under the hood

#### Custom tools
- `@tool`-decorated functions with docstrings the model reads as tool descriptions
- `langchain_core.tools.Tool` for wrapping arbitrary callables
- A DuckDuckGo web-search tool (via `langchain_community.tools.DuckDuckGoSearchRun`, backed by the `ddgs` package)

## Troubleshooting

### Common Issues

1. **Agent doesn't call a tool you expect** — check the tool's docstring is descriptive; the model chooses tools based on it
2. **Web search errors** — make sure `ddgs` is installed (`pip install -r requirements.txt`); DuckDuckGo's free endpoint can also rate-limit
3. **Response parsing** — read `result["messages"][-1].content`, not the raw result dict

## Next Steps

After completing this tutorial:
1. Build custom agent architectures
2. Develop specialized tools
3. Continue to Tutorial 5: Advanced Agent Techniques, where we build a multi-tool research assistant with persistent memory

## Additional Resources

- [LangChain Agents docs](https://docs.langchain.com/oss/python/langchain/agents)
- [LangChain v1 migration guide](https://docs.langchain.com/oss/python/migrate/langchain-v1)
