# ChromaDB: A Clear Beginner Guide

## 1) What is ChromaDB?

ChromaDB is a lightweight vector database. It stores text as embeddings, which are numerical representations of meaning.

This allows us to search by similarity instead of exact keyword matching.

Example:
- Search for "pet" may also match "dog" or "cat"
- Traditional databases usually look for exact words
- Vector databases focus on semantic similarity

## 2) Why use vector databases?

Vector databases are useful when you want to:
- search by meaning
- build RAG systems
- find similar documents
- recommend related items

## 3) Install required packages

```bash
python -m pip install chromadb sentence-transformers
```

## 4) Import libraries

```python
import chromadb
from pathlib import Path
```

## 5) Create a persistent client

```python
persist_dir = Path("./chroma_db").resolve()
persist_dir.mkdir(exist_ok=True)
client = chromadb.PersistentClient(path=str(persist_dir))
```

## 6) Create a collection

```python
collection = client.get_or_create_collection(
    name="my_first_collection",
    metadata={"hnsw:space": "cosine"},
)
```

A collection is like a table in a database. It stores the text and its vector representation.

## 7) Add documents

```python
documents = [
    "Machine learning models learn from data.",
    "Cats are curious and independent animals.",
    "Vector databases store embeddings for semantic search.",
    "Neural networks process information like the brain.",
]

metadatas = [
    {"topic": "machine learning"},
    {"topic": "animals"},
    {"topic": "vector databases"},
    {"topic": "neural networks"},
]

ids = [f"doc_{i}" for i in range(len(documents))]

collection.add(documents=documents, metadatas=metadatas, ids=ids)
```

## 8) Run a semantic search

```python
query = "Tell me about machine learning and AI"

results = collection.query(
    query_texts=[query],
    n_results=3,
    include=["documents", "metadatas", "distances"],
)
```

### Output example

```python
for doc, meta, distance in zip(results["documents"][0], results["metadatas"][0], results["distances"][0]):
    print(doc)
    print(meta)
    print(distance)
```

## 9) Why this matters

Vector databases help us search by meaning, not just by text matching.

Example:
- Query: "How does AI learn?"
- Relevant document: "Machine learning models learn from data."

This is the foundation for:
- semantic search
- chatbots
- RAG systems
- recommendation systems

## 10) Final takeaway

ChromaDB makes it easy to:
1. store documents
2. create embeddings
3. search semantically
4. build AI-powered applications

It is simple, lightweight, and beginner-friendly.

---

This guide is a clean, beginner-oriented overview of ChromaDB based on the original concept and simplified for easy understanding.
