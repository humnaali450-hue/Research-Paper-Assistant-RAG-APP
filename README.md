# 🤖 Research Paper Assistant — RAG Application

An AI-powered **Research Paper Assistant** built with **Retrieval-Augmented Generation (RAG)** that enables users to upload research papers in PDF format and ask natural-language questions about their content.

The application extracts and processes document text, divides it into meaningful chunks, generates semantic embeddings using **Sentence Transformers**, stores the embeddings in a **FAISS vector database**, and retrieves the most relevant information to provide context-aware answers using a **local Ollama LLM**.

The system is designed to answer questions **strictly based on the uploaded research paper**, making it useful for reading, exploring, and understanding academic documents.

---

## 🚀 Key Features

* 📄 **PDF Research Paper Upload**

  * Upload research papers directly through the Streamlit interface.

* 🔎 **Document Text Extraction**

  * Extracts textual content from uploaded PDF documents for further processing.

* ✂️ **Smart Text Chunking**

  * Splits large documents into smaller chunks to improve retrieval accuracy.

* 🧠 **Semantic Embeddings**

  * Uses Sentence Transformers with the **MiniLM** model to convert text chunks into numerical vector representations.

* ⚡ **FAISS Vector Search**

  * Performs fast similarity searches to retrieve the most relevant document sections.

* 🤖 **Local LLM with Ollama**

  * Uses **TinyLlama** through Ollama to generate answers based on retrieved document context.

* 💬 **Question Answering**

  * Users can ask natural-language questions about the uploaded research paper.

* 🎯 **Context-Grounded Responses**

  * The model is instructed to answer using the retrieved document context rather than relying on unrelated information.

* 🎨 **Interactive Streamlit UI**

  * Provides a clean and user-friendly interface for document upload and question answering.

* 🔐 **Local AI Processing**

  * Uses locally hosted models through Ollama, reducing the need for external LLM APIs.

---

## 🏗️ System Architecture

The application follows a typical **Retrieval-Augmented Generation (RAG)** pipeline:

```text
                ┌─────────────────────┐
                │   Upload PDF Paper  │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   Extract PDF Text  │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │    Text Chunking    │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Generate Embeddings │
                │    MiniLM Model     │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   FAISS Vector DB   │
                └──────────┬──────────┘
                           │
                    User Question
                           │
                           ▼
                ┌─────────────────────┐
                │ Similarity Search   │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │ Relevant Chunks     │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   Ollama / LLM      │
                │     TinyLlama       │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │   Generated Answer  │
                └─────────────────────┘
```

---

## 🛠️ Tech Stack

| Technology                | Purpose                         |
| ------------------------- | ------------------------------- |
| **Python**                | Core programming language       |
| **Streamlit**             | Interactive web application     |
| **PyPDF2 / PDF Library**  | PDF text extraction             |
| **Sentence Transformers** | Text embedding generation       |
| **MiniLM**                | Semantic embedding model        |
| **FAISS**                 | Vector similarity search        |
| **Ollama**                | Local LLM inference             |
| **TinyLlama**             | Local language model            |
| **NumPy**                 | Numerical and vector operations |


---

### 2. Create a Virtual Environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### macOS / Linux

```bash
python -m venv venv
source venv/bin/activate
```

---

### 3. Install Dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

---

## 🤖 Ollama Setup

This project uses **Ollama** to run the LLM locally.

First, install Ollama on your system and make sure the Ollama service is running.

Then pull the TinyLlama model:

```bash
ollama pull tinyllama
```

You can verify that the model is available with:

```bash
ollama list
```

The application should be able to access the locally running Ollama service before starting the Streamlit application.

---

## ▶️ Run the Application

After activating the virtual environment and configuring Ollama, run:

```bash
streamlit run app_streamlit.py
```

Streamlit will provide a local URL where you can access the application in your browser.

---

## 💡 How to Use

### Step 1 — Upload a Research Paper

Upload a research paper in **PDF format** through the Streamlit interface.

### Step 2 — Process the Document

The application:

1. Extracts text from the PDF.
2. Splits the text into smaller chunks.
3. Generates embeddings for each chunk.
4. Stores the embeddings in FAISS.

### Step 3 — Ask a Question

Enter a question related to the uploaded paper.

For example:

```text
What is the main objective of this research?
```

or:

```text
What methodology was used in the study?
```

or:

```text
What are the key findings of the paper?
```

### Step 4 — Retrieve Relevant Context

FAISS searches the document embeddings and identifies the text chunks most relevant to the question.

### Step 5 — Generate the Answer

The retrieved context is provided to TinyLlama through Ollama, which generates the final response.

---

## 🧠 Retrieval-Augmented Generation (RAG)

The core of this project is the **RAG architecture**.

Instead of directly asking an LLM to answer a question, the application first searches the uploaded document for relevant information.

The process can be represented as:

```text
User Question
      ↓
Question Embedding
      ↓
FAISS Similarity Search
      ↓
Relevant Document Chunks
      ↓
Context + Question
      ↓
Local LLM (TinyLlama)
      ↓
Final Answer
```

This approach helps the application provide responses that are grounded in the content of the uploaded research paper.

---

## 🔍 Why FAISS?

**FAISS (Facebook AI Similarity Search)** is used as the vector search engine.

Research papers can contain thousands of sentences, making direct keyword-based searching less effective for understanding semantic relationships.

FAISS enables efficient similarity searches over the generated embeddings and helps identify document chunks that are semantically related to the user's question.

---

## 🧠 Why Sentence Transformers?

Traditional keyword search may fail when the user's question uses different words from the research paper.

Sentence Transformers generate **semantic embeddings**, allowing the system to compare the meaning of the question with the meaning of document chunks.

For example:

```text
Question:
"What approach did the researchers use?"

Document:
"The study employed a deep learning-based methodology..."
```

Although the wording is different, semantic embeddings can identify the relationship between the two pieces of text.

---

## 🤖 Local LLM with Ollama

The project uses **TinyLlama** through Ollama for local text generation.

Running the model locally provides several advantages:

* No external LLM API is required.
* Documents can remain on the local machine.
* No API key is required for inference.
* Suitable for experimentation with private documents.
* Provides an introduction to local LLM deployment.

---

## 📊 Example Workflow

```text
📄 Research Paper
       ↓
📖 PDF Text Extraction
       ↓
✂️ Text Chunking
       ↓
🧠 MiniLM Embeddings
       ↓
🔍 FAI
```
