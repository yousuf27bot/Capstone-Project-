# AI-Driven Bridge Condition Prediction & Maintenance Urgency Classification
Team: Muhammad Ammar, Wasif Ahmed Mir, Muntazir Zaidi, Yousuf uddin Ahmed 

## Project Overview

This project focuses on predicting future bridge condition and maintenance urgency using historical bridge inspection data from the National Bridge Inventory (NBI). The main goal is to support proactive bridge maintenance planning by using machine learning and deep learning models to identify bridges that may require earlier attention.

The project compares classical machine learning models with a deep learning time-series model to determine which approach performs better for 5-year bridge condition prediction.

---

## Problem Statement

Bridge infrastructure degradation creates major safety risks, traffic disruptions, and high repair costs. Traditional bridge inspections are often periodic and reactive, meaning maintenance action may only be taken after visible deterioration is observed.

This project uses AI/ML techniques to predict future bridge condition and classify maintenance urgency, helping support earlier and more informed maintenance decisions.

---

## Dataset

- **Source:** National Bridge Inventory (NBI) — Georgia Bridges. [Dataset link](https://www.kaggle.com/datasets/cynthiamengyuanli/nbi-data-1990-2022/data)
- **Time Period:** 1990–2022
- **Original Dataset Size:** 425,638 rows × 42 columns
- **Final Cleaned Dataset Size:** 192,565 rows × 32 features
- **Final Bridges Used:** 7,956 bridges with sufficient historical data

The dataset contains bridge structural details, traffic information, condition ratings, environmental variables, and geographic information.

---

## Key Features

The dataset includes the following types of features:

- **Structural features:** bridge age, deck area, roadway width, number of spans, maximum span length
- **Traffic features:** average daily traffic, truck percentage, truck volume, future traffic estimates
- **Environmental features:** humidity, average temperature, maximum temperature, minimum temperature, wind speed
- **Condition features:** deck condition, superstructure condition, substructure condition
- **Categorical features:** bridge material and design type
- **Geographic features:** latitude and longitude

---

## Methodology

The project followed a complete AI/ML workflow:

1. Data loading and initial inspection
2. Data cleaning and missing value handling
3. Exploratory Data Analysis (EDA)
4. Feature engineering
5. Feature selection
6. Model development
7. Time-series sequence construction
8. Model evaluation
9. Maintenance urgency classification
10. Comparison between classical ML and LSTM

---

## Data Preprocessing

The dataset was cleaned and prepared before model training. Major preprocessing steps included:

- Filtered the dataset to use records from 1998 onward
- Removed irrelevant columns
- Renamed columns for easier understanding
- Removed records with missing critical condition ratings
- Replaced structurally invalid zero values in selected columns
- Converted condition rating columns into numeric format
- Handled missing environmental values using spatial-temporal imputation
- Filled bridge-specific missing values using forward and backward filling
- Removed bridges with insufficient historical records
- Prepared the final dataset for both tabular and time-series modeling

---

## Feature Engineering

Several new features were created to improve model learning:

- **Bridge age:** calculated from inspection year and year built
- **Effective age:** calculated based on reconstruction history
- **Traffic transformations:** log-transformed traffic-related variables
- **Temperature range:** difference between maximum and minimum temperature
- **Composite condition metrics:** minimum and mean condition scores
- **Encoded categorical variables:** material and design were label encoded
- **Future target construction:** future bridge condition was created using a 5-year prediction horizon

---

## Feature Selection

Feature selection was performed to reduce the dataset to the most relevant predictors.

The cleaned modeling dataset was prepared, and **5-year future deck condition** was used as the target variable. Missing values were handled using **median imputation** before feature selection.

Two methods were applied:

- **Mutual Information:** used to identify features with strong non-linear relationships with the target
- **Random Forest Regressor:** used to rank features based on feature importance

The top 12 most influential features were selected for model development.

---

## Models Used

### Classical Machine Learning Models

The following non-time-series machine learning models were applied:

- Ridge Regression
- Decision Tree
- K-Nearest Neighbors
- Random Forest
- XGBoost
- LightGBM

### Deep Learning / Time-Series Model

After converting the dataset into time-series sequences, an LSTM model was applied:

- LSTM using 15-year historical bridge sequences
- Used to capture temporal degradation patterns over time

Random Forest and LSTM were selected for final evaluation because they represent the two main approaches in this project:

- **Random Forest:** best-performing classical ML model for tabular/static features
- **LSTM:** deep learning model for temporal sequence-based prediction

---

## Evaluation Metrics

The models were evaluated using:

- **MAE:** Mean Absolute Error
- **RMSE:** Root Mean Squared Error
- **R²:** Coefficient of Determination

For maintenance urgency classification, classification performance was also considered using accuracy and class-based performance.

---

## Results

The models were evaluated using **MAE, RMSE, and R²** for future bridge condition prediction.

During experimentation, non-time-series models were first applied, followed by time-series modeling using **Random Forest** and **LSTM** after converting the dataset into temporal sequences.

Random Forest achieved the best overall performance among the classical machine learning models. Classical ML models outperformed LSTM on this dataset, showing that the tabular/static features were more useful than sequence patterns for 5-year prediction.

Key results:

- Random Forest achieved the best overall performance among the tested models
- Classical ML models outperformed LSTM in this dataset
- LSTM added temporal complexity but did not improve prediction accuracy
- Tabular/static features were more useful than sequence patterns for 5-year prediction
- Models were evaluated using MAE, RMSE, and R²

---

## Key Findings

- Data structure significantly influenced predictive performance
- Classical ML models performed better than the LSTM sequence model
- More advanced models did not automatically produce better results
- Random Forest provided the best balance between accuracy, interpretability, and practicality
- Temporal sequence modeling added complexity but did not improve final prediction accuracy
- Static/tabular bridge features were more effective for this 5-year prediction task

---

## Maintenance Urgency Classification

The project also included maintenance urgency classification to make the predictions more actionable.

Bridge condition predictions were used to classify maintenance urgency into categories such as:

- **LOW**
- **MEDIUM**
- **HIGH**

This helps convert numerical condition predictions into practical maintenance priority levels.

---

## Engineering Constraints & Trade-offs

The project involved several engineering constraints and trade-offs:

- Random Forest provided stronger accuracy but required more processing than simpler models
- LSTM captured temporal patterns but required 15-year historical bridge sequences
- Using time-series sequences reduced the usable dataset because newer bridges lacked sufficient history
- Environmental variables required imputation due to missing values
- Future traffic values were based on projections rather than actual future measurements
- The final approach balanced accuracy, interpretability, computational cost, and real-world practicality

---

## Ethical Considerations & Explainability

The model was designed for infrastructure decision support, so explainability and fairness were important.

Key considerations:

- The dataset only covers Georgia bridges, so the model may not generalize to other regions
- Historical maintenance patterns may reflect past funding or inspection biases
- No personal or private data was used
- Bridge IDs and locations represent public infrastructure information
- Feature importance and explainability methods were used to understand model behavior

Explainability is important because bridge maintenance decisions can affect public safety and resource allocation.

---

## Solution Improvements

Possible future improvements include:

- Combine Random Forest and LSTM using ensemble stacking
- Add more regional datasets to improve generalization
- Apply cost-sensitive learning to better detect rare high-urgency cases
- Use real-time weather and traffic data for dynamic updates
- Explore Transformer-based time-series models
- Develop a dashboard for bridge maintenance planning
- Include cost estimates for maintenance prioritization

---

## Conclusion

This project developed an AI-based system to predict future bridge condition and maintenance urgency using Georgia NBI bridge data.

The final cleaned dataset contained **192,565 records** from **7,956 bridges**. The project included data preprocessing, feature engineering, feature selection, and evaluation of multiple machine learning and deep learning models.

Random Forest achieved the best overall performance among the tested models, while LSTM did not improve prediction accuracy despite using temporal bridge history. This shows that simpler classical ML models can be more effective when the dataset structure is mainly tabular.

Although individual regression scores were not very strong, the overall system still demonstrated useful predictive capability for bridge condition and maintenance planning.

Final outcomes:

- Built a complete AI/ML pipeline for bridge condition prediction
- Used 192,565 cleaned records and 7,956 bridges
- Compared classical ML models with LSTM-based deep learning
- Identified Random Forest as the most practical and effective model
- Showed that tabular/static features were more useful than temporal sequences for this dataset
- Created a system that can support proactive bridge maintenance decision-making

---

## Tools & Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost
- LightGBM
- TensorFlow / Keras

---
[code collab link](https://colab.research.google.com/drive/1SkNRrNce6dhJAg_5SyrpWB-v4VUYqRSL?usp=sharing)

README.md
