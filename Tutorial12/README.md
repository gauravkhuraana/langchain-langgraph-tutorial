# Tutorial 12: Advanced LangChain Techniques

## What you'll learn

1. Custom Chain Development:
   - Building a specialized processing step as a plain Python/LCEL-compatible class
   - Composing steps with LCEL (`prompt | llm | parser`)

2. Advanced Prompting:
   - Multi-turn few-shot prompt templates with `ChatPromptTemplate.from_messages()`
   - Context management across a templated conversation

3. Retrieval-Augmented Generation:
   - FAISS vector store with a three-tier embeddings fallback (Ollama → HuggingFace → Fake)
   - Document loading, splitting, and retrieval-augmented answering

4. "Fine-tuning" via prompting:
   - Simulating task specialization (sentiment analysis) with a dedicated prompt, since the Groq-hosted models aren't fine-tunable here

## Prerequisites

- Completion of Tutorials 1-11
- Python 3.10+
- Groq API key

## Getting Started

### 1. Ensure Virtual Environment is Activated

#### Linux/macOS:
```bash
cd langchain-langgraph-tutorial
source .venv/bin/activate
cd Tutorial12
```

#### Windows:
```cmd
cd langchain-langgraph-tutorial
.\.venv\Scripts\activate
cd Tutorial12
```

### 2. Launch Jupyter Notebook
```bash
jupyter notebook Tutorial_12_advanced_langchain_techniques.ipynb
```

## What's Included

- `Tutorial_12_advanced_langchain_techniques.ipynb`: Main tutorial notebook
- `sample_document.txt`: Sample document used for the RAG section

### Key Features

#### Chain Development
- A custom LCEL-compatible processing class
- Multi-turn prompt templates composed into an LCEL chain (replacing the deprecated `LLMChain`)

#### RAG Implementation
- `langchain_huggingface.HuggingFaceEmbeddings` as a local-embedding fallback tier (needs `sentence-transformers` installed to actually activate — otherwise the notebook falls back further to `FakeEmbeddings`)
- FAISS similarity search feeding an LCEL RAG chain
- `RecursiveCharacterTextSplitter` for chunking — note that `CharacterTextSplitter` splits on `\n\n` by default, which the sample document never contains, so it would yield a single unsplittable chunk and defeat retrieval entirely

> **Why FAISS here and not in Tutorials 3/5/9?** Those tutorials use `InMemoryVectorStore` from `langchain_core`: exact brute-force search, no native dependency, and entirely adequate for a handful of chunks. FAISS (`faiss-cpu`) adds approximate nearest-neighbor indexing, which is what you want once scanning every vector per query becomes the bottleneck. This tutorial keeps FAISS so you've seen the production-grade path; the two APIs are near-identical, so switching is a one-line change.

#### Prompt-based specialization
- A dedicated sentiment-analysis prompt as a lightweight stand-in for fine-tuning

## Next Steps

After completing this tutorial:
1. Create more complex chain architectures
2. Try the HuggingFace embeddings tier locally (`pip install sentence-transformers`)
3. Continue to Tutorial 13: Best Practices and Advanced Topics

## Additional Resources

- [LangChain Documentation](https://docs.langchain.com/oss/python/langchain/overview)
- [langchain-huggingface docs](https://python.langchain.com/docs/integrations/providers/huggingface/)
- [FAISS Documentation](https://github.com/facebookresearch/faiss)
- [Groq API Documentation](https://console.groq.com/docs)
