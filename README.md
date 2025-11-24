🏠 Advanced House Price Prediction

📋 Executive Summary
Business Goal:
Develop an automated valuation model (AVM) to predict residential property prices with high precision. This solution aims to assist real estate investment funds and agencies in identifying undervalued assets and minimizing risk in market analysis.
Key Achievement:
Achieved a Top 15% ranking on the Kaggle Leaderboard with an RMSLE score of 0.12240, utilizing a Stacking Ensemble architecture and Bayesian Hyperparameter Optimization.

🛠️ Methodology & Approach
The project follows a production-ready Machine Learning pipeline, ensuring data integrity (no leakage) and model interpretability.
1. Exploratory Data Analysis (EDA) & Cleaning
Outlier Detection: Identified and removed structural anomalies (e.g., properties > 4000 sq.ft with abnormally low prices) to prevent regression bias.
Target Transformation: Applied log1p transformation to the target variable (SalePrice) to correct positive skewness and satisfy the normality assumption of linear models.
Correlation Analysis: Filtered multicollinear features and identified key price drivers (OverallQual, GrLivArea).
<img width="876" height="547" alt="download (1)" src="https://github.com/user-attachments/assets/caf88dd4-7b76-415d-b7d3-0a74621a9a7c" />
<img width="1298" height="470" alt="download (2)" src="https://github.com/user-attachments/assets/55efdbd0-f54d-473f-98af-d971894a5f62" />
<img width="1311" height="470" alt="download (3)" src="https://github.com/user-attachments/assets/94503330-d03a-4ae7-a35d-175045acc5f5" />
<img width="851" height="772" alt="download (4)" src="https://github.com/user-attachments/assets/24dfc770-4b01-4566-a3c9-82f73b27e89c" />

2. Advanced Feature Engineering
Imputation Strategy: Implemented domain-specific imputation logic (e.g., filling LotFrontage based on neighborhood medians) instead of simple mean/mode filling.
Feature Construction: Engineered aggregated features such as TotalSF (Total Square Footage) and TotalBath, which demonstrated higher correlation with the target than individual metrics.
Data Integrity: Used sklearn.pipeline and ColumnTransformer to prevent data leakage during preprocessing.
3. Modeling Architecture (Stacking Ensemble)
To minimize variance and improve generalization, a Stacking Ensemble approach was implemented:
Level 1 (Base Models):
ElasticNet & Lasso: For capturing linear relationships and feature selection.
Kernel Ridge Regression (KRR): For capturing non-linear patterns.
Gradient Boosting (sklearn): With Huber loss for robustness against outliers.
Level 2 (Meta Model):
Lasso Regression: Trained on out-of-fold predictions from Level 1 models to correct their biases.
Final Blending:
Weighted average of Stacking Model (70%), XGBoost (15%), and LightGBM (15%).
4. Optimization
Optuna: Used Bayesian optimization for hyperparameter tuning, which is more efficient than standard Grid Search.
🔍 Model Interpretation (XAI)
To ensure the model is trustworthy for business stakeholders, SHAP (SHapley Additive exPlanations) values were analyzed.
<img width="516" height="588" alt="Screenshot 2025-11-19 at 21 49 51" src="https://github.com/user-attachments/assets/c50019dd-45db-4e2d-9156-3bbd5994ff4b" />
<img width="855" height="547" alt="download (5)" src="https://github.com/user-attachments/assets/95a18b60-03e5-4533-977e-261001d4084b" />

Key Business Insights:
Quality over Quantity: OverallQual (Material & Finish Quality) is the single most critical predictor, showing a non-linear exponential impact on price.
Renovation Value: Recent YearRemodAdd significantly boosts valuation, whereas lack of renovation heavily penalizes the price.
Risk Factors: The SaleCondition_Abnorml feature (e.g., foreclosures) acts as a strong negative signal, crucial for risk assessment.
📈 Performance
The model was evaluated using Root Mean Squared Logarithmic Error (RMSLE) to penalize relative errors rather than absolute ones.

Model Architecture	CV Score (RMSLE)
Lasso (Baseline)	0.1095
XGBoost	0.1162
Stacking Ensemble	0.0777 (Train)
Final Kaggle Score	0.12240

Source:
Kaggle - https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques
Egor Volokitin
