# FIND&FEED — Intelligent Knowledge Retrieval & RAG Architecture

FIND&FEED is an AI platform built for working with knowledge stored inside documents. Users can upload PDFs and interact with their content through questions. The system combines document processing, semantic retrieval, local vector search, and locally running language models to produce context-aware responses supported by document sources.

## Turning PDFs into an Interactive Knowledge Base

### Search Through Multiple PDFs

Multiple PDF documents can be uploaded and managed within the application. Users can select the documents they want to work with and search them for information relevant to their questions.

### Retrieve Before Generating

The platform uses Retrieval-Augmented Generation (RAG), where relevant content is retrieved from the documents before an answer is produced. This keeps the generated response grounded in the uploaded knowledge.

### Search by Meaning

Instead of depending only on matching words, document sections are converted into embeddings and compared through similarity search to locate information relevant to the user's question.

### Connect Answers to Their Sources

Generated responses are connected to relevant document sources, allowing users to determine where the information in the response originated.

### Expand Questions for Better Retrieval

The system creates alternative versions of a user's question when necessary. These additional queries help retrieve relevant content when the original wording does not directly match the wording in the documents.

### Keep AI Processing Local

Ollama handles both local language-model processing and embedding processing, reducing the system's dependence on external AI services.

### Ask Questions Through an AI Chat

Users can select documents and interact with them through a conversational chat interface, allowing questions to be asked as part of an ongoing conversation.

### Manage the Document Collection

The application supports the complete document-management flow, including PDF uploading, processing, listing, selection, and deletion.

## Architectural Approach

### Grounding the Model in Document Knowledge

Relevant document content is obtained before generation takes place. This enables the model to answer using the user's documents instead of depending solely on general knowledge.

### Keeping Data and AI Local

Ollama makes it possible to execute models locally, allowing both document content and AI processing to remain on the user's system.

### Improving Retrieval Accuracy

Semantic search and multi-query retrieval work together to locate useful information even when the wording used in the question differs from the wording present in the document.

### Separating Major Responsibilities

The system divides document processing, retrieval, AI generation, storage, and the user interface into separate components, maintaining a modular architecture.

## From PDF Upload to Source-Grounded Answer

### Step 1 — Prepare the Documents

Users upload PDF files. Their contents are extracted and broken into smaller text sections that can be searched.

### Step 2 — Build the Searchable Index

The extracted sections are converted into embeddings with a local embedding model and stored in ChromaDB, making them available for semantic search.

### Step 3 — Find the Relevant Information

When a question is submitted, it is expanded into relevant queries. These queries are matched against the stored document embeddings to locate useful sections.

### Step 4 — Generate with Retrieved Context

The retrieved sections are passed to a local Ollama model. The model uses the selected document context to generate the answer.

### Step 5 — Return Supporting Information

Relevant document information is delivered together with the response, enabling users to identify the content supporting the generated answer.

## Retrieval and Generation Flows

### Building the Document Index

`PDF → Text Extraction → Chunking → Embeddings → Vector Storage`

PDF content is extracted, divided into searchable sections, and then transformed into vector representations.

### Producing an Answer from a Question

`Question → Query Expansion → Semantic Retrieval → Context → Local LLM → Answer`

Relevant sections are retrieved from the documents and supplied to the local model so that it can generate an answer using the available context.

### Working Across Multiple PDFs

`Question → Selected PDFs → Retrieval → Relevant Chunks → Combined Context → Answer`

The system can search multiple selected PDFs, bring together their relevant content, and use the combined context to generate the final response.

## Technology Foundation

| Domain                  | Technologies                                       |
| :---------------------- | :------------------------------------------------- |
| **Frontend**            | Next.js, React, TypeScript, Tailwind CSS           |
| **Backend & API**       | Python, FastAPI, Uvicorn                           |
| **RAG Framework**       | LangChain                                          |
| **Local AI**            | Ollama, Local LLMs, Ollama Embeddings              |
| **Vector Search**       | ChromaDB                                           |
| **Document Processing** | PDFPlumber, Unstructured, LangChain Text Splitters |
| **Database**            | SQLite, SQLAlchemy                                 |
| **Development**         | Git, GitHub, pnpm                                  |

## Environment Requirements

The platform requires the following:

* Python 3.10+
* Node.js 18+
* pnpm
* Ollama
* A local Ollama language model
* `nomic-embed-text` or another compatible embedding model
* Git
