# Capstone Project  
**Predicting FDA Approval of Biological Products**  
**Final Report**

---

## 1. Define the Problem Statement

### **Business Understanding**
The FDA approval process for biological products is complex, resource-intensive, and often unpredictable. Manufacturers face significant uncertainty, which impacts strategic decisions around R&D investment and product pipeline management. This project aims to build a machine learning-based predictive model that determines whether a biological product will receive FDA approval based on its attributes such as applicant, BLA type, dosage form, route of administration, and strength.

### **Goals**
- Predict the FDA approval status (approved/rejected) of a biological product.
- Provide actionable insights for manufacturers, healthcare providers, and regulatory stakeholders.
- Identify key factors influencing approval outcomes.

### **Challenges**
- Data limitations and potential inconsistencies in regulatory records.
- Imbalanced or biased approval patterns.
- Variability in categorical features such as dosage or route of administration.

### **Benefits**
- Helps manufacturers reduce risk and better allocate resources.
- Assists healthcare professionals in anticipating treatment options.
- Informs policy makers about patterns in the FDA approval process.

---

## 2. Model Outcomes or Predictions

- **Type of Learning**: **Supervised Learning**
- **Learning Task**: **Binary Classification** (Approved vs. Not Approved)
- **Models Used**:
  - Logistic Regression
  - Decision Tree
  - Support Vector Machine (SVM)
  - K-Nearest Neighbors (KNN)
  - Random Forest Classifier
  - XGBoost Classifier
  - Stacking Ensemble (meta-model combining top base models)
- **Expected Output**: A binary label predicting the likelihood of FDA approval.

---

## 3. Data Acquisition

### **Data Source**
- **Primary Dataset**: FDA Purple Book  
  Source: [FDA Purple Book Database](https://purplebooksearch.fda.gov/)  
  Description: Contains information on FDA-licensed biological products, including biosimilars and their reference products.

### **Data Exploration and Visualization**
- Initial assessment showed categorical dominance, missing approval dates, and inconsistent formatting.
- A heatmap was used to visualize missing values.
- Count plots and bar charts showed distribution of products by applicant, dosage, and route.

---

## 4. Data Preprocessing / Preparation

### a. **Data Cleaning Techniques**
- Removed duplicates and invalid entries.
- Imputed missing categorical values using mode imputation.
- Created a target column: `Approval_Status_binary` based on marketing status and approval date.
- Removed records with conflicting or missing target values.

### b. **Data Splitting**
- Dataset was split into:
  - **Training Set**: 80%
  - **Test Set**: 20%
- Stratification was used to maintain class balance in both sets.

### c. **Feature Engineering & Encoding**
- Converted categorical features using one-hot encoding and label encoding.
- StandardScaler was applied to normalize numerical features.
- Features selected included:
  - Applicant
  - BLA Type
  - Dosage Form
  - Route
  - Strength

---

## 5. Modeling

### **Models Selected**
- **Baseline Models**: 
  - Logistic Regression
  - Decision Tree
  - Support Vector Machine (SVM)
  - K-Nearest Neighbors (KNN)

- **Advanced Models**: 
  - Random Forest
  - XGBoost

- **Ensemble Method**: 
  - Stacking Classifier using Random Forest, XGBoost, and Logistic Regression as base learners with Logistic Regression as meta-learner

---

## 6. Model Evaluation

### a. **Performance Metrics**
- **Accuracy**, **Precision**, **Recall**, and **F1-score** on the test set
- **Cross-validation (5-fold)** to ensure generalizability
- **Train-Test Comparison** to check for overfitting

### b. **Test Set Results Summary**

| Model               | Accuracy | Precision | Recall | F1-Score |
|---------------------|----------|-----------|--------|----------|
| Logistic Regression | 0.71     | 0.79      | 0.71   | 0.74     |
| KNN                 | 0.80     | 0.82      | 0.80   | 0.81     |
| Decision Tree       | 0.82     | 0.84      | 0.82   | 0.83     |
| SVM                 | 0.76     | 0.82      | 0.76   | 0.78     |
| Random Forest       | 0.84     | 0.85      | 0.84   | 0.85     |
| XGBoost             | 0.86     | 0.86      | 0.86   | 0.86     |
| Stacking Ensemble   | 0.86     | 0.86      | 0.86   | 0.86     |

### c. **Cross-Validation Results (5-Fold)**

| Model               | Mean Accuracy | Std Deviation |
|---------------------|----------------|----------------|
| Logistic Regression | 0.68           | 0.08           |
| KNN                 | 0.66           | 0.03           |
| Decision Tree       | 0.64           | 0.11           |
| SVM                 | 0.68           | 0.06           |
| Random Forest       | 0.69           | 0.05           |
| XGBoost             | 0.66           | 0.07           |
| Stacking Ensemble   | **0.76**       | **0.01**       |

### d. **Improvement Post-Tuning**

| Model               | Test Accuracy Before | Test Accuracy After | Comments                                 |
|---------------------|----------------------|----------------------|------------------------------------------|
| Logistic Regression | 0.71                 | 0.71                 | No improvement; model likely at capacity.|
| KNN                 | 0.78                 | 0.80                 | Minor improvement from K tuning.         |
| Decision Tree       | 0.83                 | 0.82                 | Slight drop; may need less regularization.|
| SVM                 | 0.73                 | 0.76                 | Tuning improved margin separation.       |
| Random Forest       | 0.85                 | 0.84                 | Slight drop; may be variance-based.      |
| XGBoost             | 0.83                 | 0.86                 | Significant improvement post-tuning.     |

---

## 7. Findings

### **Key Insights**
- **XGBoost and Stacking Ensemble performed best**, achieving **86% accuracy**.
- **Route of administration and dosage form** were among the most impactful features.
- **Simpler models like Logistic Regression underperformed**, suggesting non-linearity in the data.
- Ensemble methods improved both accuracy and model robustness.

### **Interpretation for Non-Technical Stakeholders**
- Products with certain dosage forms and routes (e.g., intravenous vs. subcutaneous) show higher historical approval rates.
- Ensemble models can accurately mimic regulatory decision-making and reduce uncertainty in drug development.
- Predictive analytics can provide early warning signals for non-approvable filings.

---

## 8. Next Steps and Recommendations

1. **Operationalization**
   - Deploy the stacking model in a dashboard for internal use by pharmaceutical companies or regulators.
2. **Model Explainability**
   - Use SHAP values to identify which product features influence predictions most.
3. **Data Expansion**
   - Include supplementary datasets (e.g., clinical trial data, manufacturing facility ratings).
4. **Model Monitoring**
   - Refresh model with updated FDA data every quarter to maintain relevance.
5. **User Education**
   - Provide product teams with decision support documentation and visualizations for intuitive interpretation.

---

## Appendix: Business Impact Summary

| Stakeholder             | Value Delivered                                         |
|-------------------------|----------------------------------------------------------|
| **Manufacturers**       | Better predict success, reduce investment risk           |
| **Healthcare Providers**| Faster insight into treatment availability               |
| **Regulatory Agencies** | Data-driven policy decisions and process efficiency      |
