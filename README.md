# inshorts-data-scientist-task
This repository contains the solution to the Inshorts Data Scientist Task, where we design and implement two distinct recommendation algorithms for news articles based on user behavior and content attributes.

---

## Project Structure
├── notebooks/
│ └── 04_modeling_and_inference.ipynb # Cleaned modeling & inference pipeline
├── user_features.csv # Engineered user-level features
├── content_features.csv # Engineered content-level features
├── training_data.csv # Labeled user-content pairs
├── test_candidates.csv # User-content pairs for inference
├── submission.csv # Final prediction file (top-50 per user)
├── top50_rule_based.csv # Rule-based recs (location + popularity)
├── model_lgbm.pkl # Serialized LightGBM model (optional)
└── README.md # This documentation


---

## Task Objective

Design and implement two news recommendation algorithms that leverage:

- User reading history  
- Expressed interests (category preferences)  
- Content popularity  
- User location relevance  

The algorithms must be real-time capable and suitable for production deployment.

---

## Data Overview

- **Devices**: User metadata (device ID, OS, location, language, timestamps)  
- **Event Logs**: User interactions (clicks, time spent) with content  
- **Training Content**: Content details for articles users interacted with  
- **Testing Content**: Inventory for future recommendations

---

## Solution Approach

### 1. Data Preparation & EDA
- Loaded CSVs into DataFrames and inspected schema and null rates.  
- Parsed timestamps (Unix epoch) for chronological features.  
- Explored distributions of event types, time spent, and user/device characteristics.

### 2. Feature Engineering
- **User Features**: total events, total time spent, unique content count, active days, first/last timestamps.  
- **Content Features**: view count, unique viewers, average time spent per view.  
- Saved feature tables as `user_features.csv` and `content_features.csv`.

### 3. Algorithm 1: Machine Learning Recommender
- **Model**: LightGBM binary classifier with early stopping.  
- **Training Data**: positive clicked pairs (label=1) vs. category-matched negatives (label=0).  
- **Validation**: Stratified split, achieved AUC = 0.9655.  
- **Inference**: Scored test candidates, exported `submission.csv` with top-50 per user.

### 4. Algorithm 2: Rule-Based Recommender
- **Logic**: For each user, recommend top-50 globally popular articles, filtered by user’s last known location when available.  
- **Output**: `top50_rule_based.csv` containing the ranked articles per user.

---

## How to Run

1. **Install dependencies**:  
   ```bash
   pip install pandas lightgbm scikit-learn
2. Execute notebook:
Open notebooks/04_modeling_and_inference.ipynb in Colab or Jupyter and run all cells.

3. Generate submission:
Ensure submission.csv and top50_rule_based.csv are present in the root.
Key Results
AUC (ML model): 0.9655

Coverage: Top-50 recommendations generated per user

Dual approaches: Balanced ML precision with a lightweight rule-based fallback
