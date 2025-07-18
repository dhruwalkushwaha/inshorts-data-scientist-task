# news-recommendation-systems

This repository presents a complete solution to a real-world recommendation task. It includes the design, development, and evaluation of two scalable recommendation algorithms for news articles:

1. A model-based approach using LightGBM.
2. A rule-based fallback system leveraging content popularity and user location.

---

## Project Structure

```
├── notebooks/
│ └── 04_modeling_and_inference.ipynb # Cleaned notebook: full modeling + inference pipeline
├── user_features.csv # Engineered user-level features
├── content_features.csv # Engineered content-level features
├── submission.csv # Top-50 LightGBM-based recommendations (https://drive.google.com/file/d/1izRLz3Wof6aMPYB0IzMZNjoFAVLqmFjC/view?usp=sharing)
├── top50_rule_based.csv # Top-50 fallback recommendations (location + popularity) (https://drive.google.com/file/d/1YR8Xr5OL979XZAfT6CtQJ644AxnzBGNl/view?usp=sharing)
├── training_data.csv # Labeled click / non-click pairs for training
├── test_candidates.csv # Candidate user-content pairs for final prediction
├── LICENSE
├── README.md # Project documentation

> Note: Due to GitHub size limits, the CSV files exceeding 25MB have been provided via [Google Drive](https://drive.google.com) links inside the notebook.

---
```
## Task Objective

Build two recommendation systems for a news app to recommend relevant articles based on user behavior, content metadata, and popularity:

- Leverage past reading history
- Account for user interest categories
- Consider article popularity
- Incorporate location relevance

---

## Data Sources

- **Devices**: Metadata for each user (ID, OS, language, location, etc.)
- **Event Logs**: Interaction records (e.g., click, time spent, search, bookmark)
- **Training Content**: Metadata about previously viewed news articles
- **Testing Content**: Articles to recommend from
- **Test Devices**: Unseen users requiring fresh recommendations

---

## Solution Overview

### Step 1: Data Preparation
- Loaded and inspected millions of rows across device, content, and event logs
- Unified schemas, parsed Unix timestamps, and dropped irrelevant/low-signal events

### Step 2: Feature Engineering
- **User-Level**: Click frequency, total time spent, active days, session patterns
- **Content-Level**: View count, unique viewers, average session time
- Saved to `user_features.csv` and `content_features.csv`

### Step 3: Model-Based Recommendations
- Used **LightGBM** classifier to predict relevance scores between users and content
- Generated labeled pairs with:
  - Positive = user clicked the article
  - Negative = category-matched article not clicked
- Validation AUC: **0.9653**
- Final output: `submission.csv` with top-50 predictions per user

### Step 4: Rule-Based Recommendations
- For users missing model scores or as a fallback:
  - Rank top 500 globally popular articles
  - Filter and sort using the user’s last known location (if available)
- Output: `top50_rule_based.csv`

---

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/dhruwalkushwaha/news-recommendation-systems.git
   cd news-recommendation-systems

2. Open the final notebook
Open notebooks/04_modeling_and_inference.ipynb in Google Colab or Jupyter.

3. Run all sections

4. Load data

5. Feature engineering

6. Train the LightGBM model

7. Score test data

8. Generate submission.csv and top50_rule_based.csv
```
Review Output

submission.csv: Top-50 articles per user (model)

top50_rule_based.csv: Top-50 articles per user (fallback)

Results Summary
Metric	Value
LightGBM AUC Score	0.9653
Rule-Based Coverage	100%
Fallback Logic	Location + Global Popularity
```
Notes

• The entire pipeline was executed on Google Colab (Free Tier, 12.67 GB RAM).

• RAM-safe operations and batching were used to prevent crashes on large files.

• No proprietary APIs or external paid tools were used.

• This project reflects a realistic, production-minded recommendation workflow.
```
License
MIT License © 2025 Dhruwal Kushwaha
