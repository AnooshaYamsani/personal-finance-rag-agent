# 💰 Personal Finance RAG + Agent

An AI-powered Personal Finance Assistant built using **Python, RAG (Retrieval-Augmented Generation), LangChain, AI Agents, Pandas, and OpenAI**.

This project combines **structured transaction analysis** with **document-based question answering**. Pandas is used for accurate financial calculations, while RAG is used to retrieve relevant information from personal finance documents.

> **Note:** This project is implemented and demonstrated using a Jupyter Notebook. 

---

## 🎯 Project Objective

The goal of this project is to build a practical AI system that can:

* Analyze financial transactions
* Calculate spending by merchant
* Calculate spending by month
* Calculate spending by category
* Analyze income
* Analyze cash flow
* Search personal finance documents using RAG
* Retrieve relevant document information
* Use an AI agent to select the appropriate tool
* Reduce hallucinations by using financial data as the source of truth

---

## 🏗️ Project Architecture


                    User Question
                         │
                         ▼
                    AI Agent
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
      Transaction Tool          RAG Tool
         (Pandas)                    │
              │                     ▼
              │              Document Retrieval
              │                     │
              │                     ▼
              │              Relevant Chunks
              │                     │
              └──────────┬──────────┘
                         ▼
                    Final Answer


## 📂 Project Structure


personal-finance-rag-agent/
│
├── data/
│   ├── transactions.csv
│   ├── bank_statement.txt
│   ├── utility_bills.txt
│   ├── insurance_policy.txt
│   └── subscriptions.txt
│
├── notebooks/
│   └── personal_finance_rag_agent.ipynb
│
├── README.md
├── requirements.txt
└── .env

---

## 📊 Data Sources

The project uses **synthetic financial data** for demonstration and learning purposes.

### Structured Data

`transactions.csv` contains:

* Date
* Description
* Category
* Amount
* Type
* Month

Example transactions include:

Tesco Supermarket
Amazon
Netflix
British Gas
Council Tax
Spotify
Pizza House
Gym Membership
Salary - ABC Technologies


### Unstructured Documents

The RAG system works with:

* Bank statement
* Utility bills
* Insurance policy
* Subscription information

---

# 🔎 RAG Pipeline

The document-based questions follow a standard RAG pipeline:

Financial Documents
        │
        ▼
   Load Documents
        │
        ▼
    Split Text
        │
        ▼
   Create Chunks
        │
        ▼
     Embeddings
        │
        ▼
   Vector Store
        │
        ▼
     Retriever
        │
        ▼
 Relevant Chunks
        │
        ▼
       LLM
        │
        ▼
    Final Answer


The project uses:


RecursiveCharacterTextSplitter(
    chunk_size=800,
    chunk_overlap=100
)


The documents are divided into smaller chunks before being converted into embeddings and stored for retrieval.

---

# 🤖 AI Agent

The project uses an AI agent to determine which tool should be used for a particular question.

The agent has access to two main tools.

### 1. Document Search Tool


search_finance_documents


This tool is used for questions related to information stored in the financial documents.

Example:


Question:
What does my insurance policy cover?


The agent can use the document search tool to retrieve the relevant information.

---

### 2. Transaction Analysis Tool


analyze_finance_transactions


This tool uses Pandas to analyze the structured transaction dataset.

Example:


Question:
How much did I spend at Tesco?


The transaction analysis tool searches the transaction data and calculates the exact amount.

---

# 📈 Transaction Analysis

Financial calculations are performed using **Pandas** instead of asking the LLM to calculate the values.

This makes the numerical results deterministic.

### Example 1 — Merchant Spending


Question:
How much did I spend at Tesco?

Answer:
£521.20


### Example 2 — Monthly Merchant Spending


Question:
How much did I spend at Tesco in March?

Answer:
£194.20


### Example 3 — Unknown Merchant


Question:
How much did I spend at G&Co?

Answer:
I cannot answer this transaction question yet.


The system does not invent a transaction when the merchant does not exist in the dataset.

---

# 🛡️ Hallucination Prevention

Financial applications require reliable numerical answers.

Therefore, this project follows an important design principle:


Transaction Data
       │
       ▼
     Pandas
       │
       ▼
Exact Calculation
       │
       ▼
    Final Answer

The LLM is **not responsible for calculating transaction totals**.

Instead:


LLM / Agent
     │
     ▼
Select appropriate tool
     │
     ▼
Pandas performs calculation
     │
     ▼
Return actual result


This approach helps reduce the risk of hallucinated financial amounts.

---

# 🧠 Example Questions

The project can handle different types of questions.

### Transaction Questions


How much did I spent on gym?

How much did I spend at Tesco in March?

How much did I spend at Amazon?

What is my total spending?

What is my total income?

What is my cash flow?


### Category Questions


How much did I spend on groceries?

Show my spending by category.

What are my major spending categories?


### Document Questions


What does my insurance policy cover?

What information is available in my bank statement?

What are my utility bills?

What subscriptions do I have?


---

# 🧪 Testing

The project includes testing of both transaction analysis and RAG functionality.

### Transaction Testing

Example:


Input:
How much did I spent on gym?

Expected:
£105.00



Input:
How much did I spend at Tesco in March?

Expected:
£194.20


Input:
How much did I spend at Pizza House in January?

Expected:
£32.50


Input:
How much did I spend at G&Co?

Expected:
I cannot answer this transaction question yet.


These tests verify that the system uses the actual transaction dataset instead of generating unsupported values.

---

# 🛠️ Technologies Used

| Technology       | Purpose                          |
| ---------------- | -------------------------------- |
| Python           | Main programming language        |
| Jupyter Notebook | Development and demonstration    |
| Pandas           | Transaction analysis             |
| LangChain        | LLM and RAG framework            |
| AI Agents        | Tool selection and orchestration |
| OpenAI           | Language model and embeddings    |
| Vector Store     | Document retrieval               |
| Python-dotenv    | Environment variable management  |
| Git              | Version control                  |
| GitHub           | Project repository               |

---

# 🔐 API Key Configuration

The project uses an OpenAI API key.

The key is stored locally in a .env file.

Example:

OPENAI_API_KEY=your_api_key_here


The .env file should **not** be uploaded to GitHub.

Add the following to .gitignore`:

.env


This prevents the API key from being accidentally exposed.

---

# ⚙️ Installation

Clone the repository:


git clone <your-github-repository-url>


Move into the project directory:


cd personal-finance-rag-agent


Create and activate a virtual environment if required.

Install the project dependencies:


pip install -r requirements.txt


Start Jupyter Notebook:


jupyter notebook


Open:

notebooks/personal_finance_rag_agent.ipynb

Run the notebook cells step by step.

---

# ▶️ How to Run the Project

### Step 1 — Load the transaction data

import pandas as pd

df = pd.read_csv("data/transactions.csv")


### Step 2 — Load financial documents

The project loads the .txt documents from the data folder.

### Step 3 — Split documents into chunks

The documents are divided into smaller chunks using a text splitter.

### Step 4 — Create embeddings

Document chunks are converted into vector representations.

### Step 5 — Create the retriever

The vector store is used to retrieve relevant document chunks.

### Step 6 — Create the RAG pipeline

The retrieved information is passed to the language model to generate an answer.

### Step 7 — Create transaction analysis

Pandas is used to calculate financial values directly from `transactions.csv`.

### Step 8 — Create tools

The RAG search and transaction analysis functions are exposed as tools.

### Step 9 — Create the AI agent

The agent can select the appropriate tool based on the user's question.

### Step 10 — Test the system

Different transaction and document questions are tested in the notebook.

---

# 📌 Important Design Decision

This project separates **reasoning** from **financial calculations**.


                 AI Agent
                    │
          ┌─────────┴─────────┐
          │                   │
          ▼                   ▼
      RAG Search        Pandas Analysis
          │                   │
          ▼                   ▼
    Documents             CSV Data
          │                   │
          └─────────┬─────────┘
                    ▼
               Final Answer


The agent determines **which tool is required**.

Pandas performs **financial calculations**.

RAG performs **document retrieval**.

The LLM generates natural-language responses from the retrieved information.


# 🚀 Future Improvements

Future versions of the project could include:

* Expense forecasting
* Budget recommendations
* Spending trend analysis
* Monthly financial reports
* Automatic expense categorization
* Financial dashboards
* More advanced agent workflows
* Multiple specialized financial agents
* Database integration
* Cloud deployment
* Evaluation and monitoring
* API deployment using FastAPI

A future version can also introduce a user interface if required.

---

# 🎓 Learning Outcomes

Through this project, I practiced:

* Python programming
* Pandas data analysis
* Working with CSV data
* Working with unstructured documents
* Document loading
* Text splitting
* Embeddings
* Vector search
* Retrieval-Augmented Generation (RAG)
* LangChain
* AI agents
* Tool calling
* Prompt engineering
* Environment variables
* API integration
* Git and GitHub
* Jupyter Notebook development
* Hallucination prevention
* Building AI applications using real-world architecture

---


# Disclaimer

This project uses synthetic financial data and is intended for educational and demonstration purposes only.

It is not intended to provide professional financial, investment, tax, or legal advice.

---

#  Author

** Anoosha Yamsani **

AI Engineer | Python | Generative AI | RAG | AI Agents

---

## ⭐ Project Highlights


Python
  +
Pandas
  +
RAG
  +
Vector Search
  +
LLM
  +
AI Agents
  =
Personal Finance AI System


This project demonstrates how traditional Python data analysis can be combined with modern Generative AI techniques to build a practical AI application.
