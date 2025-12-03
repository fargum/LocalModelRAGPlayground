# LocalModelRAGPlayground

A **Retrieval-Augmented Generation (RAG)** pipeline for exploring Dungeons & Dragons guidebook content using local LLMs. This project uses a Python notebook to experiment with different local language models via Ollama to test their performance on various RAG tasks.
This repo is a small companion to my larger Portfolio Manager AI project, which I have built to manage my personal investment portfolio.
There I focus on cloud-hosted models and enterprise patterns; here I explore what a fully local RAG pipeline looks like using small models (Phi-3 Mini) and an in-memory vector store. I am very excited about the potential for small, local language models and how much of the AI load (especially in Agentic setups) can be passed to them. Ollama is a great tool for this, although I have used Hugging Face's transformer framework for more granular control.

## Overview

All operations are performed locally:
- **Local LLM**: Ollama with Phi3 Mini model. Other models I have tested with are Mistral, Llama and Qwen
- **Local Vector Store**: DocArrayInMemorySearch
- **Local Processing**: Embedding and retrieval operations

## Features

### 1. Environment Setup (Cells 1-6)
- Checks the current working directory
- Creates a test notebook file
- Lists files in the directory

### 2. LLM Testing (Cell 7)
- Tests the Ollama LLM with the Phi3 Mini model locally
- Asks a simple question about the Sword Coast

### 3. PDF Processing with OCR (Cell 8)
- Extracts text from a scanned PDF ("Sword Coast Adventurer's Guide.pdf") using OCR
- Uses Tesseract and Poppler to convert PDF pages to images and extract text
- Splits the extracted text into chunks (1000 characters with 500 overlap)
- Creates document chunks for retrieval

### 4. Prompt Template Setup (Cell 9)
- Creates a prompt template that instructs the LLM to answer in one short, concise sentence
- Includes context and question placeholders

### 5. Output Parser (Cell 10)
- Sets up a string output parser to format LLM responses

### 6. Chain Creation (Cell 11)
- Creates a basic chain: `prompt → LLM → parser`

### 7. Vector Store & Embeddings (Cell 12)
- Creates embeddings for all document chunks using Ollama's Phi3 Mini model
- Stores them in an in-memory vector database (DocArrayInMemorySearch)

### 8. Retriever Setup (Cell 13)
- Configures a retriever with similarity search (k=5) to find relevant chunks
- Tests retrieval with a query about Calimshan

### 9. Full RAG Chain (Cell 14)
- Combines retriever + prompt + LLM + parser into a complete RAG pipeline
- Takes a question, retrieves relevant context, and generates an answer

### 10. Debugging Tools (Cells 15-17)
- **Cell 15**: Inspects what chunks the retriever returns for debugging
- **Cell 16**: Token counting utility to analyze chunk sizes and token distribution
- **Cell 17**: Searches all chunks for specific keywords to verify content is present

## Summary

This is a **local RAG system** that:
1. Extracts text from a scanned D&D PDF using OCR
2. Chunks the text into manageable pieces
3. Creates embeddings for semantic search
4. Uses retrieval + a local LLM to answer questions about the content

## Requirements

- Python 3.x
- Ollama with Phi3 Mini model
- Tesseract OCR
- Poppler

### Python Dependencies

Install the required packages:

```bash
pip install -r requirements.txt
```

Or manually install:
- langchain
- langchain-community
- langchain-ollama
- docarray
- pytesseract
- pdf2image
- Pillow
- tiktoken
- nbformat

## Usage

1. Install Python dependencies: `pip install -r requirements.txt`
2. Ensure Ollama is running with the Phi3 Mini model
3. Install Tesseract and Poppler on your system
4. Place your PDF file in the project directory
5. Open and run `local_rag_dnd_guidebook.ipynb` cells sequentially

## Note

The PDF file is not included in this repository due to GitHub's file size limitations. You'll need to provide your own PDF source document.
