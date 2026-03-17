# AI-Powered-Supply-Chain-Risk-Intelligence-System
### *Phase 1: 14 Days* – Databricks AI Challenge-2 (Advanced) &amp; *Phase 2*: AI-Powered Supply Chain Risk Intelligence System Project in Supply Chain &amp; Operations domain.
![204](https://github.com/user-attachments/assets/ac758d17-43b6-4fcc-834e-0940303467f3)


----
## Problem Definition & AI Framing:
The objective of this project is to predict whether a shipment will be delayed or not, making it a binary classification problem. The system takes structured shipment data as input and produces a delay risk prediction as output.
In modern supply chain operations, shipment delays are a major challenge that directly impact customer satisfaction, operational efficiency, and overall business cost. Delays can occur due to multiple interacting factors such as shipment mode, warehouse efficiency, product characteristics, and external conditions like weather.

Traditional rule-based systems are not sufficient here because:
They cannot capture complex interactions between variables.
They fail to adapt to changing patterns.
They lack scalability and predictive capability.
This is why a machine learning approach is used.

The success criteria for this system include:
Achieving a reliable prediction performance. (AUC ~0.74 achieved)
Generating actionable insights for business users.
Identifying high-risk shipments proactively.

This problem is highly relevant in real-world logistics and operations, making it a practical and impactful AI use case.


### Why AI (Not Rules)?    Because:
- Mental health risk is influenced by multiple interacting factors.
- Simple thresholds (like “screen time > 6 hrs.”) miss complex relationships
- ML can learn nonlinear patterns between sleep, usage time, content type, and psychometric scores.

----

## Data Understanding & Feature Engineering:
### Data Understanding:
The dataset represents 8,000 social media users with detailed digital behavior and mental health indicators.
Each record combines:
- Demographics (Age, Gender)
- Usage behavior (screen time, activity type, late-night usage)
- Psychometric scores (GAD-7 for anxiety, PHQ-9 for depression)
The data is synthetic but scientifically grounded, generated using psychological research patterns.
Designed specifically for gender-based comparative analysis and behavioral risk modeling.

### Key observations from raw data:
- Mental health impact is behavior-driven, not caused by a single variable.
- Late-night usage and reduced sleep appear frequently with higher depression scores.
- Passive content consumption and social comparison are common anxiety triggers.

----

## Feature Engineering (Silver Layer) : 
Cleaned raw data by: Removing duplicates and handling missing values in critical numerical fields.
Created behavioral risk features to translate raw usage into meaningful signals:
Engineered Features:
- High_Screen_Time: Flagged users spending more than 6 hours daily on screens.
- Sleep_Deprived: Identified users sleeping less than 6 hours.
- LateNight_Sleep_Risk: Combined late-night activity with sleep deprivation.
- Passive_Usage_Risk: Captured risk from passive scrolling behavior.
- Social_Comparison_Risk: Represented exposure to comparison-driven content.
- High_Mental_Health_Risk (Target): Flagged users with moderate-to-severe anxiety or depression scores.
These features converted raw digital behavior into interpretable mental health risk signals.

----

## AI Innovation & Insight Generation:
### What makes this project “AI” and not just SQL?
- Instead of only reporting mental health statistics, I designed behavioral risk signals from raw social media usage data.
- I transformed daily habits (screen time, sleep, late-night usage, activity type) into risk indicators.
These features helped uncover hidden behavioral patterns, not obvious from raw data alone.

### Key AI-driven insights generated:
- High screen time + sleep deprivation strongly correlates with higher anxiety and depression scores.
- Late-night social media usage amplifies mental health risk.
- Passive consumption and social comparison increase anxiety levels.
- Gender-based risk distribution highlights different behavioral impacts.

Innovation here is feature engineering + insight generation from behavior, not just prediction.

----

## Training, Evaluation & Metrics:
### How I validated the model?
Model training and experiments were tracked using Mlflow and I logged key evaluation metrics:
- Accuracy –Mental health predictions require balanced evaluation.
- AUC –AUC helps avoid misleading accuracy in imbalanced datasets.
- Confusion Matrix – false positives vs false negatives- supports explainability and trust.

### Outcome:
- Model achieved stable performance.
- Predictions stored in a Gold prediction table.
- Metrics and model version fully reproducible via Mlflow.

----

## Database ↔ AI Workflow (Lakehouse Integration):
Data flows through:
- Bronze → Raw ingestion (Delta).
- Silver → Cleaned & feature-engineered data.
- Gold → Analytics tables & ML-ready datasets.
AI integration: ML model reads directly from Gold Delta tables.
Predictions written back to Gold prediction table.
Same data serves: SQL Analytics | Dashboards | ML training | Model inference.

This avoids data duplication and ensures single source of truth.

----

## Business Impact & Practical Use:
### Why this project matters in the real world?
- Enables early detection of mental health risk based on behavior and helps platforms:
- Identify high-risk users proactively.
- Design targeted well-being interventions.
- Monitor impact of platform usage patterns.

### Practical applications:
- Mental health monitoring dashboards.
- Risk-based user segmentation.
- Responsible AI use in social platforms.

### Scalable & production-ready:
- Automated jobs.
- Governed data access via Unity Catalog.
- ML lifecycle managed with Mlflow.

