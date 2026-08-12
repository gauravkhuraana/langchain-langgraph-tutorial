# Tutorial 5: Advanced Agent Techniques in LangChain

Welcome to the fifth tutorial in our LangChain and LangGraph series! In this tutorial, we'll explore advanced techniques for working with agents in LangChain, focusing on building an AI-powered research assistant.

## What you'll learn

1. Building a specialized agent for scientific literature analysis
2. Giving an agent a vector-search tool over your own documents (FAISS + Ollama/FakeEmbeddings)
3. Adding persistent, multi-turn memory to an agent with a `MemorySaver` checkpointer
4. Composing a small real-world application (a research assistant) out of these pieces

## Prerequisites

- Completion of Tutorials 1-4
- Solid understanding of Python and Jupyter Notebooks
- A Groq API key (sign up at https://console.groq.com)
- Basic understanding of vector databases (covered in Tutorial 3)

## Getting Started

### 1. Ensure Virtual Environment is Activated

#### For Linux/macOS:
```bash
cd langchain-langgraph-tutorial
source .venv/bin/activate
cd Tutorial05
```

#### For Windows:
```cmd
cd langchain-langgraph-tutorial
.\.venv\Scripts\activate
cd Tutorial05
```

### 2. Launch Jupyter Notebook
```bash
jupyter notebook Tutorial_5_Advanced_Agent_Techniques.ipynb
```

## What's Included

- `Tutorial_5_Advanced_Agent_Techniques.ipynb`: Main tutorial notebook
- `research_papers/`: Sample research papers the agent searches over

### Key Features

#### Research assistant agent
- Built with `create_agent()` and a custom `system_prompt`
- Tools: vector-store search, summarise, analyse — each a plain `@tool`-decorated function

#### Memory
- `MemorySaver` checkpointer gives the agent conversational memory across turns of the same `thread_id`
- This is the direct replacement for the old `ConversationBufferMemory` + `ConversationChain`

## Troubleshooting

### Common Issues

1. **Vector store returns irrelevant results** — if Ollama isn't running, the notebook falls back to `FakeEmbeddings`, which produces random (not semantically meaningful) similarity — this is expected in that fallback mode, not a bug
2. **Agent doesn't remember earlier turns** — make sure you're passing the same `thread_id` in the `config` on every `invoke()` call
3. **Slow responses** — the research agent uses a larger model (`qwen/qwen3-32b`) for better tool-routing reliability

## Next Steps

After completing this tutorial:
1. Customize the research assistant for specific domains
2. Swap `MemorySaver` for `SqliteSaver` to persist memory across process restarts (Tutorial 19)
3. Continue to Tutorial 6: Memory Systems, for a deeper look at short-term vs. long-term memory patterns

## Additional Resources

- [LangChain Agents docs](https://docs.langchain.com/oss/python/langchain/agents)
- [LangGraph Persistence docs](https://langchain-ai.github.io/langgraph/concepts/persistence/)
