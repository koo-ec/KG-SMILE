

# GraphRAG Explainability: Enhancing Transparency in Retrieval-Augmented Generation (RAG)


<img src="https://github.com/koo-ec/XGRAG/blob/main/docs/Figures/Explainability.png" alt="example">


## 📌 Overview

This repository presents an approach to improving the explainability of **GraphRAG**—a framework that integrates **Knowledge Graphs (KGs)** with **Retrieval-Augmented Generation (RAG)** to enhance AI-driven decision-making, particularly in high-stakes domains like **law** and **cybersecurity**.

The primary goal of this research is to assess how **perturbations** in knowledge graphs influence AI-generated responses and to quantify their impact using advanced **explainability metrics** such as **cosine similarity** and **inverse Wasserstein distance (inv\_WD)**.

---
## 🔍 Features

- **Graph-Based Retrieval:** Enhancing RAG with structured knowledge graphs.
- **Explainability Metrics:** Using **cosine similarity**, **Wasserstein distance**, **inverse Wasserstein distance (inv\_WD)**, and **hybrid metrics** to measure response fidelity.
- **Perturbation-Based Analysis:** Identifying influential nodes and edges in KGs by systematically altering graph structures.
- **Regression Modeling:** **Weighted linear regression** and **Bayesian Ridge Regression (BayLIME)** to evaluate graph components' significance.
- **Pre-Prompt Mechanism:** Reducing hallucinations, improving query responses through **rephrasing techniques**, and ensuring the system provides accurate answers even when direct retrieval fails.
- **Accuracy, Stability & Consistency Analysis:** Evaluating how minor modifications to the KG affect AI-generated explanations, ensuring that small changes do not significantly alter outputs while maintaining correctness and reliability in responses.
- **Graph Visualization:** Color-coded visualization to highlight impactful nodes and relationships.

---

## 💂 Data Extraction & Knowledge Graph Construction

**Constructing a knowledge graph** enhances RAG performance by structuring high-quality data. Knowledge graphs store structured, semi-structured, and unstructured information, mapping out **complex relationships** between entities to support improved AI decision-making.

### **Knowledge Graph Construction Process**

- **Data Source:** Structured cybersecurity-related knowledge was extracted from **DBpedia**.
- **Querying Mechanism:** Used **SPARQL**, a query language designed for retrieving and manipulating RDF (Resource Description Framework) data.
- **Implementation:**
  - Used `SPARQLWrapper` in Python to execute queries on DBpedia’s **public SPARQL endpoint**.
  - Focused on **software-related cybersecurity** concepts containing keywords like "cyber," "security," or "malware."
  - Extracted three key attributes per entity:
    1. **Entity Label** (human-readable name)
    2. **Abstract** (descriptive summary)
    3. **Classification** (software type)
  - Filtered for **English-language abstracts and labels**.
  - Structured extracted data into **subject-predicate-object** format.
- **Relations in the Knowledge Graph:**
  - **Type relation** linking each entity to the **Software** category.
  - **Label relation** providing a meaningful name.
  - **Abstract relation** storing textual descriptions.

This structured **KG** supports **downstream tasks**, including:

- **Question Answering**
- **Semantic Reasoning**
- **Explainability Analysis in Cybersecurity Applications**

The resulting **knowledge graph** serves as a **foundational dataset** for evaluating **stability** and **fidelity** in graph-based representations, which is **central to this research**.

---

## 📊 Evaluation Metrics

### **Fidelity Metrics**

- **Cosine Similarity:** Measures how similar the original and perturbed responses are by comparing vector representations.
- **Wasserstein Distance (WD):** Captures **distributional shifts** between original and perturbed outputs.
- **Inverse Wasserstein Distance (inv\_WD):** Highlights **opposite nodes** and emphasizes contrasting elements, improving interpretability.
- **Hybrid Metric (Cosine - WD - inv\_WD):** Balances **local alignment**, **global structure changes**, and **contrastive interpretability**.

### **Accuracy Metrics**

- **Ground Truth Comparison:** Evaluates AI-generated responses against **human-verified correct answers**.
- **Precision & Recall:** Measures correctness and retrieval efficiency.
- **F1 Score:** Provides a balanced accuracy assessment.
- **Mean Absolute Error (MAE):** Quantifies the average deviation from expected results.

### **Stability Analysis**

- **Jaccard Similarity Index:** Evaluates response consistency under minor KG perturbations.
- **Temperature Control (T=0 vs. T=1):** Analyzes **deterministic vs. stochastic retrieval** effects.

### **Consistency Metrics**

- **Box Plot Analysis:** Measures response variation across different KG segments.
- **Statistical Regression Models:** **Bayesian Ridge** and **Weighted Linear Regression** for explanation uniformity.

### **Explainability Through Perturbation**

- **Graph Component Analysis:** Identifies nodes/edges influencing AI-generated responses.
- **Visualization:** **Color-coded KG representation** highlighting influential components.

### **Chain-of-Thought (CoT) Reasoning**

- **Multi-Step Logical Deductions:** Ensures structured, explainable decision-making by breaking down queries into intermediate steps.
- **Interpretability Enhancement:** Reduces AI hallucinations and improves response coherence in high-stakes domains.

### **Pre-Prompting for Query Refinement**

- **Rephrased Queries:** Enhances retrieval accuracy by generating multiple query variants.
- **Filtering Mechanism:** Eliminates uncertain responses ("I don’t know").
- **Embedding-Based Aggregation:** Synthesizes multiple responses for improved robustness.

---

## 🗂 Repository Structure

```
GraphRAG-Explainability
│── README.md               # Project documentation
│── requirements.txt        # Dependencies
│── GraphRAG_Explainability.ipynb  # Jupyter Notebook with code & experiments
│── data                    # Sample datasets and knowledge graphs
│   ├── cybersecurity_kg.txt # Extracted cybersecurity-related knowledge graph
│   ├── queries              # SPARQL queries used for data extraction
│   ├── triples              # Structured subject-predicate-object relations
│   ├── raw_data             # Original unprocessed DBpedia extractions
│── results                  # Output visualizations and analysis reports
```

---

## ⚙️ Installation & Usage

### **Install Dependencies**

```bash
pip install langchain openai networkx numpy pandas sklearn scipy matplotlib seaborn SPARQLWrapper
```

### **Run Jupyter Notebooks**

You can open and execute notebooks in **Google Colab** using these links:

- **[Consistency Notebook](https://colab.research.google.com/drive/1OAENL5jSKZemoc79fA5u2PV8pBC8xLUI)**
- **[COT- PrePrompt Notebook](https://colab.research.google.com/drive/1tuNUdAoKdnSMOIw63mxriQvJdGjtpz-k#scrollTo=TQwaa-8771BB)**
- **[Fidelity - Number Of Perturbation Notebook](https://colab.research.google.com/drive/10TbC29CrBmpnSUpNr_6vnzpst0nnRAKL)**
- **[Stability Notebook](https://colab.research.google.com/drive/1AP36M9hljghB8CtlhLs7D2bOn3-YwzEK)**
- **[Time Complexity Notebook](https://colab.research.google.com/drive/1Eqj4-hT7pgbwqFmtDk7hHDn6k13gzx_W)**

Alternatively, run locally:

```bash
jupyter notebook <notebook_name>.ipynb
```

---

## 🔬 Future Directions

- **Exploring Advanced Similarity Measures: Evaluating KL Divergence alongside cosine similarity and inverse Wasserstein distance for better response ranking.**
- **Weighted Response Aggregation: Prioritizing responses based on semantic similarity, source credibility, and frequency to improve accuracy.**
- **Graph-Based Cache-Augmented Generation (CAG): Enhancing retrieval efficiency by storing and updating knowledge dynamically within a structured graph.**
- **Establishing a Benchmark for GraphRAG Explainability: Defining evaluation metrics and performance baselines for explainability in GraphRAG.**

---

## 🤝 Contributions

We welcome contributions! Open an **issue** for feature requests or submit a **pull request**.

---

## 🌟 Acknowledgments

Special thanks to **Professor Dhaval Thakker**, **DR** **Koroosh aslansefat**, and the **Responsible AI Research Group** at **University of Hull**.


