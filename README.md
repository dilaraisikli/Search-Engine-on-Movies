# $$\text{MOVIE SEARCH ENGINE PROJECT}$$

This repository contains the complete workflow for building a **search engine over 30,000 movies**, collected and processed from raw Wikipedia pages.  
The system allows users to search movies by **genre, topics, keywords, dates, descriptions**, or any query they want.

---

# $$\text{1. DATA COLLECTION — collector.py}$$

**Goal:** Build our own dataset from 30,000 Wikipedia URLs.

**Process:**
- A list of **30,000 movie Wikipedia links** is provided.
- `collector.py`:
  - Downloads each HTML page.
  - Stores every file inside the **Movies/** directory.
- This creates a complete raw dataset of HTML movie descriptions.

---

# $$\text{2. DATA PARSING — parser.py}$$

**Goal:** Convert raw HTML files into structured TSV files.

**Steps:**
- Extract key information from each HTML page:
  - **Title**
  - **Introduction**
  - **Plot**
  - **Info-box details**
  - **Movie URL**
- Each parsed file is saved inside **MoviesTSV/**.
- Final output: **one clean TSV file per movie**, ready for indexing.

---

# $$\text{3. UTILITY FUNCTIONS — utils.py}$$

This module contains helper functions used across the project.

### **Data Processing — preprocess()**
This function prepares text for indexing through three steps:

1. **Normalize text**
   - Convert to lowercase  
   - Remove punctuation  

2. **Remove stopwords**
   - Uses a predefined English stopword list  

3. **Stemming**
   - Reduces words to their base forms  

### **TF-IDF Computation — computeTfidf()**
- Computes:
  - **Term Frequency (TF)**
  - **Inverse Document Frequency (IDF)**
- Builds vector weights using:
  ```
  tfidf(t, d) = tf(t, d) × idf(t)
  ```

---

# $$\text{4. INDEXING — index.py}$$

**Goal:** Create the dictionaries needed for fast retrieval.

This script builds and saves the following:

### **Core Dictionaries**
- **Vocabulary**  
  List of all stemmed terms appearing in the corpus.

- **IndexDict**  
  Posting lists mapping:
  ```
  term → {document_id : term_frequency}
  ```

- **tfIdfIndexDict**  
  Mapping:
  ```
  term → {document_id : tfidf_weight}
  ```

### **Extra Dictionaries for Question 3**
Additional structures built for extended features such as advanced ranking or filtering.

---

# $$\text{5. SEARCH ENGINES — main.py}$$

Implements **three different search engines**, increasing in complexity and accuracy.

### **Search Engine 1 — Boolean / Keyword Match**
- Simple keyword lookup  
- Returns all movies containing the query terms  

### **Search Engine 2 — TF-IDF Based Ranking**
- Computes similarity using TF-IDF scores  
- Ranks documents based on weighted relevance  

### **Search Engine 3 — Euclidean Distance Search**
- Represents each movie as a TF-IDF vector  
- Computes Euclidean distance between query vector and movie vectors  
- Returns the closest movies by semantic meaning  

This final engine produces **the most accurate and meaningful results**.

---

# $$\text{6. BONUS SCRIPT — exercise\_4.py}$$

This script solves a separate algorithmic challenge:

### **Longest Palindromic Substring**
- Uses **dynamic programming**
- Computes the length of the longest palindromic substring in a given input string

---

# $$\text{SUMMARY}$$

This project demonstrates the complete pipeline for building a **custom movie search engine**:

- Data collection  
- Data parsing  
- Text preprocessing  
- Index construction  
- Multiple search methodologies  
- Efficient vector-based retrieval over a large dataset  

Everything is modular, extendable, and easy to run.
