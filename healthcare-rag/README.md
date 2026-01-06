# Multimodal Retrieval-Augmented Generation (RAG) for Healthcare Q&A
This project implements an **advanced multimodal Retrieval-Augmented Generation (RAG) system** designed for grounded question answering in a healthcare context.  
The system retrieves relevant **text and image-based knowledge** from curated sources and generates accurate, explainable responses using large language models.
The primary goal is to **reduce hallucinations**, improve **answer relevance**, and demonstrate how modern RAG architectures can be applied to real-world healthcare and wellness applications.

## Problem Motivation

Traditional keyword-based search and standalone LLMs struggle with:
- Capturing **semantic intent** in user queries
- Providing **grounded, verifiable answers**
- Incorporating **multimodal context** (text + images)
- Avoiding hallucinations in high-stakes domains like healthcare
This project demonstrates how **RAG pipelines with reranking and query expansion** address these challenges.

## System Overview

**Key capabilities:**
- Text-based retrieval from healthcare PDFs
- Image-based retrieval using CLIP embeddings
- Query expansion to improve recall
- Cross-encoder reranking to improve precision
- Grounded response generation with retrieved context
- Multimodal output (text answers + relevant images)

## Architecture

1. **Document Ingestion**
   - Healthcare PDFs loaded and chunked
   - Images ingested with metadata
2. **Embedding**
   - Text embeddings using OpenAI models
   - Image embeddings using CLIP
3. **Vector Storage**
   - ChromaDB used for persistent vector storage
4. **Query Expansion**
   - LLM-generated reformulations of user queries
5. **Retrieval**
   - Initial retrieval using vector similarity
6. **Reranking**
   - Cross-encoder reranking for top-K relevance
7. **Answer Generation**
   - LLM generates responses grounded strictly in retrieved context
8. **Multimodal Response**
   - Returns both text explanations and relevant images

## Technologies Used

- **LangChain**
- **ChromaDB**
- **OpenAI Embeddings**
- **GPT-4o-mini (LLM)**
- **HuggingFace Transformers**
- **Sentence Transformers**
- **Cross-Encoders (MS MARCO)**
- **CLIP (image embeddings)**
- **PyPDF**
- **Python / Jupyter**



