# Tutorial 11: Working with Structured Data

## What you'll learn

1. Pydantic Integration:
   - Data validation and modeling
   - Type annotations and `Field(description=...)`
   - Schema creation for LLM outputs

2. Structured Output:
   - `.with_structured_output(Schema)` — the modern replacement for `PydanticOutputParser` + `LLMChain`
   - `ToolStrategy` vs `ProviderStrategy` — how structured output actually works under the hood
   - Type-safe, validated responses straight from the model

3. JSON Processing:
   - Answering questions about arbitrary JSON data with an LLM
   - Generating format instructions/schemas from example data

4. Application Integration:
   - Combining Pydantic models with a `create_agent()` tool
   - A structured movie-recommendation agent

## Prerequisites

- Completion of Tutorials 1-10
- Python 3.10+
- Groq API key

## Getting Started

### 1. Ensure Virtual Environment is Activated

#### Linux/macOS:
```bash
cd langchain-langgraph-tutorial
source .venv/bin/activate
cd Tutorial11
```

#### Windows:
```cmd
cd langchain-langgraph-tutorial
.\.venv\Scripts\activate
cd Tutorial11
```

### 2. Launch Jupyter Notebook
```bash
jupyter notebook Tutorial_11_structured_data.ipynb
```

## What's Included

- `Tutorial_11_structured_data.ipynb`: Main tutorial notebook

### Key Features

#### Data Modeling
- Pydantic `BaseModel` classes with typed, described fields
- Validation errors on malformed data

#### Structured Output
- `llm.with_structured_output(Schema)` for reliable typed responses
- Wiring a Pydantic-returning function into a `create_agent()` tool

#### JSON Processing
- Asking an LLM questions about a JSON dataset directly, no agent required
- Auto-generating a format/schema description from example data

## Next Steps

After completing this tutorial:
1. Build type-safe applications with `.with_structured_output()`
2. Combine structured output with agent tools
3. Continue to Tutorial 12: Advanced LangChain Techniques

## Additional Resources

- [Pydantic Documentation](https://docs.pydantic.dev/)
- [LangChain Structured Output docs](https://docs.langchain.com/oss/python/langchain/structured-output)
- [Groq API Documentation](https://console.groq.com/docs)
