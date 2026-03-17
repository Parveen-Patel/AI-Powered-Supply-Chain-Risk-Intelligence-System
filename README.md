# AI-Powered-Supply-Chain-Risk-Intelligence-System
### *Phase 1: 14 Days* – Databricks AI Challenge-2 (Advanced) &amp; *Phase 2*: AI-Powered Supply Chain Risk Intelligence System Project in Supply Chain &amp; Operations domain.
![204](https://github.com/user-attachments/assets/ac758d17-43b6-4fcc-834e-0940303467f3)


----
## Problem Definition & AI Framing:
In modern supply chain operations, shipment delays are a major challenge that directly impact customer satisfaction, operational efficiency, and overall business cost. Delays can occur due to multiple interacting factors such as shipment mode, warehouse efficiency, product characteristics, and external conditions like weather.
The objective of this project is to predict whether a shipment will be delayed or not, making it a binary classification problem. The system takes structured shipment data as input and produces a delay risk prediction as output.

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

----

### Dataset Overview:
The primary dataset is an E-commerce Shipping Dataset consisting of 10,999 records and 12 variables. It contains detailed shipment-level information including customer behavior, product characteristics, and logistics details.
The key target variable is whether the shipment was delivered on time or delayed, making it suitable for a classification problem.
To enhance the analytical depth, a second dataset - Historical Weather Data was incorporated. This dataset includes hourly weather observations such as temperature, humidity, and pressure across multiple cities over several years.
The goal of combining these datasets is to simulate both internal operational factors and external environmental risks, which are critical in real-world supply chain analytics.
This project combines internal shipment data with external environmental signals to create a more realistic and intelligent risk prediction system.
The datasets were originally available in multiple CSV formats.
The weather dataset consisted of separate files for each attribute (temperature, humidity, pressure, etc.), organized across time and cities.

To prepare the data for analysis:
Multiple CSV files were ingested into the system.
Data was standardized into a unified schema.
Time-based alignment was ensured.
Structured tables were created for downstream processing.
This step reflects real-world data engineering challenges, where data is fragmented and requires transformation before it can be used for analytics or machine learning.

----

## Data Architecture & Pipeline Design:
This project follows the Medallion Architecture (Bronze → Silver → Gold) to ensure a structured and scalable data pipeline.
In the Bronze layer, raw data is ingested without transformations to preserve original data integrity. This includes shipment data and weather-related data.
In the Silver layer, data is cleaned, standardized, and transformed. This involves restructuring datasets, handling inconsistencies, and preparing data for downstream processing.
In the Gold layer, the data is enriched with business logic and feature engineering. 
This layer contains:
ML-ready datasets.
Prediction outputs.
Aggregated analytics tables for dashboards.
The pipeline ensures clear separation between raw, processed, and analytical data, improving maintainability and scalability.
All datasets are stored as managed tables in Databricks, ensuring efficient querying and integration across notebooks.

----


## Data Understanding & Feature Engineering:
The dataset consists of shipment-level information such as:
Customer interactions. (customer care calls, ratings)
Product attributes. (cost, importance, weight)
Operational details. (warehouse block, shipment mode)
The target variable is whether the shipment was delivered on time or delayed.

Feature engineering plays a critical role in improving model performance. 
In this project:
Categorical variables like shipment mode, warehouse block, and product importance were encoded using StringIndexer.
A synthetic weather severity index was created to simulate external disruptions.
All features were assembled into a single vector for machine learning.

Data preprocessing included:
Selecting relevant columns.
Converting categorical to numerical.
Structuring the dataset for ML pipeline.
This ensures the data is clean, consistent, and suitable for modeling.

----

## Delta Lake Implementation:
All data layers are implemented using Delta tables, enabling reliable and scalable data management.
Key features used:
ACID transactions ensure data consistency during read/write operations.
Schema enforcement prevents incorrect data ingestion.
Time travel capability allows access to previous versions of data.
Overwrite mode ensures clean updates during pipeline runs.

Additionally, performance optimization techniques such as:
Table optimization.
Efficient storage format.
can be applied for large-scale scenarios.
This makes the system production-ready and aligned with modern data engineering standards.

----

## Model Selection & Technical Reasoning:
The problem is framed as a binary classification task, where the goal is to predict whether a shipment will be delayed.
A Random Forest Classifier was selected for this task because:
It handles both numerical and categorical features effectively.
It captures non-linear relationships.
It is robust to noise and overfitting.

The model also provides feature importance, which helps in understanding key drivers of delay: Discount offered and weight of shipment are the most influential features.

Limitations:
Weather data is simulated, so its impact is limited.
Model performance can improve with real-world external data.

----

## Training, Evaluation & Metrics:
The dataset was split into training and testing sets using an 80/20 ratio:
Training: 8865 records
Testing: 2134 records
The model was evaluated using AUC (Area Under Curve), which is suitable for binary classification: Achieved AUC Score: 0.7399

This indicates that the model has a good ability to distinguish between delayed and non-delayed shipments.
From predictions:
Overall delay risk: 34.91%
This aligns well with real-world expectations.

Trade-offs:
Model favors interpretability and robustness over extreme accuracy.
Can be further tuned for improvement.

----

## MLflow Experiment Tracking:
MLflow was used to manage the machine learning lifecycle.

During model training:
Parameters such as number of trees were logged.
Evaluation metric (AUC) was recorded.
Each run was tracked for reproducibility.

This allows:
Comparing different model runs.
Tracking improvements.
Managing model versions.

This ensures transparency and reproducibility in the ML pipeline.

----

## Data Pipeline ↔ AI Workflow Integration:
The project integrates data engineering and machine learning seamlessly.

Data is ingested and stored in Bronze layer.
Cleaned and transformed in Silver layer.
Feature engineered in Gold layer.
ML model consumes Gold data.
Predictions are written back to Gold layer.

Final prediction table:   supply_chain_ai.gold.shipping_delay_predictions

This ensures:
End-to-end automation.
Reusability of datasets.
Consistent data flow.

----

## Business Impact & Practical Use:
AI-Powered Supply Chain Risk Intelligence System provides strong business value by converting raw data into actionable insights.
Key insights: 
- 34.91% shipments are at risk of delay.
- Ship mode has highest delay risk. (35.4%)
- Warehouse Block 0 has highest delay probability. (40.08%)

These insights help:
- Logistics teams prioritize shipments.
- Identify high-risk warehouses.
- Optimize shipment modes.

High-risk shipment identification (prediction ≥ 0.7) enables:
- Proactive decision-making.
- Reduced delays.
- Improved customer satisfaction.
- This makes the solution highly practical and impactful.








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

