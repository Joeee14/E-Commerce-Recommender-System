# AIE425 – Intelligent Recommender System

A full-stack product recommender system built from scratch for the AIE425 course at Alamein International University. The system implements eight recommendation algorithms across three paradigms, exposes them through a Flask web application, and evaluates them with five standard metrics.

---

## Features

- **8 recommendation algorithms** across three paradigms — all core math implemented manually (no recommender libraries)
- **Explainability layer** — every recommendation comes with a plain-English reason
- **Evaluation dashboard** — compare all methods side-by-side on RMSE, Precision@5, Recall@5, Coverage, and Diversity
- **User purchase & rating history** — see what drove each recommendation
- **Product catalogue** — search, filter by category, sort by price or rating

---

## Recommendation Methods

### Collaborative Filtering (CF)
| Method | Key Idea |
|---|---|
| User-Based Pearson | Finds neighbours via Pearson correlation; predicts ratings using mean-adjusted weighted average |
| User-Based Jaccard | Treats interactions as binary sets; scores by J(A,B) = \|A∩B\| / \|A∪B\| |
| Item-Based Adj. Cosine | Pre-subtracts user means before cosine similarity; predicts via similarity-weighted ratings |
| MF Gradient Descent | Decomposes the user-item matrix into latent factors P, Q via manual SGD |

### Content-Based Filtering (CB)
| Method | Key Idea |
|---|---|
| TF-IDF + Cosine | Builds TF-IDF vectors from product text; ranks by cosine similarity to user history |
| Feature Vector | One-hot encodes category/brand, normalises price/rating; ranks by cosine similarity |

### Knowledge-Based Filtering (KB)
| Method | Key Idea |
|---|---|
| Constraint-Based | Filters by budget, preferred categories, min rating; ranks survivors by overall rating |
| Case-Based Reasoning | Scores all products against a reference item on category (40%), brand (20%), price (20%), rating (20%) |

---

## Project Structure

```
project/
├── data/
│   ├── products.csv          # 117 products (name, category, brand, price, rating, tags)
│   ├── users.csv             # 50 users (profile, budget, preferred categories)
│   ├── ratings.csv           # 1 191 user-product ratings (1–5 scale)
│   └── purchases.csv         # 803 purchase records
│
├── recommenders/
│   ├── collaborative.py      # CF: Pearson, Jaccard, Adj-Cosine, MF-SGD
│   ├── content_based.py      # CB: TF-IDF, Feature Vector
│   └── knowledge_based.py   # KB: Constraint, CBR
│
├── explainers/
│   └── explain.py            # Natural-language explanation generator
│
├── evaluation/
│   └── metrics.py            # RMSE, Precision@K, Recall@K, Coverage, Diversity
│
├── utils/
│   └── data_loader.py        # DataStore class + 80/20 train-test split
│
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

---

## Setup

**Requirements:** Python 3.8+

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/aie425-recommender.git
cd aie425-recommender

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the web app
python web/server.py
```

Then open `http://localhost:5000` in your browser.

---

## Evaluation Metrics

| Metric | Applies to | Description |
|---|---|---|
| RMSE | CF only | How accurately the model predicts held-out ratings. Lower = better. |
| Precision@5 | All | Fraction of top-5 recommendations that are truly relevant (rating ≥ 4). |
| Recall@5 | All | Fraction of all relevant items that appear in the top-5. |
| Coverage | All | % of the product catalogue recommended at least once across all users. |
| Diversity | All | Average pairwise cosine distance between recommended TF-IDF vectors. |

> The train/test split is 80/20 per user, ordered by timestamp, so the most recent 20% of each user's ratings form the held-out test set.

---

## Implementation Notes

- All similarity and factorisation algorithms are implemented **from scratch** using only NumPy and basic Python — no recommender-system libraries (Surprise, LightFM, etc.) are used.
- The item-based cosine similarity matrix is pre-computed with vectorised NumPy operations for efficient batch evaluation.
- MF-SGD trains once per evaluation run (not once per user) using a batch helper that scores all users from a single P/Q decomposition.
- Explanations are generated server-side and returned with every recommendation API response.

---

## Course

**AIE425 – Intelligent Recommender Systems**  
Alamein International University
