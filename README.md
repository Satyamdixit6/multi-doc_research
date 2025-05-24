# Chatbot Theme Identifier

## Overview

The Chatbot Theme Identifier is a web application that allows users to upload documents, interact with a Retrieval Augmented Generation (RAG) powered chatbot to ask questions about these documents, and identify key themes within the document corpus. It supports various document formats, utilizes local or OpenAI language and embedding models, and leverages a vector database (ChromaDB) for efficient information retrieval.

This guide focuses on running the application with a local Llama.cpp server.

## Features

* **Document Upload & Management:** Supports PDF, TXT, MD, DOCX, images for OCR, etc.
* **Conversational RAG Chat:** Ask questions and get answers sourced directly from your documents, with citations.
* **Theme Identification:** Extract key themes from specific documents, query context, or all processed documents.
* **Local First:** Designed to run with local LLMs (like a Llama.cpp server) and local embedding models.
* **User-Friendly Interface:** Built with Gradio.

## Prerequisites

* Python 3.8+
* Git
* **Tesseract OCR Engine:** For processing scanned documents/images.
    * Installation instructions: [https://tesseract-ocr.github.io/tessdoc/Installation.html](https://tesseract-ocr.github.io/tessdoc/Installation.html)
    * Ensure Tesseract and its language data are in your system's PATH.
* **Poppler:** For PDF processing, especially with OCR.
    * Often required by `pdf2image` and `unstructured`.
    * Windows users: Download from [Poppler for Windows](https://github.com/oschwartz10612/poppler-windows/releases/) and add the `bin/` directory to PATH.
    * Linux: `sudo apt-get install poppler-utils` or similar for your distribution.
    * MacOS: `brew install poppler`
* **Llama.cpp Server:** You need a running Llama.cpp server instance that exposes an OpenAI-compatible API endpoint.

## Project Structure
chatbot_theme_identifier_gradio/
├── app.py                     # Main Gradio application script
├── core/
│   ├── __init__.py
│   ├── settings.py            # Configuration (LLM endpoints, model names, etc.)
│   └── utils.py               # Utility functions
├── services/
│   ├── __init__.py
│   ├── document_processor.py  # Handles file loading, OCR, chunking
│   ├── vector_store_manager.py# Manages ChromaDB and embeddings
│   ├── rag_chain_builder.py   # Builds and manages Langchain RAG chains
│   └── theme_service.py       # For theme identification logic
├── data/                        # For uploaded documents and vector store
│   ├── uploaded_documents/
│   └── vector_store/


## Setup Instructions

**1. Clone the Repository**
   *(If you haven't already)*
   ```bash
   git clone Satyamdixit6/multi-doc_research
   cd chatbot_theme_identifier_gradio
   mkdir -p chatbot_theme_identifier_gradio/data/{uploaded_documents,vector_store}
   ./llama-server -ngl 99 -hf unsloth/gemma-3-1b-it-GGUF --port 8080 --host 0.0.0.0 --hf-token hf_OH******* 
   python app.py
