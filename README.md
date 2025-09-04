# Applied Data Science - Supreme Court Legal Decisions Project (2025)

This repository contains the semester project for the course **Applied Data Science (2025)**. The project focuses on extracting, analyzing, and modeling Greek Supreme Court decisions.

## Project Overview

The project is divided into two main parts:

### Part A - Data Collection and Exploration

- **Objective**: Build a structured dataset from legal decisions published on the Supreme Court website.
- **Approach**:
  - Studied the website structure to define dataset specifications.
  - Developed a **Python web crawler** using `selenium` and `BeautifulSoup` to collect decisions.
  - Used `regex` for extracting structured information.
  - Visualized basic statistics and distributions of the dataset.
- **Dataset Fields**:
  - `decision_number` (string) – Number of the decision
  - `year` (int) – Year of the decision
  - `department_type` (string) – Department type
  - `department_number` (string) – Department number
  - `judges` (list of strings) – Judges involved
  - `introduction_text` (string)
  - `main_text` (string)
  - `conclusion_text` (string)
  - `penal_code` (set of strings) – Articles of Penal Code
  - `code_of_criminal_procedure` (set of strings)
  - `civil_code` (set of strings)
  - `code_of_civil_procedure` (set of strings)
  - `decision_link` (string) – URL to the decision
- **Results**: Collected **2475 decisions**; most fields were extracted successfully, while some legal references had inconsistencies due to heterogeneous text structures.

### Part B - Legal Document Analysis

#### B1. Supervised Learning for Document Classification
- Models implemented: **SVM**, **Logistic Regression**, **Random Forest**
- Labels: `volume`, `chapter`, `subject`
- Preprocessing: TF-IDF and Bag-of-Words
- Observations:
  - Performance decreases as the number of classes increases (volume → chapter → subject)
  - Some categories with few samples resulted in low metrics for precision, recall, and F1-score.

#### B2. Topic Modeling and LLM Summarization
- **Exploratory Data Analysis**: Identified 315 unique categories; distribution is imbalanced.
- **K-Means Clustering**:
  - TF-IDF + SVD for dimensionality reduction (500 features)
  - Tested K = 2–20 clusters; best K = 19 (full text) and K = 20 (summaries)
- **LLM-based Topic Extraction**:
  - Selected 3 decisions per cluster (closest to centroid or random)
  - Used **LLM (llama-4-maverick:free)** to generate cluster titles
  - Centroid-based selection yielded more accurate and concise titles

## Tools and Libraries

- Python 3.x
- Selenium, BeautifulSoup, re
- Scikit-learn, Pandas, NumPy
- LLM API: OpenRouter (llama-4-maverick:free)
