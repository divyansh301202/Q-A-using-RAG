# Q-A-using-RAG

# Document-based Question Answering System using RAG

A Retrieval-Augmented Generation (RAG) system that allows users to ask questions based on the content of documents (e.g., NCERT books or PDFs). This project extracts content from PDFs, stores them as vector embeddings in a PostgreSQL database (with pgvector), and uses an LLM to generate answers based on retrieved relevant context.

---

## Features

- Supports PDF document ingestion and OCR (Tesseract)
- Smart chunking using titles, paragraphs, or characters
- Stores document chunks with source metadata (filename, page number)
- Embedding via HuggingFace (`all-MiniLM-L6-v2`)
- Fast similarity search using PostgreSQL + pgvector
- Context-aware question answering using Cohere or HuggingFace LLMs
- Optional filtering by document
- Return top N relevant chunks with full traceability

---


## Installation

### Prerequisites

- Python 3.10 or higher
- Git
- [PostgreSQL](https://www.postgresql.org/) with [pgvector extension](https://github.com/pgvector/pgvector)
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)
- [Poppler](https://github.com/oschwartz10612/poppler-windows) for PDF image extraction

### Setup Steps


# Clone the repository
git clone https://github.com/<your-username>/Q_A.git
cd Q_A

# Create and activate virtual environment
python -m venv .venv
.venv\Scripts\activate  # On Windows
# source .venv/bin/activate  # On Linux/macOS

# Install Python dependencies
pip install -r requirements.txt

Required Tools Setup
1. Tesseract OCR
Download from: https://github.com/tesseract-ocr/tesseract

Add its installation folder (e.g., C:\Program Files\Tesseract-OCR) to your system PATH.

2. Poppler (for pdf2image)
Download from: https://github.com/oschwartz10612/poppler-windows/releases

Extract and add poppler-xx\Library\bin to your system PATH.

3. 🐘 PostgreSQL with pgvector
Install PostgreSQL: https://www.postgresql.org/download/

Enable the pgvector extension in your database:
CREATE EXTENSION IF NOT EXISTS vector;

#Environment Setup
Create a .env file in your root directory:

COHERE_API_KEY=your_cohere_api_key
POSTGRES_USER=your_db_user
POSTGRES_PASSWORD=your_db_password
POSTGRES_DB=your_db_name
POSTGRES_HOST=localhost
POSTGRES_PORT=5432

#Document Ingestion Pipeline
Extract text (and OCR images if needed) from PDF

Chunk text using RecursiveCharacterTextSplitter or by title

Generate vector embeddings via HuggingFace

Store chunks + metadata in PostgreSQL (with vector)

#Ask Questions
The app retrieves top-k relevant document chunks and uses an LLM to generate a final answer.

> Enter filename to search: ncert_class_12.pdf
> Ask a question: What is the function of mitochondria?

Answer: Mitochondria are the powerhouses of the cell...
Source: ncert_class_12.pdf | Page: 15

#Tech Stack
LangChain – for chaining retrieval and generation

HuggingFace Transformers – for embeddings and models

Cohere – LLMs for answer generation (you can swap with OpenAI or local LLMs)

PostgreSQL + pgvector – vector DB

Tesseract – OCR for scanned PDFs

Poppler + pdf2image – for converting PDF pages to images

Unstructured.io – for PDF parsing and chunking (high accuracy)


