# Tutorial 6: Memory Systems in LangChain

Welcome to Tutorial 6. In this tutorial we explore how conversational memory works in modern LangChain 1.0 + LangGraph 1.0 — where memory lives in graph state and checkpointers, not in the old `Conversation*Memory` classes.

## What you'll learn

1. Why the old memory classes are gone
   - `ConversationBufferMemory`, `ConversationSummaryMemory`, `CombinedMemory`, and `ConversationKGMemory` have all been removed
   - LangGraph state + checkpointers replace them, with more explicit control

2. Short-term (per-thread) memory
   - `Annotated[List, operator.add]` message accumulation in graph state
   - `MemorySaver` checkpointer to persist history across turns of the same conversation

3. Summary memory
   - Summarising older messages with an LCEL/LLM call once history grows past a threshold, to keep the context window small

4. Long-term (cross-thread) memory
   - `InMemoryStore` for facts that need to be available across different conversation threads for the same user

## Prerequisites

- Completion of Tutorials 1-5
- Python and Jupyter Notebooks
- Groq API key (https://console.groq.com)

## Getting Started

### 1. Ensure Virtual Environment is Activated

#### Linux/macOS:
```bash
cd langchain-langgraph-tutorial
source .venv/bin/activate
cd Tutorial06
```

#### Windows:
```cmd
cd langchain-langgraph-tutorial
.\.venv\Scripts\activate
cd Tutorial06
```

### 2. Launch Jupyter Notebook
```bash
jupyter notebook Tutorial_6_Memory_Systems_in_LangChain.ipynb
```

## What's Included

- `Tutorial_6_Memory_Systems_in_LangChain.ipynb`: Main tutorial notebook — buffer memory, summary memory, and long-term memory, each built from LangGraph primitives

### Key Concepts Covered

#### Buffer memory
- `StateGraph` with `Annotated[List, operator.add]` for message accumulation
- `MemorySaver` checkpointer + `thread_id` to persist a conversation

#### Summary memory
- Summarising the older portion of a conversation once it exceeds a message threshold
- Prepending the running summary as a `SystemMessage` for subsequent turns

#### Long-term memory
- `InMemoryStore` namespaced by user, for facts that persist across separate `thread_id`s
- Swap `InMemoryStore` for a persistent store (e.g. a database-backed one) in production

## Troubleshooting

Common Issues:
1. Forgetting to pass the same `thread_id` between turns — each new `thread_id` starts a fresh conversation
2. Long conversations exceeding the model's context window — see the summary memory section, and Tutorial 19 for `trim_messages()`-based trimming
3. Long-term facts not persisting — check you're using the same `InMemoryStore` instance and namespace across sessions

## Next Steps

After completing this tutorial:
1. Study Tutorial 19 for `SqliteSaver` (durable, cross-restart persistence) and `trim_messages()`
2. Experiment with custom summarisation strategies
3. Build a chatbot that combines short-term and long-term memory

Continue to Tutorial 7: Introduction to LangGraph

## Additional Resources

- [LangGraph Persistence Concepts](https://langchain-ai.github.io/langgraph/concepts/persistence/)
- [LangGraph Memory Concepts](https://langchain-ai.github.io/langgraph/concepts/memory/)
