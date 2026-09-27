# 🧪 LabMate AI

> **Your AI-powered laboratory manual assistant.**

LabMate AI is a Retrieval-Augmented Generation (RAG) based assistant designed to help engineering students understand and revise their laboratory manuals.

Instead of requiring students to search through lengthy PDF laboratory manuals manually, LabMate extracts the content, converts it into searchable semantic representations, retrieves the most relevant sections for a question, and uses an LLM to generate an answer grounded in the retrieved material.

---

## 🎯 Problem

Engineering students often have to work with lengthy laboratory manuals containing experiments, procedures, principles, formulas, observations, and precautions.

Finding the relevant information quickly can be difficult, especially while preparing for:

* Laboratory sessions
* Viva examinations
* Practical assessments
* Experiment preparation
* Quick revision

Generic AI chatbots can answer questions, but they may not be specifically grounded in the student's laboratory manual and can potentially generate information that is not present in the uploaded material.

---

## 💡 Solution

LabMate AI allows students to upload their laboratory manuals and ask questions about their contents.

The application:

1. Extracts text from uploaded PDFs.
2. Splits the extracted text into smaller chunks.
3. Converts the chunks into numerical embeddings.
4. Stores the embeddings in a vector database.
5. Converts the student's question into an embedding.
6. Retrieves the most relevant sections of the laboratory manual.
7. Sends the retrieved context to an LLM.
8. Generates an answer based on the retrieved laboratory material.

### Architecture

```text
                 Laboratory PDF
                       │
                       ▼
                PDF Text Extraction
                   (pdfplumber)
                       │
                       ▼
                    Chunking
                       │
                       ▼
                   Embeddings
                (Sentence Transformers)
                       │
                       ▼
                   ChromaDB
                Vector Database
                       │
                       │
             Student asks a question
                       │
                       ▼
              Query Embedding
                       │
                       ▼
             Similarity Search
                  (ChromaDB)
                       │
                       ▼
             Relevant PDF Chunks
                       │
                       ▼
                    Gemini
                      LLM
                       │
                       ▼
               Generated Answer
```

---

## 🚀 Features

### 📄 Multiple PDF Upload

Students can upload laboratory manuals in PDF format and index their contents for semantic search.

### 🔎 Semantic Retrieval

Instead of relying only on exact keyword matching, LabMate converts both the manual content and the student's question into embeddings and retrieves semantically relevant information.

### 🧠 Retrieval-Augmented Generation

The retrieved laboratory-manual content is provided to the LLM as context before generating the answer.

This helps keep responses grounded in the uploaded material.

### 🧪 Experiment-Oriented Learning

The application is designed around laboratory experiments, allowing students to interact with their practical manuals rather than treating the document as a generic chatbot knowledge source.



---

## 🛠️ Technologies Used

| Technology            | Purpose                               |
| --------------------- | ------------------------------------- |
| Python                | Core application logic                |
| Streamlit             | Web application interface             |
| pdfplumber            | PDF text extraction                   |
| Sentence Transformers | Text embeddings                       |
| ChromaDB              | Vector database and similarity search |
| Gemini API            | LLM-powered answer generation         |

---

## 🔄 How RAG Works in LabMate

LabMate uses a Retrieval-Augmented Generation architecture.

### 1. Document Processing

When a student uploads a PDF, `pdfplumber` extracts the text from the document.

### 2. Chunking

The extracted text is divided into smaller overlapping chunks.

This allows individual sections of the manual to be retrieved instead of processing the entire document for every question.

### 3. Embedding

Each chunk is converted into a vector representation using a sentence-transformer embedding model.

These vectors represent the semantic meaning of the text.

### 4. Vector Storage

The chunks and their embeddings are stored in ChromaDB.

### 5. Question Retrieval

When a student asks a question, the question is also converted into an embedding.

ChromaDB searches for the chunks that are semantically most similar to the question.

### 6. Answer Generation

The retrieved chunks are passed as context to the Gemini LLM.

The LLM then generates the final response using the retrieved laboratory-manual information.

---

## 🆚 Why Not Just Upload the PDF to ChatGPT?

LabMate is specifically designed around **laboratory-manual retrieval and interaction**.

Its architecture separates:

**Document processing → semantic retrieval → contextual generation**

Instead of simply treating the PDF as a general conversation attachment, LabMate builds a searchable vector representation of the laboratory material.

This makes it possible to retrieve the most relevant sections before generating an answer.

The project is also designed specifically around the workflow of engineering laboratory learning and experimentation.

---

## 📂 Project Structure

```text
lab-manual-assistant/
│
├── app.py
├── chunking.py
├── embeddings.py
├── vector_store.py
├── pdf_utils.py
├── llm.py
├── requirements.txt
├── .gitignore
├── README.md
│
└── chroma_db/
```

### File Responsibilities

**`app.py`**

Main Streamlit application and user interface.

**`pdf_utils.py`**

Extracts text from uploaded PDF laboratory manuals.

**`chunking.py`**

Splits extracted text into smaller overlapping chunks.

**`embeddings.py`**

Creates embeddings for document chunks and user questions.

**`vector_store.py`**

Stores and retrieves document chunks using ChromaDB.

**`llm.py`**

Handles communication with the Gemini API.

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/Govardhangowda/lab-manual-assistant.git
cd lab-manual-assistant
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

### 3. Activate the virtual environment

On Windows:

```bash
.venv\Scripts\activate
```

### 4. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 5. Configure the Gemini API key

Create a `.env` file:

```text
GEMINI_API_KEY=your_api_key_here
```

**Do not commit your `.env` file or API key to GitHub.**

### 6. Run the application

```bash
python -m streamlit run app.py
```

The Streamlit application will open in your browser.

---

## 🧪 Example Workflow

```text
Upload Laboratory Manual
          ↓
Select / interact with experiment
          ↓
Ask a question
          ↓
Retrieve relevant manual content
          ↓
Send retrieved context to Gemini
          ↓
Generate grounded response
```

Example:

> **Question:** What is the principle of the Air Wedge experiment?

LabMate retrieves relevant information from the uploaded manual and uses that information to generate the response.

---

## 🔐 API Key Security

API keys should never be uploaded to GitHub.

The project uses environment variables through `.env`.

Make sure `.env` is included in `.gitignore`.

---

## 📌 Project Status

**Prototype / Hackathon Project**

LabMate AI is currently a working prototype demonstrating a laboratory-manual RAG pipeline.

The current focus is on:

* PDF processing
* Semantic search
* Vector retrieval
* LLM-based answer generation
* Laboratory-focused interaction

---

## 👥 Team

**LabMate AI**

Built as a student AI project focused on improving the way engineering students interact with laboratory manuals.

---

## 📜 License

This project is released under the **MIT License**.
