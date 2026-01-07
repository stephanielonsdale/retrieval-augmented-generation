# Salesforce CRM RAG Q&A Assistant

A **Retrieval-Augmented Generation (RAG)** notebook that transforms Salesforce CRM documentation into a grounded, queryable **Q&A assistant**.  
The system retrieves relevant document context using vector search and generates answers strictly based on retrieved evidence, with a built-in **LLM-based evaluation framework** to assess answer quality.

---

## Overview

This project demonstrates an end-to-end RAG pipeline designed for internal business knowledge use cases (e.g., Sales, CRM, Enablement teams). It focuses on **traceability**, **groundedness**, and **evaluation**, not just answer generation.

The notebook includes:
- Document ingestion and chunking
- Vector embedding and storage with Chroma
- Context-aware answer generation using an OpenAI-compatible LLM
- Multi-metric LLM-based evaluation of responses

---

## Architecture

### 1. Data Ingestion & Chunking
- Loads multiple Salesforce-related PDFs using `PyPDFLoader`
- Splits documents into overlapping text chunks using `RecursiveCharacterTextSplitter`
- Preserves semantic continuity across chunks

### 2. Embedding & Vector Store
- Generates embeddings using `OpenAIEmbeddings`
- Stores vectors locally in a persistent **Chroma** database
- Enables fast similarity search across large documentation sets

### 3. Query Handling & Answer Generation
- Retrieves the top-*k* most relevant chunks using cosine similarity
- Passes **only retrieved context + user query** to the LLM
- Enforces strict grounding rules in the prompt to prevent hallucinations

### 4. LLM-Based Multi-Metric Evaluation
A second LLM evaluates each generated answer using five metrics:
- **Groundedness** – Is the answer supported by retrieved context?
- **Relevance** – Does it directly address the user’s question?
- **Faithfulness** – Are the claims logically valid and consistent?
- **Context Precision** – Does it avoid irrelevant context?
- **Context Recall** – Does it capture all key information?

Each metric is scored on a **1–5 scale** with a structured JSON justification.

---

## Repository Structure

```text
.
├── Salesforce_Q&A_Assistant.ipynb   # Main RAG + evaluation notebook
├── Salesforce/                      # Folder for Salesforce CRM PDFs (not committed)
├── chroma_db/                       # Local persisted Chroma vector store (generated)
├── README.md
```

> **Note:** `Salesforce/` and `chroma_db/` should not be committed to a public repository.

---

## Setup

### 1) Create an environment

```bash
python -m venv .venv
source .venv/bin/activate  # Mac/Linux
# .venv\Scripts\activate   # Windows
```

### 2) Install dependencies

The notebook uses (at minimum):

```bash
pip install langchain langchain_community chromadb pypdf tiktoken openai
```

---

## Configuration (API Key)

This notebook currently reads credentials from a local configuration file and sets environment variables.

### Recommended (safer) approach for GitHub

Use a `.env` file and add it to `.gitignore`.

Create a `.env` file:

```bash
OPENAI_API_KEY="your_api_key_here"
OPENAI_BASE_URL="https://api.openai.com/v1"
```

Add the following to `.gitignore`:

```gitignore
.env
config.json
Salesforce/
chroma_db/
```

---

## How to Run

1. Place Salesforce CRM PDFs into:
   ```text
   Salesforce/
   ```
2. Open the notebook:
   ```bash
   jupyter notebook
   ```
3. Run cells top-to-bottom:
   - Load and chunk PDFs
   - Create embeddings and persist the vector store
   - Submit a business question
   - Generate a grounded answer
   - Evaluate the response using all five metrics

---

## Example Business Questions

The assistant is designed to answer questions such as:

- What are the key features and functionalities of Salesforce CRM Sales Cloud?
- How do we integrate third-party marketing tools with Salesforce?
- How can we generate a report showing lead conversion rates by region?
- How can customer satisfaction be tracked and reported in Salesforce?
- What are best practices for updating opportunities during a sales review?

---

## Key Design Decisions

- **Strict grounding:** The LLM is instructed to answer *only* from retrieved context.
- **Chunk overlap:** Improves recall for multi-sentence concepts.
- **Persistent vector store:** Avoids re-embedding documents across sessions.
- **Evaluation-first mindset:** Treats answer quality as a first-class concern, not an afterthought.

---

## Future Improvements

- Add inline citations (document name + page number) to generated answers
- Introduce hybrid retrieval (BM25 + vector search)
- Use MMR or diversity-based retrieval to reduce redundant chunks
- Aggregate evaluation scores across a benchmark question set
- Add query rewriting for short or ambiguous user questions

---

## Disclaimer

This project is intended for **educational and demonstration purposes**.  
Production deployments should include:
- Secure secret management
- Human-in-the-loop evaluation
- Monitoring for retrieval and hallucination failures
- Access control and audit logging

---

## Author

**Stephanie Lonsdale**  
Graduate Student, AI Engineering  
Johns Hopkins University

