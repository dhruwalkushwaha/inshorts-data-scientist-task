# inshorts-data-scientist-task

This repository contains the solution to the Inshorts Data Scientist Task, where we build and evaluate two robust recommendation systems for news articles: a machine learning model and a rule-based approach using user behavior and content popularity.

---

##  Project Structure
├── notebooks/
│ └── 04_modeling_and_inference.ipynb # Full modeling pipeline (cleaned)
├── user_features.csv # Engineered user-level features
├── content_features.csv # Engineered content-level features
├── submission.csv # Top-50 ML-based recommendations
├── top50_rule_based.csv # Top-50 rule-based fallback recommendations
├── training_data.csv # Generated click/non-click labeled pairs
├── test_candidates.csv # User-content pairs for scoring
├── README.md # This file

---

##  Task Objective

Design and implement two recommendation algorithms that leverage:

- User reading behavior
- Expressed content interest
- Article popularity trends
- User's geographic location

---

##  Data Sources

- Devices: Metadata for each user (ID, OS, timestamps, geo-location).
- Events: Logs of user interactions like `TimeSpent`, `Bookmark`, `Search`, etc.
- Content: Metadata for news articles (title, category, hashtags).
- Test Users & Articles: New devices and content pool for inference.

---

##  Solution Approach

### Step 1: Data Prep & Exploration
- Parsed millions of event records and timestamps.
- Focused on `TimeSpent-Front` as the proxy for meaningful user interest.
- Handled missing values, unified column naming, and validated schema.

### Step 2: Feature Engineering
- User-Level: Total time spent, click counts, session span, content diversity.
- *Content-Level: Total views, unique viewers, avg time per article.
- Saved as `user_features.csv` and `content_features.csv`.

### Step 3: Model-Based Recommendations (LightGBM)
- Constructed binary-labeled training data (clicked = 1, sampled non-clicks = 0).
- Used stratified train/validation split.
- Trained LightGBM with early stopping (AUC = 0.9653).
- Predicted relevance scores for test candidates.
- Output: `submission.csv` with top-50 predictions/user.

### Step 4: Rule-Based Recommender
- For users with missing model predictions or as a fallback:
  - Recommend globally popular articles.
  - Prioritize based on user location if available.
- Output: `top50_rule_based.csv`.

---

## 🛠 How to Run (Colab-Friendly)

1. Clone this repo & navigate:
In bash:
git clone https://github.com/dhruwalkushwaha/inshorts-data-scientist-task.git
cd inshorts-data-scientist-task
Open the final notebook in Colab:
notebooks/04_modeling_and_inference.ipynb

Run all cells in order, including:

a. Data loading & cleaning

b. Feature engineering

c. Training & prediction

d. Generating both CSV outputs

Check outputs:

submission.csv → ML model top-50/user

top50_rule_based.csv → Rule-based fallback top-50/user

Results
Metric	Value
ML Model AUC Score	0.9653
Rule-Based Backup	Enabled (Location + Popularity)
Coverage: 50 articles per user (guaranteed)

Notes
a. All training and inference were conducted in Google Colab (Free Tier, 12.67 GB RAM).

b. The pipeline was optimized for memory efficiency via batch processing and minimal joins.

c. You may retain the raw notebook state to reflect debugging and realistic dev iterations.

Branch Info

You're on the setup-colab branch, optimized for Colab. The main branch contains the initial skeleton.
