# Predicting Industrial Machine Downtime: Level 3

## Introduction
Minimizing machine downtime is critical for manufacturers of high-precision metal components, especially in industries such as aerospace, automotive, and medical devices. Proactive maintenance, enabled by accurate downtime predictions, can significantly enhance operational efficiency and meet stringent production deadlines.

This project aims to develop a predictive model using machine learning techniques to forecast machine failures based on historical operational data. The model can be integrated with real-time data to detect likely machine failures, allowing for proactive maintenance scheduling.

## Table of Contents
- [Background](#background)
- [Data Overview](#data-overview)
- [Data Exploration and Preprocessing](#data-exploration-and-preprocessing)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Model Development](#model-development)
- [Key Predictors of Machine Downtime](#key-predictors-of-machine-downtime)
- [Conclusions](#conclusions)
- [Recommendations](#recommendations)
- [Dependencies](#dependencies)
- [Author](#author)

## Background
A manufacturer of high-precision metal components operates three different machines on its shop floor. Minimizing the downtime of these machines is vital for meeting production deadlines. The company seeks a data-driven approach to predict machine downtime, enabling proactive maintenance rather than reactive responses to machine failures.

Over a year, the company collected operational data from the machines, including instances of downtime. This project utilizes that data to develop predictive models for machine failure.

## Data Overview
The dataset `machine_downtime.csv` contains 2,500 records of operational data for three machines over a year. Each row represents data from a single machine on a given day.

**Features:**
- **Date:** The date the reading was taken.
- **Machine_ID:** Unique identifier of the machine.
- **Assembly_Line_No:** Unique identifier of the assembly line.
- **Hydraulic_Pressure(bar), Coolant_Pressure(bar), Air_System_Pressure(bar):** Pressure measurements at different points in the machine.
- **Coolant_Temperature, Hydraulic_Oil_Temperature, Spindle_Bearing_Temperature:** Temperature measurements (in Celsius) at different points.
- **Spindle_Vibration, Tool_Vibration:** Vibration measurements (in micrometers).
- **Spindle_Speed(RPM):** Rotational speed of the spindle.
- **Voltage(volts):** Voltage supplied to the machine.
- **Torque(Nm):** Torque generated by the machine.
- **Cutting(kN):** Cutting force of the tool.
- **Downtime:** Indicator of whether the machine was down (Machine_Failure) or not (No_Machine_Failure) on the given day.


## Data Exploration and Preprocessing
### Data Loading and Overview
- Loaded the dataset using pandas and conducted an initial overview.
- Identified missing values in several features.
- Converted the Date column to datetime format and extracted day, month, and day of the week for additional features.

### Data Cleaning
- Filled missing numerical values with the median of each column.
- Encoded categorical variables (Machine_ID, Assembly_Line_No, and Downtime) using Label Encoding.
- Scaled numerical features using StandardScaler to normalize the data.

### Feature Engineering
- Extracted new features from the Date column: Day, Month, and DayOfWeek.
- Dropped the original Date column after extracting necessary information.

## Exploratory Data Analysis
### Target Variable Distribution
- Visualized the distribution of the Downtime variable.
- The dataset was found to be balanced between Machine_Failure and No_Machine_Failure.

### Feature Correlation
- Generated a correlation matrix to identify relationships between features.
- Notable correlations:
  - High correlation between Spindle_Vibration and Tool_Vibration.
  - Significant correlation of Torque(Nm) with Downtime.

### Machine-Specific Analysis
- Analyzed downtime distribution for each machine.
- Observed that downtime occurrences were fairly distributed across the machines.

## Model Development
### Train-Test Split
- Split the dataset into training (80%) and testing (20%) sets.
- Stratified splitting was used to maintain the balance of the target variable in both sets.

### Handling Class Imbalance
- Applied SMOTE (Synthetic Minority Over-sampling Technique) to the training data to address any class imbalance.
- Ensured that the minority class was adequately represented during model training.

### Model Selection and Training
Trained and evaluated four machine learning models:
- Logistic Regression
- Random Forest Classifier
- XGBoost Classifier
- Support Vector Machine (SVM)

Each model was trained using the resampled training data.

### Model Evaluation
- Evaluated models using metrics: Accuracy, Precision, Recall, F1-Score, and ROC-AUC.
- Generated classification reports and plotted ROC curves for each model.

**Results:**
- **Logistic Regression:** Accuracy ~87%, ROC-AUC ~0.94
- **Random Forest:** Accuracy ~99%, ROC-AUC ~0.9998
- **XGBoost:** Accuracy ~99%, ROC-AUC ~0.9998
- **SVM:** Accuracy ~89%, ROC-AUC ~0.96

Random Forest and XGBoost outperformed the other models, achieving near-perfect classification performance.

### Feature Importance
- Calculated feature importance scores using the Random Forest and XGBoost models.
- Identified the top predictors contributing to machine downtime.

## Key Predictors of Machine Downtime
Based on feature importance analysis, the following features are critical indicators of machine downtime:
- **Spindle_Vibration:** High vibration levels indicate potential mechanical issues.
- **Torque(Nm):** Anomalies in torque may signal mechanical failures.
- **Hydraulic_Pressure(bar):** Deviations can indicate hydraulic system problems.
- **Coolant_Temperature:** Overheating may lead to component wear and failures.
- **Spindle_Speed(RPM):** Irregular speeds can reflect operational inefficiencies.

## Conclusions
- Advanced machine learning techniques effectively predict machine downtime.
- Random Forest and XGBoost models achieved near-perfect performance.
- Identified key operational metrics that serve as reliable indicators of machine failures.
- A unified predictive model is recommended for deployment due to its simplicity and high performance.

## Recommendations
### Deploy High-Performance Models for Real-Time Prediction
- **Action:** Integrate the Random Forest or XGBoost model into the manufacturing workflow.
- **Rationale:** These models provide reliable and accurate downtime predictions.

### Focus on Key Predictive Features for Monitoring
- **Action:** Prioritize monitoring of critical features and set thresholds for alerts.
- **Rationale:** Targeted monitoring allows for effective preventive maintenance.

### Integrate Predictive Models with Maintenance Scheduling
- **Action:** Automate maintenance scheduling based on model predictions.
- **Rationale:** Proactive scheduling reduces unexpected downtimes and improves efficiency.

### Maintain and Update the Predictive Models Regularly
- **Action:** Update models with new data and monitor performance metrics.
- **Rationale:** Ensures models remain accurate and adapt to changes over time.

### Enhance Data Collection and Quality
- **Action:** Invest in robust data acquisition systems and implement data integrity protocols.
- **Rationale:** High-quality data is essential for accurate predictions.

### Train and Empower Maintenance Teams
- **Action:** Educate teams on interpreting predictions and responding to alerts.
- **Rationale:** Empowered teams can effectively prevent machine failures.

### Evaluate the Cost-Benefit of Machine-Specific Models
- **Action:** Assess if machine-specific models offer significant performance gains.
- **Rationale:** Balancing complexity with performance ensures optimal resource utilization.

### Explore Advanced Feature Engineering and Model Optimization
- **Action:** Investigate new features and conduct hyperparameter tuning.
- **Rationale:** Continuous improvement can enhance model accuracy and robustness.
  

## Dependencies
- **Python 3.7 or higher**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **Imbalanced-learn**
- **XGBoost**
- **Jupyter Notebook**

## Author
Hafida Belayd

[LinkedIn](https://www.linkedin.com/in/hafida-belayd/)
