# AI-SQL-Bot
# LLM SQL AI Assistant   
_Natural-language to SQL Q&A over a MySQL retail dataset, powered by an LLM + few-shot retrieval + LangChain._

![Streamlit](https://img.shields.io/badge/UI-Streamlit-FF4B4B) ![DB](https://img.shields.io/badge/DB-MySQL-4479A1) ![LLM](https://img.shields.io/badge/LLM-Google%20PaLM-4285F4) ![Embeddings](https://img.shields.io/badge/Embeddings-all--MiniLM--L6--v2-6aa84f) ![VectorDB](https://img.shields.io/badge/VectorDB-Chroma-5B6DEF) ![LangChain](https://img.shields.io/badge/Framework-LangChain-000)

An end-to-end assistant that lets anyone query a MySQL database in plain English—no SQL required. Ask questions like:

- “How many white Adidas T-shirts in **XS** are in stock?”
- “If we sell all **Levi’s** shirts **today** after discounts, what revenue do we generate?”
- “What’s the **total inventory value** for size **S** across all brands?”

The app turns your question into safe MySQL, runs it on the **AtliQ T-Shirts** demo schema, and returns a crisp, human-readable answer in a **Streamlit** UI.

---

## ✨ Features

- **Natural-language to SQL** via a Large Language Model (Google PaLM via LangChain).
- **Few-shot + semantic retrieval** (Chroma + `all-MiniLM-L6-v2`) to pick the most relevant example SQL patterns.
- **MySQL-aware prompt** that avoids `SELECT *`, quotes identifiers with backticks, and respects the visible schema.
- **Business-friendly answers**: returns both the answer and the underlying SQL result.
- **Reproducible demo data**: ready-made SQL to create and seed a retail inventory/discount schema.

---

## 🧱 Project Structure
---
LLM-_SQL-AI-SQL-Assistant-main/
├─ main.py # Streamlit app (input box → answer)
├─ langchain_helper.py # LLM, DB chain, prompt, example selector
├─ few_shots.py # Few-shot examples for retrieval
├─ db_creation_atliq_t_shirts.sql # MySQL schema + seed data
├─ requirements.txt # Python dependencies
└─ t_shirt_sales_llm.ipynb # (Optional) Exploration notebook
---
## 🔧 Tech Stack

- **LLM**: `langchain.llms.GooglePalm` (temperature ~0.1)
- **Prompting**: `SQLDatabaseChain` with a **MySQL-specific prompt**, **FewShotPromptTemplate**, and **PROMPT_SUFFIX**
- **Embeddings**: `sentence-transformers/all-MiniLM-L6-v2`
- **Vector Store**: **Chroma** (`k=2` nearest examples per question)
- **Database**: **MySQL** (`atliq_tshirts` schema)
- **UI**: **Streamlit**
- **Env/Utils**: `python-dotenv`, `pymysql`/`mysql-connector-python`, `faiss-cpu` (optional), `langchain_experimental`

---

## 🚀 Quick Start

### 1) Prerequisites
- **Python** 3.10+  
- **MySQL** 8.x running locally (or reachable remotely)
- **Google PaLM / Generative AI API key** (set as `GOOGLE_API_KEY`)

> 💡 If you’re not using the default local MySQL root account, you’ll edit a few lines in `langchain_helper.py` to match your DB credentials.

---

### 2) Clone & Install

```bash
git clone <your-fork-or-repo-url> 

python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```
