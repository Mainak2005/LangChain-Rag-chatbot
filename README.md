# 🤖 LangChain RAG Basic Chatbot

A basic **Retrieval-Augmented Generation (RAG) chatbot** built using **LangChain, Hugging Face, FAISS, Sentence Transformers, and FLAN-T5**.

This project allows users to upload a PDF document and ask questions about its content. The system retrieves the most relevant sections from the document and uses a language model to generate an answer based on the retrieved context.

## 🚀 Project Overview

This project demonstrates how to build a simple document-question-answering system using RAG.

### RAG Pipeline

```text
        📄 PDF Document
              ↓
       PyPDFLoader
              ↓
       Text Chunking
              ↓
   Hugging Face Embeddings
              ↓
        FAISS Vector DB
              ↓
         Retriever
              ↓
    Relevant Document Chunks
              ↓
       Prompt Template
              ↓
         FLAN-T5 Model
              ↓
        🤖 Final Answer
```

## ✨ Features

* 📄 Upload and process PDF documents
* 🔍 Extract text from PDF pages
* ✂️ Split documents into smaller chunks
* 🧠 Generate semantic embeddings
* 🗃️ Store embeddings using FAISS
* 🔎 Retrieve the most relevant document chunks
* 🤖 Generate answers using FLAN-T5
* 📚 Answer questions based on the uploaded document
* 🛡️ Instruct the model not to answer when information is unavailable in the document

## 🛠️ Technologies Used

* **Python**
* **LangChain**
* **LangChain Community**
* **Hugging Face**
* **Sentence Transformers**
* **FAISS**
* **PyPDF**
* **Transformers**
* **PyTorch**
* **Google Colab**

## 🧠 Models Used

### Embedding Model

```text
sentence-transformers/all-MiniLM-L6-v2
```

Used to convert document chunks into vector embeddings for semantic similarity search.

### Language Model

```text
google/flan-t5-base
```

Used to generate answers based on the retrieved document context.

## 📦 Installation

Install the required dependencies:

```bash
pip install -q langchain langchain-community langchain-huggingface langchain-text-splitters pypdf faiss-cpu sentence-transformers transformers torch
```

Or create a `requirements.txt` file:

```text
langchain
langchain-community
langchain-huggingface
langchain-text-splitters
pypdf
faiss-cpu
sentence-transformers
transformers
torch
```

Then run:

```bash
pip install -r requirements.txt
```

## ▶️ How to Run

### Using Google Colab

1. Open the notebook in Google Colab.
2. Install the required dependencies.
3. Run the notebook cells.
4. Upload a PDF document when prompted.
5. The document will be loaded and split into chunks.
6. Embeddings will be generated for the chunks.
7. FAISS will create the vector database.
8. Ask questions about the uploaded document.
9. The RAG pipeline will retrieve relevant information and generate an answer.

## 🔍 How the RAG System Works

### 1. PDF Loading

The uploaded PDF is processed using `PyPDFLoader`.

```python
loader = PyPDFLoader(pdf_name)
documents = loader.load()
```

### 2. Text Splitting

The document is divided into smaller chunks.

```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=50
)
```

Current configuration:

* **Chunk size:** 500
* **Chunk overlap:** 50

### 3. Embeddings

Each document chunk is converted into a numerical vector using:

```python
sentence-transformers/all-MiniLM-L6-v2
```

### 4. Vector Database

The embeddings are stored in a **FAISS** vector database.

```python
vectorstore = FAISS.from_documents(
    chunks,
    embeddings
)
```

### 5. Retrieval

The retriever searches for the most relevant document chunks.

```python
retriever = vectorstore.as_retriever(
    search_kwargs={"k": 3}
)
```

The system retrieves the **top 3 relevant chunks**.

### 6. Prompt Generation

The retrieved content is passed to a prompt that instructs the model to use only the supplied context.

```text
Answer the question using ONLY the context provided below.

If the answer is not present in the context, say:
"I don't know based on the provided document."
```

### 7. Answer Generation

The retrieved context and question are passed through the RAG chain, which generates the final answer using FLAN-T5.

## 💬 Example Questions

The project demonstrates questions such as:

```text
What is HRSID?

What is the purpose of the HRSID dataset?

What type of images are used in HRSID?

What is SAR?

What are the challenges in ship detection?
```

## 📂 Project Structure

```text
LangChain-RAG-Basic-Chatbot/
│
├── langchain_rag_basic_chatbot.py
├── README.md
├── requirements.txt
└── sample/
    └── document.pdf
```

If using Google Colab:

```text
LangChain-RAG-Basic-Chatbot/
│
├── LangChain_RAG_basic_chatbot.ipynb
├── README.md
└── requirements.txt
```

## 🎯 Learning Objectives

This project provides practical experience with:

* Retrieval-Augmented Generation (RAG)
* LangChain
* Document processing
* PDF loading
* Text chunking
* Semantic search
* Embeddings
* Vector databases
* FAISS
* Hugging Face models
* Prompt engineering
* Document-based question answering

## 🔮 Future Improvements

Some possible improvements include:

* 🌐 Build a Streamlit web interface
* 💬 Add conversational chat history
* 📑 Support multiple PDF documents
* 💾 Persist the FAISS vector database
* 📌 Display source pages with answers
* 🔎 Show retrieved document chunks
* 🧠 Experiment with different embedding models
* 🤖 Experiment with larger language models
* ☁️ Deploy the chatbot as a web application
* 📤 Add drag-and-drop document uploading

## ⚠️ Limitations

This is a **basic RAG implementation** intended for learning and demonstration.

* The vector database is created during execution.
* The implementation does not currently provide a web UI.
* Chat history is not implemented.
* Answer quality depends on the uploaded document and retrieved chunks.
* Source citations are not currently displayed in the final generated answer.

## 📌 Project Highlights

> **PDF → Embeddings → FAISS → Retrieval → Prompt → FLAN-T5 → Answer**

This project demonstrates the fundamental architecture behind modern document-based AI assistants and provides a foundation for building more advanced RAG applications.

## 👨‍💻 Author

**Mainak Bal**

---

⭐ If you find this project useful, consider giving the repository a star!
