# Multimodal Retrieval-Augmented Generation (RAG) for Healthcare Q&A

An **advanced multimodal Retrieval-Augmented Generation (RAG) system** designed for **healthcare question answering**.  
This project combines **text-based medical documents (PDFs)** and **medical images** in a single vector database, applies **query expansion and cross-encoder reranking**, and generates **grounded, explainable responses** using a large language model.

The goal is to demonstrate how modern RAG architectures can reduce hallucinations and improve answer relevance in **high-stakes domains like healthcare**.

---

## Problem Motivation

Traditional keyword search and standalone LLMs struggle with:

- Capturing **semantic intent** in complex medical queries  
- Producing **verifiable, grounded answers**
- Incorporating **multimodal context** (text + images)
- Avoiding hallucinations in safety-critical domains

This project addresses these challenges using:
- Vector-based retrieval
- Query expansion for recall
- Cross-encoder reranking for precision
- Strict context-grounded answer generation

---

## System Overview

### Key Capabilities

- Text-based retrieval from healthcare PDFs
- Image-based retrieval using CLIP embeddings
- Unified multimodal vector database (ChromaDB)
- LLM-driven query expansion to improve recall
- Cross-encoder reranking (MS MARCO) to improve precision
- Grounded answer generation using retrieved context
- Multimodal outputs (text answers + relevant images)

---

## Architecture

1. **Document Ingestion**
   - Healthcare PDFs loaded and chunked
   - Images ingested with structured metadata

2. **Embedding**
   - Text embeddings using OpenAI embedding models
   - Image embeddings using CLIP

3. **Vector Storage**
   - Persistent vector storage using ChromaDB

4. **Query Expansion**
   - LLM-generated reformulations of the user query
   - Improves recall for ambiguous or underspecified questions

5. **Retrieval**
   - Initial similarity-based retrieval from vector DB

6. **Reranking**
   - Cross-encoder reranking for top-k relevance refinement

7. **Answer Generation**
   - LLM generates responses strictly grounded in retrieved context

8. **Multimodal Response**
   - Returns both text explanations and relevant images

---

## Repository Structure

```text
.
├── multimodal_healthcare_rag.ipynb   # Main notebook (text + image RAG)
├── data/
│   ├── pdfs/                         # Healthcare PDFs (not committed)
│   └── images/                       # Medical images with metadata (not committed)
├── chroma_db/                        # Persistent vector database (generated)
├── README.md
```

> **Important:** `data/` and `chroma_db/` should not be committed to a public repository.

---

## Setup

### 1) Create an environment

```bash
python -m venv .venv
source .venv/bin/activate  # Mac/Linux
# .venv\Scripts\activate   # Windows
```

### 2) Install dependencies

```bash
pip install \
  langchain \
  langchain_community \
  chromadb \
  pypdf \
  tiktoken \
  openai \
  sentence-transformers \
  transformers \
  pillow \
  matplotlib \
  torch
```

---

## Configuration (API Key)

This notebook assumes an OpenAI API key is available as an environment variable.

### Recommended (safe for GitHub)

Create a `.env` file:

```bash
OPENAI_API_KEY="your_api_key_here"
OPENAI_BASE_URL="https://api.openai.com/v1"
```

Add to `.gitignore`:

```gitignore
.env
config.json
data/
chroma_db/
```

---

## How to Run

1. Place healthcare PDFs into:
   ```text
   data/pdfs/
   ```

2. Place healthcare images into:
   ```text
   data/images/
   ```

3. Launch Jupyter:
   ```bash
   jupyter notebook
   ```

4. Run the notebook top-to-bottom:
   - Load PDFs and images
   - Create text + image embeddings
   - Build or load the vector database
   - Expand user queries
   - Retrieve and rerank relevant results
   - Generate grounded multimodal answers

---

## Example Use Cases

- “Which citrus fruits are highest in vitamin C?”
- “Show images and explain symptoms of vitamin deficiency”
- “What foods support immune health based on clinical sources?”
- “Retrieve both textual and visual evidence for nutrition guidance”

---

## Key Design Decisions

- **Multimodal retrieval:** Treats images as first-class retrieval objects
- **Query expansion:** Improves recall without manual prompt engineering
- **Cross-encoder reranking:** Increases precision for top-k results
- **Strict grounding:** LLM answers only from retrieved evidence
- **Healthcare-first mindset:** Prioritizes accuracy over creativity

---

## Future Improvements

- Add citation formatting (source PDF + page + image ID)
- Introduce evaluation metrics (groundedness, relevance, faithfulness)
- Support structured medical ontologies (e.g., ICD, SNOMED)
- Add human-in-the-loop review for clinical safety
- Extend to tabular clinical data

---

## Disclaimer

This project is intended for **educational and research purposes only**.  
It is **not a medical device** and should not be used for diagnosis or treatment.

Production healthcare systems require:
- Regulatory compliance
- Clinical validation
- Human oversight
- Secure data governance

---

## Author

**Stephanie Lonsdale**  
Graduate Student, AI Engineering  
Johns Hopkins University
