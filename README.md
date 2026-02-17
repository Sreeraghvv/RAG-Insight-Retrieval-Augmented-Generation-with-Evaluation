Retrieval-Augmented Generation (RAG) System with Evaluation
 Overview

This project implements a complete Retrieval-Augmented Generation (RAG) pipeline with automated evaluation.

The system retrieves relevant documents using dense embeddings and FAISS, refines them using a cross-encoder re-ranking model, generates answers using a local LLM (Ollama), and evaluates the responses using an LLM-as-a-judge approach.

The goal of this project is to move beyond simple generation and focus on measuring reliability, faithfulness, and answer quality.

 Architecture
User Query
    ↓
Text Embedding (Sentence Transformers)
    ↓
FAISS Vector Search
    ↓
Cross-Encoder Re-ranking
    ↓
LLM Generation (Ollama)
    ↓
LLM-as-Judge Evaluation
    ↓
Structured Evaluation Report (CSV)

 Tech Stack

Python

Sentence Transformers (all-MiniLM-L6-v2)

FAISS (Vector Similarity Search)

Cross-Encoder Re-ranking (ms-marco-MiniLM-L-6-v2)

Ollama (Local LLM: llama3 + phi3)

Pandas & NumPy

 Evaluation Metrics

The system evaluates answers using two core metrics:

1️ Faithfulness

Measures whether the generated answer is fully supported by the retrieved context.
Helps detect hallucinations.

2️ Relevance

Measures how well the generated answer addresses the original question.

All results are exported into a structured CSV file for analysis.

 Setup Instructions
1️ Clone the Repository
git clone <your-repo-url>
cd rag-project

2️ Install Dependencies
pip install -r requirements.txt

3️ Install and Start Ollama

Install Ollama from:
https://ollama.com

Start the server:

ollama serve


Pull required models:

ollama pull llama3
ollama pull phi3

4️ Run the Pipeline

From the src/ directory:

python pipeline.py

 Project Structure
rag-project/
│
├── src/
│   ├── embeddings.py
│   ├── retrieval.py
│   ├── rerank.py
│   ├── generator.py
│   ├── evaluation.py
│   └── pipeline.py
│
├── data/
│   └── documents.txt
│
├── evaluation_report.csv
├── requirements.txt
└── README.md

 Output

After running the pipeline, the system generates:

evaluation_report.csv


Containing:

Question

Generated Answer

Faithfulness Score

Relevance Score

This enables structured performance analysis and system improvement.

 Key Learnings

Retrieval quality directly impacts generation reliability.

Re-ranking improves contextual precision.

LLM-as-judge enables scalable automated evaluation.

Using separate models for generation and evaluation reduces bias.

Deterministic inference (temperature = 0) improves reproducibility.

 Future Improvements

Add Precision@K and MRR metrics

Integrate RAGAS for advanced evaluation

Build Streamlit UI

Deploy as FastAPI service

Add experiment tracking (MLflow)

Benchmark multiple LLMs

 Objective

This project demonstrates:

Understanding of embedding-based retrieval

Vector search implementation

LLM prompt control

Hallucination detection

Automated evaluation design

Modular and clean AI system architecture

