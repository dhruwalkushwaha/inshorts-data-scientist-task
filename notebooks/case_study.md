# Case Study: News Recommendation Systems
## Overview
This project demonstrates the development of a scalable, two-stage news recommendation system. The system integrates user interaction data, content metadata, and device-level location information to provide personalized article recommendations.
```

Problem Statement
Develop a recommendation system capable of suggesting relevant news articles to users by analyzing:

User engagement behavior

Content preferences (categories, hashtags)

Article popularity and reading trends

User location data (sub-admin regions)

The solution should be production-ready, RAM-efficient, and designed to work within constraints such as limited system memory.
```

###  Data Sources
#### Dataset	Description

Event Logs	Over 3.5 million rows of user interactions (time spent, bookmarks, search actions)
Devices	Device ID, operating system, and location metadata
##### Training Content	
  Article metadata including title, hashtags, and category
##### Testing Content	
  New articles available for recommendation
##### Test Devices	
  New users to recommend articles to
```
```
#### Approach Summary
1. Data Cleaning and Exploration
  • Parsed and validated timestamps from raw interaction logs

  • Filtered TimeSpent-Front events as signals of active engagement

  • Ensured consistency of column naming and schema structure across datasets
```
```
2. Feature Engineering
  • User-level features: total time spent, number of events, diversity of content, session spans

  • Content-level features: total views, unique viewers, average time spent per article

  • Finalized and stored as user_features.csv and content_features.csv
```

```
3. Model-Based Recommendations (LightGBM)
  • Binary classification model trained on positive (clicked) and negative (sampled) user-content pairs

  • Applied stratified validation splits

  • Achieved AUC of 0.9653 on validation set

  • Inference performed in RAM-safe batches of 250 users at a time
```


```
4. Rule-Based Fallback System
For users with no model predictions or cold-start scenarios

Recommended top-viewed global articles, filtered by the user's last known location

Produced a complete backup submission with 50 recommendations per user
```
```
### Results

  Metric	Value
  Validation AUC (ML Model)     	  0.9653

  Top-K Coverage	                 50 per user

  Rule-Based Support	             Location + Popularity

  Environment	Google Colab (Free Tier, 12.67 GB RAM)

#### Engineering Highlights
• Efficient memory handling using batch operations

• Separate feature engineering and modeling pipelines

• Cleaned modeling notebook includes debug states for transparency

• Optimized merge strategies and joins to avoid crashes during runtime

Output files: submission.csv (ML-based) and top50_rule_based.csv (rule-based fallback)


##### Key Learnings
• Negative sampling within the same content category improves classifier quality

• Rule-based recommenders remain valuable in production environments with unknown or new users

• Resource limitations can be addressed with careful pipeline design

• Even assessment tasks that do not lead to selection can be productized and reused as portfolio assets

```
Repository
github.com/dhruwalkushwaha/news-recommendation-systems
