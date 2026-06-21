# Sample Docs with LangChain Docling

## Project Overview

This repository demonstrates how to use **LangChain Docling** to load, chunk, and process documents (PDFs, Word files, etc.) for downstream LLM applications such as retrieval‑augmented generation (RAG).  The notebooks showcase:

- Installing the required libraries (`langchain`, `langchain-docling`, `sentence‑transformers`, `qdrant-client`, etc.).
- Loading a remote PDF with `DoclingLoader` and converting the resulting `DocChunk` objects into plain Python dictionaries.
- Performing hierarchical chunking using `HierarchicalChunker` and further splitting markdown‑style headings with `MarkdownHeaderTextSplitter`.
- Preparing the chunks for embedding and vector store ingestion (e.g., Qdrant).

The goal is to provide a minimal, end‑to‑end example that can be run locally or in Google Colab.

---

## Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/your‑username/sample_docs.git
   cd sample_docs
   ```

2. **Create a virtual environment (optional but recommended)**
   ```bash
   python -m venv .venv
   source .venv/bin/activate   # on Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt  # if a requirements file is added later
   # or install directly:
   pip install langchain langchain-community langchain-huggingface \
               langchain-qdrant langchain-groq sentence-transformers \
               qdrant-client langchain-docling
   ```

4. **Set up API keys**
   - The notebooks use the **Groq** API for LLM inference. Export your key before running:
     ```bash
     export GROQ_API_KEY="your-groq-api-key"
     ```
   - If you prefer to be prompted for the key, simply run the notebook; it will ask for input via `getpass`.

---

## Usage Examples

### Running the notebook locally
```bash
jupyter notebook langchain_docling.ipynb
```
Follow the cells to:
1. Install packages.
2. Load a PDF from a public URL.
3. Chunk the document with `HierarchicalChunker`.
4. Convert each `DocChunk` to a dictionary containing headings, raw content, and a `chunk_text` ready for embedding.
5. (Optional) Further split markdown sections with `MarkdownHeaderTextSplitter`.

### Minimal script example
```python
from langchain_docling.loader import DoclingLoader, ExportType
from docling.chunking import HierarchicalChunker

FILE_URL = "https://raw.githubusercontent.com/tnahddisttud/sample-doc/refs/heads/main/AtliqAI_HR_Policies.pdf"
EMBED_MODEL = "sentence-transformers/all-MiniLM-L6-v2"

chunker = HierarchicalChunker(tokenizer=EMBED_MODEL)
loader = DoclingLoader(
    file_path=FILE_URL,
    export_type=ExportType.DOC_CHUNKS,
    chunker=chunker,
)

docs = loader.load()

# Convert to plain dicts
def to_dict(chunk):
    headings = chunk.metadata.get("dl_meta", {}).get("headings", [])
    content = chunk.page_content.strip()
    breadcrumb = " > ".join(headings)
    chunk_text = f"{breadcrumb}\n\n{content}" if breadcrumb else content
    return {"headings": headings, "content": content, "chunk_text": chunk_text}

chunks = [to_dict(c) for c in docs]
print(chunks[0])
```

---

## Contributing Guidelines

We welcome contributions! Please read the [CONTRIBUTING.md](CONTRIBUTING.md) file for details on our code of conduct, the process for submitting pull requests, and how to set up a development environment.

---

## License

This project is licensed under the MIT License – see the `LICENSE` file for details.
