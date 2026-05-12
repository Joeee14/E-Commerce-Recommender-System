<div align="center">
  <h1>🌟 Intelligent Recommender System</h1>
  <p><strong>AIE425 – Alamein International University</strong></p>
  <p><i>A full-stack, from-scratch product recommender system featuring 8 distinct algorithms, real-time explanations, and a sleek web dashboard.</i></p>

  ![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
  ![Flask](https://img.shields.io/badge/Flask-Web%20App-lightgrey?style=for-the-badge&logo=flask&logoColor=black)
  ![NumPy](https://img.shields.io/badge/NumPy-Math%20Core-013243?style=for-the-badge&logo=numpy&logoColor=white)
  ![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
</div>

<br />

## ✨ Key Features

- 🧠 **8 Recommender Algorithms**: Spanning Collaborative, Content-Based, and Knowledge-Based paradigms.
- 🧮 **Built From Scratch**: Core math and optimizations implemented manually using NumPy—no black-box recommender libraries!
- 💬 **Explainable AI**: Every recommendation includes a plain-English explanation of *why* it was chosen.
- 📊 **Evaluation Dashboard**: Compare methods side-by-side on RMSE, Precision@5, Recall@5, Coverage, and Diversity.
- 🛍️ **Interactive Web Portal**: A Flask-powered UI to browse products, view history, and get real-time recommendations.

---

## 🛠️ Recommendation Methods

### 🤝 Collaborative Filtering (CF)
| Method | Key Idea |
| :--- | :--- |
| **User-Based Pearson** | Finds neighbours via Pearson correlation; predicts ratings using mean-adjusted weighted average. |
| **User-Based Jaccard** | Treats interactions as binary sets; scores by `J(A,B) = |A∩B| / |A∪B|`. |
| **Item-Based Adj. Cosine**| Pre-subtracts user means before cosine similarity; predicts via similarity-weighted ratings. |
| **MF Gradient Descent** | Decomposes the user-item matrix into latent factors `P` and `Q` via manual SGD. |

### 📄 Content-Based Filtering (CB)
| Method | Key Idea |
| :--- | :--- |
| **TF-IDF + Cosine** | Builds TF-IDF vectors from product text; ranks by cosine similarity to user history. |
| **Feature Vector** | One-hot encodes category/brand, normalises price/rating; ranks by cosine similarity. |

### 💡 Knowledge-Based Filtering (KB)
| Method | Key Idea |
| :--- | :--- |
| **Constraint-Based** | Filters by budget, preferred categories, min rating; ranks survivors by overall rating. |
| **Case-Based Reasoning** | Scores products against a reference item on category (40%), brand (20%), price (20%), and rating (20%). |

---

## 📂 Project Structure

```bash
project/
├── 📁 data/                  # 📊 Products, users, ratings, and purchases CSVs
├── 📁 recommenders/          # 🧠 Core logic (CF, CB, KB implementations)
├── 📁 explainers/            # 💬 Natural-language explanation generator
├── 📁 evaluation/            # 📈 Metrics (RMSE, Precision, Recall, etc.)
├── 📁 utils/                 # ⚙️ Data loaders and train/test splitting
└── 📁 web/                   # 🌐 Flask server, templates, and static assets
```

<details>
<summary><b>Show Detailed Structure</b></summary>

```bash
project/
├── data/
│   ├── products.csv          # 117 products (name, category, brand, price, rating, tags)
│   ├── users.csv             # 50 users (profile, budget, preferred categories)
│   ├── ratings.csv           # 1,191 user-product ratings (1–5 scale)
│   └── purchases.csv         # 803 purchase records
├── recommenders/
│   ├── collaborative.py      # CF: Pearson, Jaccard, Adj-Cosine, MF-SGD
│   ├── content_based.py      # CB: TF-IDF, Feature Vector
│   └── knowledge_based.py    # KB: Constraint, CBR
├── explainers/
│   └── explain.py            # Natural-language explanation generator
├── evaluation/
│   └── metrics.py            # RMSE, Precision@K, Recall@K, Coverage, Diversity
├── utils/
│   └── data_loader.py        # DataStore class + 80/20 train-test split
└── web/
    ├── server.py             # Flask routes and API endpoints
    ├── static/
    │   ├── css/style.css
    │   └── js/main.js
    └── templates/
        ├── base.html
        ├── index.html
        ├── recommendations.html
        ├── product.html
        └── analysis.html
```
</details>

---

## 🚀 Quick Start

### Requirements
- **Python:** 3.8+

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/aie425-recommender.git
   cd aie425-recommender
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Launch the web application**
   ```bash
   python web/server.py
   ```
   *Then open `http://localhost:5000` in your browser.*

---

## 🔬 Evaluation Metrics

<div align="center">

| Metric | Applies to | Description |
| :---: | :---: | :--- |
| **RMSE** | CF only | How accurately the model predicts held-out ratings. *Lower = better*. |
| **Precision@5** | All | Fraction of top-5 recommendations that are truly relevant (rating ≥ 4). |
| **Recall@5** | All | Fraction of all relevant items that appear in the top-5. |
| **Coverage** | All | % of the product catalogue recommended at least once across all users. |
| **Diversity** | All | Average pairwise cosine distance between recommended TF-IDF vectors. |

</div>

> ℹ️ **Note on Data Splitting:** The train/test split is 80/20 per user, ordered by timestamp. The most recent 20% of each user's ratings form the held-out test set.

---

## 📝 Implementation Details

- **No Black Boxes:** All similarity and factorisation algorithms are implemented **from scratch** using only NumPy and basic Python.
- **Optimised Execution:** The item-based cosine similarity matrix is pre-computed with vectorised NumPy operations for efficient batch evaluation.
- **Efficient MF-SGD:** Trains once per evaluation run using a batch helper that scores all users from a single `P`/`Q` decomposition.
- **Real-Time Explanations:** Explanations are generated dynamically server-side and returned alongside every API response.

<hr>
<p align="center">
  <i>Developed for the AIE425 – Intelligent Recommender Systems course at Alamein International University.</i>
</p>
