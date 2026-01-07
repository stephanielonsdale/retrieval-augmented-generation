# Retrieval-Augmented Generation (RAG)

A collection of **end-to-end Retrieval-Augmented Generation (RAG) systems** demonstrating grounded question answering using embeddings, vector search, reranking, multimodal retrieval, and LLM-based evaluation.

This repository focuses on **accuracy, traceability, and hallucination mitigation** across different real-world domains, with implementations designed to be readable, reproducible, and extensible.

---

## What’s in this repository

This repo currently contains **two complete RAG projects**, each implemented as a standalone notebook with its own README and setup instructions.

```text
retrieval-augmented-generation/
├── healthcare-rag/
│   ├── README.md
│   └── multimodal_healthcare_rag.ipynb
│
├── salesforce-QA-assistant/
│   ├── README.md
│   └── Salesforce_Q&A_Assistant.ipynb
│
├── README.md
├── LICENSE
└── .gitignore
```

---

## Projects

### 🏥 Healthcare Multimodal RAG

**Domain:** Healthcare / Nutrition / Medical knowledge  
**Focus:** Multimodal retrieval, reranking, query expansion, grounded responses

Key features:
- Text retrieval from healthcare PDFs
- Image retrieval using CLIP embeddings
- Unified multimodal vector database (ChromaDB)
- LLM-based query expansion for improved recall
- Cross-encoder reranking (MS MARCO) for improved precision
- Multimodal outputs (text answers + relevant images)

📁 Located in: `healthcare-rag/`  
📄 See project-specific README for full details.

---

### 💼 Salesforce CRM RAG Q&A Assistant

**Domain:** Enterprise / CRM / Sales enablement  
**Focus:** Grounded Q&A with explicit evaluation metrics

Key features:
- PDF ingestion and overlapping chunking
- Vector similarity search using Chroma
- Strict context-grounded answer generation
- LLM-based evaluation across five metrics:
  - Groundedness
  - Relevance
  - Faithfulness
  - Context Precision
  - Context Recall
- Designed for internal business documentation and enablement use cases

📁 Located in: `salesforce-QA-assistant/`  
📄 See project-specific README for full details.

---

## Design Philosophy

Across all projects in this repository, the guiding principles are:

- **Groundedness over creativity**  
  Answers are generated strictly from retrieved context.

- **Evaluation as a first-class concern**  
  RAG quality is measured, not assumed.

- **Modularity and clarity**  
  Each notebook is self-contained, readable, and reusable.

- **Production-inspired design**  
  Architectures reflect real-world RAG systems used in practice.

---

## Technologies Used

- Python / Jupyter Notebook
- LangChain
- ChromaDB
- OpenAI Embeddings and Chat Models
- Hugging Face Transformers
- Sentence Transformers
- CLIP (image embeddings)
- Cross-encoder reranking (MS MARCO)

---

## Who this repository is for

- Recruiters evaluating applied AI / ML engineering skills
- Students learning modern RAG architectures
- Engineers building domain-specific Q&A systems
- Researchers interested in hallucination mitigation and evaluation

---

## Disclaimer

These projects are intended for **educational and demonstration purposes only**.  
They are **not production systems** and should not be used for medical diagnosis, clinical decision-making, or enterprise deployment without additional safeguards.

---

## Author

**Stephanie Lonsdale**  
Graduate Student, AI Engineering  
Johns Hopkins University
