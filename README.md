# inshorts-data-scientist-task
# Inshorts Data Scientist Task – Click Prediction & Recommendations

This repository contains my end-to-end solution for the Inshorts Data Scientist challenge. I approached the task using two strategies:

1. **Model-Based Recommendation** – Trained a LightGBM classifier to predict click probabilities from event logs, user behavior, and content features.  
2. **Rule-Based Fallback** – Leveraged device location data and global popularity signals to recommend top 50 articles.

### Highlights

- Full pipeline engineered on Google Colab (12GB RAM limit)
- Created balanced training data with positive (click) and negative samples
- Used `TimeSpent-Front` as a weak signal for positive engagement
- RAM-safe prediction generation using batched scoring for 10,400 users
- Rule-based fallback for cold-start users based on location

### Outputs

- `submission.csv`: Top-50 predicted content for each test user (model-based)
- `top50_rule_based.csv`: Rule-based backup using location + popularity

---

### Notes

Due to platform limitations, this solution was heavily optimized for memory. I kept the development process raw and real — the notebooks show the debugging journey and fallback strategies used to get the model trained reliably.

