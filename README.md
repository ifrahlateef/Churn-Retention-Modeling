# Strategic Customer Churn Prediction & Revenue Retention Optimisation
## Project Overview:
Customer churn poses a significant threat to long-term profitability in subscription-based models. This project delivers an end-to-end machine learning solution designed to identify high-risk customers with **91.4% sensitivity** (i.e Recall - ability to catch max possible churners). By leveraging advanced Gradient Boosting (XGBoost) and Bayesian Optimization, this pipeline provides actionable insights that allow for proactive retention, potentially saving significant revenue.<br>
**Key Result**: Achieved an **11% uplift** in model performance through advanced hyperparameter optimisation, leading to a more efficient allocation of marketing resources.

________________________________________
## 1. Data Engineering & Quality Assurance
To ensure the model is built on a reliable foundation, a rigorous data preprocessing and validation pipeline was implemented:<br>
    •	**Data Cleaning:** Handled missing values through statistical imputation and addressed outliers that could skew the decision boundaries of the models.<br>
    •	**Data Validation:** Implemented schema checks to ensure data consistency and integrity, verifying these features (e.g., tenure, monthly charges) fell within logical bounds.<br>
    •	**Preprocessing:** Categorical Encoding(Binary and One-hot encoding): Transformed qualitative data into numerical formats suitable for gradient boosting.<br>
    •	**Feature Scaling:** Standardized numerical variables to ensure uniform contribution to the model's loss function.<br>
________________________________________
## 2. Statistical Exploratory Data Analysis (EDA)
Beyond basic visualization, the project focused on the structural integrity of the feature set:<br>
    •	**Correlation Analysis:** Utilised Pearson correlation matrices to identify linear and non-linear relationships between features and the target variable.<br>
    •	**Multicollinearity (VIF):** Calculated the Variance Inflation Factor (VIF) to detect redundant features.<br>
    •	**Why it matters:** Multicollinearity can inflate the variance of coefficient estimates, making the model unstable and confusing feature importance. Removing highly collinear variables ensures a leaner, more interpretable model.
________________________________________
## 3. Model Development & MLOps Framework:
I benchmarked three high-performance algorithms: **Decision Trees, LightGBM, and XGBoost**. The final selection was **XGBoost** due to its superior handling of sparse data and internal regularization.<br>
    **1. The Optimization Engine (Optuna) -** Instead of traditional grid search, I used Optuna for Bayesian optimisation to find the global minima of the cost function efficiently.<br>
        •	**Winning Parameters:** n_estimators: 796, learning_rate: 0.076, max_depth: 5, and specialized L1/L2 regularization.<br>
    **2. Experiment Tracking (MLflow) -** The entire lifecycle was managed using MLflow, ensuring 100% reproducibility.<br>
        •	**Metrics Logged:** Precision, Recall, F1-Score, and ROC-AUC.<br>
        •	**Artifacts:** The final model was serialized and versioned within the MLflow Model Registry for seamless deployment.
________________________________________
## 4.  Performance & Statistical Metrics
    The model was tuned to prioritize Recall, ensuring that the **business catches as many at-risk customers as possible**.<br>
|**Metric**|**Score**|**Technical Significance**|**Business Value**|
|----|----|----|----|
|**Recall**|91.4|Highly sensitivity via scale-pos_weight|Identifies 9 out of 10 churners|
|**ROC-AUC**|85%|Excellent discriminative power|Effectively ranks customers by risk level|
|**F1 Score**|0.59|Harmonic mean of Precision/Recall|Balanced performance for targeted outreach|
|**Inference Time**|24ms|Low latency prediction|Enables real-time churn triggers in CRM|

    The "Optimal Threshold" Strategy - Through a precision-recall sweep, I adjusted the decision boundary to 0.3.<br>
        •  Why? In churn prediction, the cost of a "False Negative" (losing a customer) is far higher than a "False Positive" (sending a discount to a loyal customer). 
            My strategy prioritizes coverage to maximize revenue retention.<br>
        •  The AUC (Area Under the Curve) represents the probability that the model will rank a random positive (churner) higher than a random negative (non-churner).<br>
            A score of 1.0 is perfect, and 0.5 is no better than a coin flip. The higher the ROC-AUC value the better the model performance.
________________________________________
## 5. Business Value & Conclusion
The final model provides a prioritised list of customers likely to churn.<br>
    •	**High-Risk Identification:** By capturing 91.4% of churners, the marketing team can now focus on high-probability saves.<br>
    •	**Operational Efficiency:** With a training time of only 0.36 seconds, the model can be retrained frequently as customer behavior evolves.<br>
    •	**Proactive Strategy:** The integration of probability-based thresholds allows for "tiered" retention—offering bigger incentives to those with the highest churn probability.

________________________________________
## Technical Stack:
Languages: Python (Pandas, NumPy, Scikit-Learn)<br>
    •	**Modeling:** XGBoost, LightGBM, Random Forest<br>
    •	**Optimization:** Optuna (Bayesian Search)<br>
    •	**MLOps:** MLflow (Tracking & Registry)<br>
    •	**Visualization:** Matplotlib, Seaborn, WordCloud  

