# Jupiter FAQ Bot

An intelligent, conversational FAQ bot for the [Jupiter Help Centre](https://jupiter.money), designed to answer user queries by retrieving and rephrasing FAQ content in a friendly tone.

---

## 🚀 Project Overview

**Objective:**  
Build a human-friendly chatbot that responds to Jupiter users’ frequently asked questions using semantic search and large language models.

---

## 🛠️ Methodology and Architecture

### 1️⃣ Data Collection
- **Scraping:** Collected FAQ content by crawling internal links from the Jupiter website.
- **Filtering:** Selected pages containing FAQ sections (`<h1>` with "Frequently Asked Questions").
- **Extraction:** Pulled Q&A pairs using:
  - `div.faq-header` and `div.faq-answer`
  - `h3` headings and following `<p>` tags as fallback.

### 2️⃣ Preprocessing and Cleaning
- Removed HTML tags and excessive whitespace.
- Deduplicated questions using:
  - TF-IDF vectorization
  - Cosine similarity threshold of 0.9.

### 3️⃣ Semantic Retrieval Pipeline
- Embedded questions using **SentenceTransformers** (`all-MiniLM-L6-v2`).
- Indexed embeddings with **FAISS** for fast similarity search.
- Retrieved the top match for each user query.

### 4️⃣ LLM-based Answer Generation
- Rephrased retrieved answers in a conversational style using **Mistral-7B-Instruct-v0.2**.
- **Prompt Template:**
