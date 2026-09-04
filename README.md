# AI Contract Analyzer

AI-powered contract analysis platform designed to automatically extract structured information from PDF contracts and allow users to ask natural-language questions about their documents.

The application combines **document processing**, **Natural Language Processing (NLP)**, and a **multilingual Transformer model** with a FastAPI backend and two available frontend interfaces.

## Features

* Upload and analyze PDF contracts
* Automatic PDF text extraction
* Structured contract information extraction
* Extract contract number
* Identify client and supplier
* Extract contract object
* Detect total amount and currency
* Identify contract location
* Ask questions directly about uploaded contracts
* Multilingual AI question answering
* REST API architecture
* Streamlit user interface
* HTML/CSS/JavaScript web interface
* Automatic FastAPI API documentation

## AI & NLP

The application uses a multilingual Transformer-based question-answering model:

```text
mrm8488/bert-multi-cased-finetuned-xquadv1
```

The model is loaded using the Hugging Face `transformers` pipeline.

For larger contracts, extracted text is divided into smaller chunks. The AI model analyzes each chunk and selects the answer with the highest confidence score.

Structured information is extracted using a combination of:

* Regular expressions
* PDF text extraction
* Natural Language Processing
* Transformer-based Question Answering

## Extracted Contract Data

The system can extract information such as:

```text
Contract Number
Supplier
Client
Object
Total Amount
Currency
Date
Location
```

## Tech Stack

### Backend

* Python
* FastAPI
* Uvicorn
* Pydantic
* PyMuPDF
* Hugging Face Transformers
* PyTorch
* Regular Expressions
* REST APIs

### Frontend

Two frontend implementations are included.

**Streamlit**

* Streamlit
* Python
* Pandas
* Requests

**Web**

* HTML5
* CSS3
* JavaScript

## Project Structure

```text
.
├── backend/
│   ├── main.py
│   └── contract_extractor.py
│
├── frontend_streamlit/
│   ├── app.py
│   └── ocp_logo.png
│
├── frontend_web/
│   ├── index.html
│   ├── style.css
│   ├── script.js
│   └── assets
│
├── GUIDE.md
└── requirements.txt
```

## Architecture

```text
             ┌─────────────────┐
             │   PDF Contract  │
             └────────┬────────┘
                      │
                      ▼
             ┌─────────────────┐
             │    FastAPI API  │
             └────────┬────────┘
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
 ┌────────────────┐      ┌────────────────┐
 │ PDF Extraction │      │  Contract Q&A  │
 │    PyMuPDF     │      │ Transformers   │
 └───────┬────────┘      └───────┬────────┘
         │                       │
         └───────────┬───────────┘
                     ▼
             ┌─────────────────┐
             │ Structured Data │
             │   + AI Answers  │
             └─────────────────┘
                     │
              ┌──────┴──────┐
              ▼             ▼
        ┌───────────┐ ┌───────────┐
        │ Streamlit │ │ Web UI    │
        └───────────┘ └───────────┘
```

## Installation

Clone the repository:

```bash
git clone https://github.com/mchemchaq/PFA_OCP.git
cd PFA_OCP
```

It is recommended to create a virtual environment:

```bash
python -m venv venv
```

Activate it.

### macOS / Linux

```bash
source venv/bin/activate
```

### Windows

```bash
venv\Scripts\activate
```

Upgrade pip:

```bash
pip install --upgrade pip setuptools wheel
```

Install the required dependencies:

```bash
pip install fastapi uvicorn pydantic python-multipart PyMuPDF transformers torch streamlit pandas requests
```

## Running the Backend

Navigate to the backend:

```bash
cd backend
```

Start the FastAPI server:

```bash
uvicorn main:app --reload --port 8000
```

The API will be available at:

```text
http://localhost:8000
```

Interactive API documentation:

```text
http://localhost:8000/docs
```

## Running the Streamlit Frontend

From the project root:

```bash
cd frontend_streamlit
streamlit run app.py
```

The Streamlit interface will normally be available at:

```text
http://localhost:8501
```

Make sure the FastAPI backend is running before using the frontend.

## Running the Web Frontend

From the project root:

```bash
cd frontend_web
python -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

## API Endpoints

### Health Check

```http
GET /
```

Checks whether the API is running.

### Extract Contract Information

```http
POST /extract/
```

Accepts a PDF contract and returns:

* Structured contract data
* Full extracted document text

### Ask a Contract Question

```http
POST /chat/
```

Example request:

```json
{
  "full_contract_text": "Contract text...",
  "question": "What is the total contract amount?"
}
```

Example response:

```json
{
  "answer": "500,000 MAD"
}
```

## Example Workflow

1. Upload a PDF contract.
2. The backend extracts the document text using PyMuPDF.
3. Contract fields are identified automatically.
4. Structured information is returned to the frontend.
5. The extracted contract text becomes the context for the AI model.
6. Users can ask natural-language questions about the contract.
7. The Transformer model searches the contract and returns the most relevant answer.

## Skills Demonstrated

This project demonstrates experience with:

* Artificial Intelligence
* Natural Language Processing
* Transformer Models
* Hugging Face
* BERT
* Document AI
* Question Answering Systems
* Python
* FastAPI
* REST API Development
* PDF Processing
* PyMuPDF
* PyTorch
* Streamlit
* JavaScript
* HTML & CSS
* API Integration
* Data Extraction
* Text Processing
* Regular Expressions
* Backend Development

## Possible Improvements

Future improvements could include:

* OCR support for scanned contracts
* Vector embeddings and semantic search
* Retrieval-Augmented Generation (RAG)
* Support for additional document formats
* Contract summarization
* Clause detection and classification
* Risk and anomaly detection
* Contract comparison
* Authentication and user accounts
* Persistent document storage
* Conversation history
* Docker containerization
* Automated testing
* Production-ready CORS configuration
* Improved confidence scoring
* Support for larger documents

## Author

**mchemchaq**

GitHub: https://github.com/mchemchaq

## Disclaimer

This project was developed for educational and demonstration purposes. Extracted information and AI-generated answers should be reviewed before being used for legal or business decisions.
