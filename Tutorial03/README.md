# Tutorial 3: Document Processing with LangChain

Welcome to the third tutorial in our LangChain and LangGraph series! In this tutorial, we'll explore document processing techniques using LangChain, focusing on loading, parsing, and analyzing text documents.

## What you'll learn

1. Loading and parsing different document types (`.txt`, `.pdf`)
2. Text splitting and chunking strategies
3. Building a simple question-answering system with an LCEL retrieval chain
4. Implementing semantic search over your own documents

## Prerequisites

- Completion of Tutorial 1 and 2
- Basic understanding of Python and Jupyter Notebooks
- A Groq API key (sign up at https://console.groq.com)

## Getting Started

### 1. Ensure Virtual Environment is Activated

#### For Linux/macOS:
```bash
cd langchain-langgraph-tutorial
source .venv/bin/activate
cd Tutorial03
```

#### For Windows:
```cmd
cd langchain-langgraph-tutorial
.\.venv\Scripts\activate
cd Tutorial03
```

### 2. (Optional) Install Ollama for Embedding Generation

The notebook prefers local Ollama embeddings and falls back to `FakeEmbeddings` (random vectors, for demo purposes) if Ollama isn't running — so this step is optional.

Download the Ollama CLI from https://ollama.com/download, then pull the embedding model:
```bash
ollama pull all-minilm
```

### 3. Launch Jupyter Notebook
```bash
jupyter notebook Tutorial_3_Document_Processing.ipynb
```

## What's Included

- `Tutorial_3_Document_Processing.ipynb`: Main tutorial notebook
- `sample_documents/`: Example documents for processing
  - `sample1.txt` — a plain-text document
  - `sample2.pdf` — a PDF document

### Key Topics

#### Document Loading
- `TextLoader` / `DirectoryLoader` for text files
- `PyPDFLoader` for PDFs
- All three live in `langchain_community.document_loaders`, which is still the only place they exist — `langchain_core.document_loaders` ships base classes only (`BaseLoader`, `Blob`, `BlobLoader`), and there is no `langchain.document_loaders`

> **Heads-up on `langchain-community`.** That package was sunset on 2026-05-22 and archived read-only on 2026-06-19, so importing from it emits a `DeprecationWarning`. It still works, and LangChain has deliberately named no replacement — the guidance is to adopt a maintained standalone package if one appears, or wrap the underlying library yourself. The loaders stay here because document loading is this tutorial's whole subject, and `PyPDFLoader` does real work wrapping `pypdf` with page splitting. Where loading is only incidental plumbing, hand-rolling it is cheaper than the dependency: Tutorial 5 builds `Document` objects straight from `pathlib` in four lines.

#### Text Processing
- `RecursiveCharacterTextSplitter` chunking
- Chunk size and overlap tuning

#### Search Implementation
- `InMemoryVectorStore` (`langchain_core.vectorstores`) — a dependency-free vector store, ideal for a small demo corpus like this one
- Embedding generation (Ollama, with a `FakeEmbeddings` fallback)
- LCEL retrieval chain (the modern replacement for the deprecated `RetrievalQA`)
- Direct `similarity_search()` for semantic search

> **Why not FAISS?** `langchain_community.vectorstores.FAISS` is still current and worth knowing (it gets a dedicated section in Tutorial 12), but it's a compiled native dependency (`faiss-cpu`) that adds approximate nearest-neighbor indexing — overkill for the couple of sample files here. `InMemoryVectorStore` ships in `langchain_core`, needs no extra install, and does exact brute-force search, which is all a small corpus needs.

## Troubleshooting

### Common Issues

1. **Document Loading Errors**
   - File format compatibility
   - Encoding issues
   - Permission problems

2. **Embeddings**
   - If Ollama isn't installed/running, the notebook automatically falls back to `FakeEmbeddings` — similarity search results will look random in that mode, which is expected

## Next Steps

After completing this tutorial:
1. Experiment with different document types
2. Optimize chunking strategies
3. Continue to Tutorial 4: Agents in LangChain

## Additional Resources

- [LangChain Document Loaders](https://docs.langchain.com/oss/python/integrations/document_loaders)
- [LangChain Text Splitters](https://docs.langchain.com/oss/python/langchain/text-splitters)
- [LangChain Vector Stores](https://docs.langchain.com/oss/python/langchain/retrieval#vector-stores)

Happy learning!
